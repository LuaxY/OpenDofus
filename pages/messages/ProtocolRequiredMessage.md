## ProtocolRequiredMessage
<p>
Id: 1
<p>
Context: Authentification
<p>

Description: Ce message est envoyé au client dès le premier signe a sa connection il contient deux paramètres:

<p>

## RequiredVersion
<p>
Type : Int <p>
Description: Represente la version minimum du protocole du serveur, le client doit posséder la même afin de communiquer correctement avec lui.
<p>
## CurrentVersion
<p>
Type : Int <p>
Description: Représente la version actuelle du protocole serveur, en principe, elle correspond a celui du client.



