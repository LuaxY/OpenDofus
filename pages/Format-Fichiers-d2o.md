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

### Le code : 
