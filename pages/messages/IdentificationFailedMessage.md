## IdentificationFailedMessage.
<b>
Id: 20.

Context: Authentification.
</b>

Description: Ce message est envoyé au client lorsque l'authentification échoue.

## Reason (String)
Description: Raison de l'échec d'authentification.

```
[NETWORK] : Process message 'IdentificationMessage'
[DEBUG] : Credentials requested : {"username":"test","password":"abc"}
[NETWORK] : Sended packet 'IdentificationFailedMessage' (id: 20, packetlen: 1, len: 4 -- 2048)
```
![failed](identificationFailed.png)
