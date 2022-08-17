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

### La table 

Pour la récupérer vous devez :
- Vérifier qu'ils reste des choses à lire dans votre fichier
- Récupérer un int comprenant la taille de la table, stockez ça dans une variable
- Définir l'indexSearchOffset qui correspond à : pointeur actuel (position du curseur) + taille de la table + 4

Itérez ensuite tant que TailleDeLaTable > 0, vous allez donc maintenant :
- Déclarer une variable size contenant le nombre de bytes disponibles à la lecture

Puis lire :
- fileldName : UTF8
- Index de départ des données : int puis ajoutez indexSearchOffset
- Type de donnée : int
- Nombre de données : int

Pour finir décrémenter fieldListSize de fieldListSize - size - nombre de bytes disponibles à la lecture


Exception pour les listes et types spéciaux (qui se réfèrent à des classes) :
- Si votre type est une liste, vous devez lire un int indiquant la taille de la liste.
- Si votre type est une structure (id > 0) alors vous devez lire un int correspondant à l'id de la structure que vous devez suivre pour récupérer les données (attention, il peut être différent du type que vous avez eu lors de la récupération de la structure, exemple pour le fichier Items.d2o, possibleEffects est défini de type 1 (EffectInstance donc) mais lors de la lecture des données le type envoyé est 3 (EffectInstanceDice))

On a presque fini ! Il reste un dernier détail, vous vous souvenez de la search table ? Voilà donc son fonctionnement.
Avec les indexes que vous avez récupéré en la lisant (SearchFieldIndex dans mon exemple) vous pouvez naviguer à la manière de l'index table.

Comment elle se compose ?

En ayant bien analysé la search table contient en fait les index de recherche pour une valeur X. En gros, si un champ est défini comme "queryable" il sera donc présent dans cette table.
Elle se présente sous cette forme (pour chaque "queryable" field) :
- Une valeur X qui sera lu en fonction du type de la field (SearchFieldType[field] dans mon exemple)
- Une valeur int à multiplier par 0.25 qui correspond au nombres d'index dans la liste
- Une liste de valeurs int sur laquelle vous devez itéré X fois en fonction du nombre défini par ce que je viens d'expliquer juste au dessus, ces valeurs correspondent aux indexes dans l'index table)

Comment elle marche ?

Elle sert en fait à effectuer une recherche plus rapidement, elle groupe donc les données qui possèdent une même valeur pour un champ donné.

Exemple :

J'ai une structure de donnée Item composée de 2 champs : Nom et Niveau
J'ai 3 entrées dans mon fichier :

1 - Nom: Test, Niveau: 100
2 - Nom: Test 2, Niveau: 150
3 - Nom: Test 3, Niveau 100

Ma search table a le champ "Niveau" "queryable", elle sera donc :

Valeur | Nombre d'entrées (divisé par 0.25) | Liste d'indexes
100 8 1,3
150 4 2


## Pour plus d'infos : 

https://cadernis.com/index.php?threads/comprendre-les-fichiers-d2o-il-serait-temps.2568/ (basé sur ça)
