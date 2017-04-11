## ProtocolRequiredMessage.
<b>
Id: 1.<p>
Contexte: Authentification.<p></b>
Description: Ce message est envoyé au client lors de sa connexion il contient deux paramètres:



## RequiredVersion (Int) 
Description: Represente la version minimum du protocole du serveur, le client doit posséder la même afin de communiquer correctement avec lui.

## CurrentVersion (Int)
Description: Représente la version actuelle du protocole serveur, en principe, elle correspond a celui du client.


Remarque: Si la version du protocole client est inferieur a la version requise, le client ne pourra pas se connecter au serveur.

![alt tag](http://i.imgur.com/GwmfFHo.png)



