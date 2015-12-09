Les scripts Lua permettent d’interagir avec le client Dofus pour créer des scénario pour des événements. Les actions des scripts sont virtuelles : elles n'agissent que dans le client, les autres joueurs ne voient les effets du scripts. Mais il est possible sur des serveur privé de pouvoir déployer et lancer le script à distance pour que tous les joueurs puissent suivre l'événement.

Vous allez pouvoir invoquer des PNJs ou monstres, les faire parler, ce déplacer, effectuer des actions spécifiques, etc...

Vous pouvez apprendre les base du langage lua en suivant ces deux liens :

- [Les bases du Lua (Wikipedia)](https://fr.wikipedia.org/wiki/Lua)
- [Manuel de référence](http://www.lua.org/manual/5.1/manual.html)

## Pré-requis

- [Client bêta](http://forum.dofus.com/fr/1557-discussions-generales/1906976-telechargement-client-beta)
- [Mode développement](Mode-developpement.md)

## Scripts Lua

### SDK

La première chose à faire est de télécharger le SDK pour les modules : [lien vers la dernière version](https://github.com/OpenDofus/wiki/releases/tag/sdk-lua)

Le SDK contient trois choses actuellement :

- La documentation des API disponibles
- La liste des informations sur les monstres, pnj et objets pour pouvoir les utiliser dans les scripts Lua
- Un exemple de script qui affiche un monstre sur la map

### Créer et lancer un script

Il existe deux manière de lancer un script Lua :

- Utiliser la commande `/lua {path/to/script.lua}` dans la console
- Utiliser la fenêtre dédié aux script Lua (`/luarecorder` dans la console), [en savoir plus](Mode-developpement.md)

### LuaRecorder

![Lua](../resources/dev/dev-lua.png)

Pour vous aider à créer des scripts facilement, le LuaRecorder est un petit utilitaire qui va convertir les actions que vous faites dans le client directement Lua. 
Pour l'afficher, utilisez la commande `/luarecorder` dans la console ou modifiez le fichier de configuration secondaire pour l'afficher par défaut au lancement du client 

Le LuaRecorder n'en est qu'à ses début, il n'enregistre pas tout mais il s'étoffera au fur et à mesure. 
