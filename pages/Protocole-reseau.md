Le protocole sur Dofus 2.x est un système de stockage binaire effectué dans un sens appelé Endianness et plus particulièrement en BigEndian.
Pour plus d'informations dessus vous pouvez visiter ce lien : [https://fr.wikipedia.org/wiki/Endianness](https://fr.wikipedia.org/wiki/Endianness)

**La Structure des paquets :**

Les nouveaux paquets de Dofus se déclinent en plusieurs parties représentées comme ceci : 

(PacketID >> MessageLenghtType >> LenghtMessage >> Message)

* Le PacketID représente tout simple le nombre qui permet d'identifier le message reçu.
* Le MessageLenghtType permet de connaître sur combien d'octets la taille est encodée.
* Le LenghtMessage permet de connaître la taille total du Message.
* Le Message permet de récupérer les informations que veut vous donner le serveur ou le client.

**Le Header :** 

L'id du paquet est encodé sur 8 + 6 bits, et le type de taille sur 2 bits. Il faut donc lire 2 octects (short) et il nous faut faire un décalage de 2 bits vers la droite afin de séparer les 2 premiers bits du nombre et obtenir l'id du paquet.

Pour mieux comprendre, voici un petit exemple, nous recevons le paquet d'id 2 (NetworkDataContainerMessage), soit 0000 0000 0000 1001 en binaire.

On effectue notre décalage afin de récupérer l'id du paquet, 0000 0000 0000 0010.

Et nous gardons désormais les bits lorsqu’ils valent tous les deux 1, 0000 0000 0000 0001. Voici notre type de taille, 1.

**La Structure d'un message :** 

La structure des messages de dofus est très simple.
C'est une suite de données inscrites en binaire.
Pour vous donner un exemple je vais prendre le contenue du paquet : Sequence Start Message

Ce paquet permet de dire au client que l'on commence une séquence à jouer avec plusieurs actions.

Code en VB : 
>         Public Overrides Sub serialize(Output As BigEndianWriter)
            Output.WriteByte(sequenceType)
            Output.WriteInt(authorId)
        End Sub

Code en C# : 

>         Public override void Serialize(IDataWriter writer)
        {
            writer.WriteSByte(sequenceType);
            writer.WriteInt(authorId);
        }


**Liens Utiles et Remerciements :**

Reader / Writer en C# par Alexandre1004 : [Lien GitHub](https://github.com/alexandre10044/Dofus-2.27-IO)

Reader / Writer en VB par Neross : [Lien GitHub](https://github.com/yebou/BigEndian)

Merci à Alexandre pour la rédaction de la partie du Header.
