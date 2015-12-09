# Format de fichier swl

Le format de fichier swl est un format créer par Ankama pour être utilisé avec typhon, le moteur de jeux de Dofus 2.0, ce format est assez simple, il s’agit d’un wrapper de fichier swf, il contient principalement un fichier swf et la liste des classes de ce dernier, ce qui va permettre à typhon de les appeler, ces classes sont chacune liées à un sprite.

### La structure d’un fichier swl :
- Le header (un entier d’un octet).
- La version (un entier d’un octet).
- Le frame rate (un entier de 4 octets).
- Une liste de chaines de caractères.
- La taille de cette liste (un entier de 4 octets).
- Chaque élément de la liste est une chaine de caractères encodé en utf8, dont la taille est définit par un entier de 2 octets.
- Le fichier swf (qui prend la place restante).

### Le Header :

Il s’agit d’une valeur constante ‘76’, elle sert à vérifier que le fichier est bien un swl.

### La version :

Elle n’est pas utilisée, du moins en 2.29

### Le Frame rate :

Le frame rate du swf.

### Les Classes :

Les classes correspondent aux classes du swf, qui sont chacune reliées à un sprite.  
Ces classes correspondent au tag ‘SymbolClass’ du swf.

### Le fichier swf :

Il s’agit tout simplement d’un fichier swf