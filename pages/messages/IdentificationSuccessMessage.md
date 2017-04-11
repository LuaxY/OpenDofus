## IdentificationSuccessMessage.
<b>
Id: 22.<p>
Contexte: Authentification.<p></b>
Description: Ce message est envoyé au client lorsque ses identifiants sont corrects:



## HasRights (Bool)
Description: Le client possède t-il des droits administrateurs?

## WasAlreadyConnected (Bool)
Description: Le client était t-il précedament connecté au serveur d'authentification?

## Login (String)
Description: Nom d'utilisateur Dofus.

## Nickname (String)
Description: Pseudo Dofus.

## AccountId (Int)
Description: Id unique du compte Dofus.

## CommunityId (Entier 8 bit signé, sbyte)
Description: Id de la communauté (Ex: Espagnole, Francophone, Anglophone etc...)

## SecretQuestion (String)
Description: Question secrète.

## AccountCreation (Double, nombre a virgule flottante)
Description: Date de la création du compte Unix (https://fr.wikipedia.org/wiki/Heure_Unix).Q

## SubscriptionElapsedDuration (Double)
Description: Temps d'abonnement écoulé Unix (https://fr.wikipedia.org/wiki/Heure_Unix).

## SubscriptionEndDate (Double)
Description: Date de fin d'abonnement Unix (https://fr.wikipedia.org/wiki/Heure_Unix).

## HavenbagAvailableRoom
Description: Cartes du havre sac disponible.

Remarque: Ce message fait passer le client vers la frame:  ServerSelectionFrame

