## RawDataMessage.
<b>
Id: 6253.<p>
Contexte: Quelconque.<p></b>
Description: Ce message peut être envoyé au client quelque soit le contexte et lui permet d'interpreter du code swf.


## Content (Tableau de byte, byte[]) 
Description: Représente un fichier swf, lors ce que le client reçoit se message, il execute le code swf contenu dans se fichier.

## Exemple de code swf envoyé au client

Code en AS3 (Flash) : 

>         public function Main()
>         {
>            super();
>            var conn:* = getDefinitionByName("com.ankamagames.dofus.kernel.net::ConnectionsHandler");
>            var message:* = new (getDefinitionByName("com.ankamagames.dofus.network.messages.common.basic::BasicPingMessage") as Class)();
>            message.initBasicPingMessage();
>            conn.getConnection().send(message); 
>         }

