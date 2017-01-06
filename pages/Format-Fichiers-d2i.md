# Format de fichier d2i

Le format de fichier d2i est un format créé par Ankama qui a pour but de stocker des chaines de caractères (nom des items, dialogues des pnjs, ...) correspondant à des clés, ce sont les fichiers "lang" du client.

### La structure d’un fichier d2i
* L'index des indexes (int)
* Les données (chaînes de caractères UTF-8 précédées de leur longueur)
* La taille en octets de la table des indexes (int)  
* La table des indexes
    * [--Répétition des 4 prochains points jusqu'à la fin du fichier--]
    * La clé (int)
    * Indicateur diacritique (bool)
    * Le pointeur (int)
    * Le pointeur diacritique (int) (non représenté sur le schéma)

note : dans la représentation ci-dessous il est considéré qu'aucune des données ne comporte de chaine diacritique
![structure](../resources/format-fichiers/d2i/d2i-structure.png)

### L'index des indexes

Correspond à l'offset de la table des indexes.

### Les données

Les données sont des chaînes de caractères au format UTF-8. Chaque chaîne est précédée de sa longueur sur deux octets (short).

### La table des indexes

La taille (en octets) de la table des indexes puis les indexes.

### Les indexes

Les indexes sont composés de 3 ou 4 éléments :

1. La clé : Appelée par exemple dans les fichiers d2o, c'est l'identifiant de la donnée.
2. Indicateur diacritique : Indique s'il existe une donnée diacritique pour cette clé.
3. Pointeur : Emplacement de la chaine dans le fichier.
4. Pointeur diacritique : Emplacement de la chaine diacritique dans le fichier, si l'indicateur diacritique est à true.

# Informations supplémentaires
- [Définition du terme : diacritique](https://fr.wikipedia.org/wiki/Diacritique)
