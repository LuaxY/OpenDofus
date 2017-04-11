## IdentificationMessage.
<b>
Id: 4.

Context: Authentification.
</b>

Description: Ce message est envoyé au serveur lorsque le client rentre ses identifiants, à la connexion.

<p>

## Autoconnect (Bool)
Description: Le client passe t-il par la selection de serveur ou se connecte t-il directement au dernier serveur joué.

## UseCertificate (Bool)
Description: 

## UseLoginToken (Bool)
Description:

## Version (VersionExtended)
Description: Représente la version complète du client dofus en cours de connexion, on vérifie si la version du client est compatible avec celle attendue par le serveur.

## Lang (String)
Description: La langue du client (voir 'd2i')

## Credentials (Tableau de 8 bits signés, sbyte[])
Description: Les informations de connexions du client (identifiants, mot de passe + clé AES a partir du client Dofus 2.33) // a détailler

## ServerId (small int , short)
Description:

## SessionOptionalSalt (long)
Description:

## FailedAttempts (ushort[])
Description:
