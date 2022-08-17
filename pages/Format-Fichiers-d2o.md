# La structure

Pour chaque fichier D2O vous aurez toujours (normalement si le fichier n'est pas protégé) 3 bytes à convertir en UTF8 qui vous donneront "D2O" (quelle surprise).

Vous aurez ensuite un int contenant l'index de démarrage de l'index table. Elle sert à aller chercher vos données, elle se décompose toujours de la même manière :
Un int contenant la taille de la table, sur lequel vous devez itérer de 0 à ce nombre en avançant votre pointeur de 8 en 8. Dans chaque itération vous allez récupérer 2 choses, un ID, et une position, conservez les deux.

Déplacez vous donc à cette index que vous avez récupérer juste après "D2O" et extrayez là.

Une fois cette index table récupérée, vous pouvez récupérer les structure des données.
Vous allez donc récupérer un int qui sera le nombre de structures dans le fichier, vous allez donc itérer d'un index de 0 à ce nombre en avançant de 1 par 1.
Pour chaque structure vous aurez :
- classId : int
- className : UTF8
- packageName : UTF8
- fieldsCount : int

Voilà bravo vous avez la moitié de votre structure (gg), maintenant récupérons les champs. Chacun est composé de 2 choses :
- name : UTF8
- type : int

Les types possibles sont les suivant :
int = -1 (méthodes readInt, writeInt)
bool = -2 (méthodes readBool, writeBool)
string = -3 (méthodes readUTF, writeUTF)
double = -4 (méthodes readDouble, writeDouble)
i18n = -5 (se comporte comme un int)
uint = -6 (méthodes readUInt, writeUInt)
list = -99

Précision, si le type est liste, le suivant sera son type interne, attention, il peut aussi être de type liste, et donc vous devez aller aussi profondément que nécessaire (c'est dégueulasse sorti du contexte, bande de porcs).

Si le type est différent de tout ceux là, alors il sera basé sur une structure, et donc le type correspondra à l'id de la structure.

Source au niveau du client (com.ankamagames.jerakine.data.GameDataFileAccessor.as) :

   public function initFromIDataInput(stream:IDataInput, moduleName:String) : void
  {
           var key:int = 0;
           var pointer:int = 0;
           var count:uint = 0;
           var classIdentifier:int = 0;
           var formatVersion:uint = 0;
           var len:uint = 0;
           if(!this._streams)
           {
              this._streams = new Dictionary();
           }
           if(!this._indexes)
           {
              this._indexes = new Dictionary();
           }
           if(!this._classes)
           {
              this._classes = new Dictionary();
           }
           if(!this._counter)
           {
              this._counter = new Dictionary();
           }
           if(!this._streamStartIndex)
           {
              this._streamStartIndex = new Dictionary();
           }
           if(!this._gameDataProcessor)
           {
              this._gameDataProcessor = new Dictionary();
           }
           this._streams[moduleName] = stream;
           if(!this._streamStartIndex[moduleName])
           {
              this._streamStartIndex[moduleName] = 7;
           }
           var indexes:Dictionary = new Dictionary();
           this._indexes[moduleName] = indexes;
           var contentOffset:uint = 0;
           var headers:String = stream.readMultiByte(3,"ASCII");
           if(headers != "D2O")
           {
              stream["position"] = 0;
              try
              {
                 headers = stream.readUTF();
              }
              catch(e:Error)
              {
              }
              if(headers != Signature.ANKAMA_SIGNED_FILE_HEADER)
              {
                 throw new Error("Malformated game data file. (AKSF)");
              }
              formatVersion = stream.readShort();
              len = stream.readInt();
              stream["position"] = stream["position"] + len;
              contentOffset = stream["position"];
              this._streamStartIndex[moduleName] = contentOffset + 7;
              headers = stream.readMultiByte(3,"ASCII");
              if(headers != "D2O")
              {
                 throw new Error("Malformated game data file. (D2O)");
              }
           }
           var indexesPointer:int = stream.readInt();
           stream["position"] = contentOffset + indexesPointer;
           var indexesLength:int = stream.readInt();
           for(var i:uint = 0; i < indexesLength; i = i + 8)
           {
              key = stream.readInt();
              pointer = stream.readInt();
              indexes[key] = contentOffset + pointer;
              count++;
           }
           this._counter[moduleName] = count;
           var classes:Dictionary = new Dictionary();
           this._classes[moduleName] = classes;
           var classesCount:int = stream.readInt();
           for(var j:uint = 0; j < classesCount; j++)
           {
              classIdentifier = stream.readInt();
              this.readClassDefinition(classIdentifier,stream,classes);
           }
           if(stream.bytesAvailable)
           {
              this._gameDataProcessor[moduleName] = new GameDataProcess(stream);
           }
  }

  private function readClassDefinition(classId:int, stream:IDataInput, store:Dictionary) : void
  {
           var fieldName:String = null;
           var fieldType:int = 0;
           var className:String = stream.readUTF();
           var packageName:String = stream.readUTF();
           var classDef:GameDataClassDefinition = new GameDataClassDefinition(packageName,className);
           var fieldsCount:int = stream.readInt();
           for(var i:uint = 0; i < fieldsCount; i++)
           {
              fieldName = stream.readUTF();
              classDef.addField(fieldName,stream);
           }
           store[classId] = classDef;
  }
