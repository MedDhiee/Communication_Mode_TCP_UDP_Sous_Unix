# Jeu de test 

## 1- Compilation :
Pour chaque mode et pour chaque aspect du mode TCP, nous avons compilé les fichiers `make.sh` de la manière suivante :


![comp](assets/compilation.png)

## 2- Exécution (mode TCP) :
### 2.1- Monoclient/monoserveur :
Tout d'abord, nous avons exécuté le serveur : 

![serv](assets/serveurmono.png)

Aprés avoir exécuter le serveur avec succés, nous passons à exécuter le client qui doit etre s'authentifier, puis lancer la demande selon un choix souhaité.


![serv](assets/date.png)

![serv](assets/liste.png)

![serv](assets/contenu.png)
 
![serv](assets/duree.png)

### 2.2- Multiclients/monoserveur :

Aprés avoir exécuter le serveur et 2 clients qui sont authentifiés avec succés, le serveur indique les clients qui sont connectés : 

![serv](assets/serveurmultimono.png)

>Chaque client peut alors demander le service à traiter 

### 2.3- Multiclients/multiserveurs :

Le modèle multiclients-multiserveurs repose sur la communication entre plusieurs clients et plusieurs serveurs via un serveur intermédiaire, souvent appelé proxy;

Nous avons alors exécuter tout d'abord le proxy puis les serveurs qui permet chacun d'entre eux de traiter un service(auth,duree,etc..),enfin nous avons exécuté les clients.

Les clients veulent connaitre leur durées de connexion :

`Client 1` :

![serv](assets/client1duree.png)

`Client 2` :

![serv](assets/clientduree1.png)

`Proxy` :

![serv](assets/proxyduree.png)

`serveur_duree` :

![serv](assets/serveurduree.png)

### 2.4- Interface graphique :

`Authentification` :

![serv](assets/auth.jpeg)

![serv](assets/auth2.jpeg)

`Services` :

![serv](assets/services.jpeg)

`Service_date` :

![serv](assets/date.jpeg)

`Service_liste_fichiers` :

Le client passe en arguments le chemin dans-lequel se trouvent les fichiers 

![serv](assets/ls.jpeg)

![serv](assets/liste.jpeg)

`Service_contenu_fichier` :

Le client passe en arguments le fichier afin d'afficher son contenu

![serv](assets/cat.jpeg)

![serv](assets/contenu.jpeg)

`Service_durée_connexion` :

![serv](assets/duree.jpeg)




