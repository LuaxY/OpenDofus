# Les .dlm 

Les fichiers .dlm se trouvent dans les fichiers .d2p 
Une fois apres avoir unpack votre .d2p vous allez vous retrouver avec différents .dlm qui correspondent à vos cartes chaque dossier contient une partie de carte de Dofus, de plus chaque .dlm correspond à une carte en particulière. 
Cependant il y'a certaines exceptions ou d'anciennes cartes persistent dans les .dlm mais n'existent plus dans le jeu, donc ces .dlm la sont "obsoletes"

## La Structure

Apres avoir décompiler un .dlm nous nous retrouvons avec un .json regardons de plus près sa structure : 

![structure](../resources/dev/dlm-struct.PNG)


Nous ne passerons pas en détail sur toute la structure, mais les choses principales sont : 

#### Le mapID : 144692 pour cette map
#### Le subAreaId : 44 qui correspond à la zone de la carte
#### Le Top, Bottom, Left, RightNeighbourID : Qui correspond aux cartes qui se situent autour de notre carte (144692)
#### Le UseReverb : Qui servira aux effets sonores de reverberations. 
#### Le LayerCount : Nombre de Layer sur la carte (systeme de calque style photoshop).
#### Les cells: Les cellules en français 
![cells](../resources/dev/Cellmapping.PNG)

## Voyons maintenant la structure des cellules 

![cells-struct](../resources/dev/layer-dlm.PNG)

Ici simplement nous pouvons voir le nombre d'element sur ce layer, le type d'element (Graphical pour la representation de sprite) l'elementID, qui correspond au sprite, le hue qui permet de gerer la couleur, le type d'ombre, l'offset sert pour le placement dans la carte.

![cells-collision](../resources/dev/cell-collision.PNG)

## Pour finir nous regardons comment Ankama gère les collisions et les zones "non-marchables", 

#### Le mov : Boolean pour savoir si on peut marcher ou non dessus.
#### Le nonWalkableDuringFight et nonWalkableDuringRP : définissent si on peut marcher dessus en combat et si on peut marcher dessus en mode "libre"
#### Le HavenBagCell : Permet d'ajouter ou non des objets en temps réel sur cette case.
