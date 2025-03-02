# Communication_Mode_TCP_UDP_Sous_Unix
# **1- Contexte du projet** :
Ce projet s'inscrit dans le cadre du cours de Programmation Système et Réseaux sous UNIX, qui met l'accent sur la compréhension et la mise en œuvre des concepts fondamentaux des sockets et des communications réseau en environnement Unix/Linux.
Le projet vise à développer deux applications client/serveur en utilisant les protocoles UDP (mode non connecté) et TCP (mode connecté) qui doit être réalisée en quatre étapes :
-	Monoclient/monoserveur
-	Multiclient/mmnoserveur
-	Multiclent/multiserveur
# **2- Mode non-connecté (UDP)** :
<ul>
<li> <strong> ClientUDP.c : </strong>  </li>
Les étapes principales du code `clientudp.c` sont :
<ol>
    <li>Vérifier les arguments (hôte et port).</li>
    <li>Créer un socket UDP.</li>
    <li>Configurer l'adresse du serveur.</li>
    <li>Générer un nombre aléatoire et préparer un message.</li>
    <li>Envoyer et recevoir le message au serveur.</li>
    <li>Afficher les valeurs reçues.</li>
    <li>Fermer le socket.</li>
</ol>
</ul>


<ul>
<li> <strong> ServeurUDP.c : </strong> </li>
Les étapes principales du code `ServeurUDP.c` sont :
<ol> <li> Vérifier les arguments (port uniquement).</li> 
     <li> Créer un socket UDP.</li> 
     <li> Configurer et lier l'adresse du serveur.</li> 
     <li> Recevoir un message du client.</li> 
     <li> Générer une séquence aléatoire en fonction de la requête.</li> 
     <li> Envoyer la réponse au client.</li> 
     <li> Fermer le socket.</li> 
</ol>
</ul> 


>logger.c : Fournit des fonctionnalités pour enregistrer, afficher et gérer des logs dans un programme.
>
>make.sh : Script shell qui sert à compiler les fichiers sources en générant les exécutables correspondants.


# **3- Mode connecté (TCP)** :
## **3.1- Monoclient/monoserveur** :
<ul>
<li> <strong> ClientTCP.c : </strong>  </li>
Les étapes principales du code `clientTcp.c` sont :
<ol> <li> Connexion au serveur.</li> 
     <li> Authentification.</li> 
     <li> Envoi de commandes via une boucle.</li> 
     <li> Réception des résultats et affichage.</li> 
     <li> Fin de session avec l'opération 5.</li> 
     <li> Fermer le socket.</li> 
</ol>
</ul>


<ul>
<li> <strong> ServeurTCP.c : </strong> </li>
Les étapes principales du code `ServeurTCP.c` sont :
<ol> <li> Initialisation du serveur.</li> 
     <li> Acceptation des connexions client.</li> 
     <li> Authentification sécurisée.</li> 
     <li> Envoi du menu d'options.</li> 
     <li> Traitement des requêtes client (services variés).</li> 
     <li> Fermeture des connexions.</li> 
</ol>
</ul> 


## **3.2- Multiclient/monoserveur** :
<ul>
<li> <strong> ServeurTCP.c : </strong> </li>
<ul>
<li>Le serveur utilise des threads pour gérer plusieurs clients simultanément.</li>
<li>Chaque client est traité dans un thread distinct, permettant un traitement parallèle.</li>
<li>Le serveur accepte plusieurs connexions avec safe_accept dans une boucle infinie.</li>
<li>Pour chaque connexion, un thread est créé avec pthread_create pour gérer le client.</li>
<li>Les threads doivent partager certaines ressources (comme le compteur active_clients).</li>
<li>Synchronisation nécessaire pour éviter les conflits : <br>
            Utilisation de mutex avec `pthread_mutex_lock` et pthread_mutex_unlock. <br>
            <strong> Exemple : </strong> Mise à jour du compteur active_clients pour suivre les connexions actives.</li>

</ul>
</ul>


## **3.2- Multiclient/multiserveur** :
<ul>
<li> <strong> Proxy.c: </strong> </li>
</ul>
<ol><li> Centralisation des connexions : </li>
        Le proxy reçoit toutes les requêtes des clients et décide à quel serveur spécifique (authentification, date, liste de fichiers, etc.) rediriger chaque requête.
        Il agit comme un intermédiaire entre les clients et les serveurs de services.
     <li>  Routage des requêtes : </li>
        Basé sur l'opération demandée (message.op), le proxy redirige les requêtes vers le serveur approprié.
        Cela permet de découpler les clients des serveurs de services, rendant l'architecture plus modulaire et maintenable.
     <li> Gestion des connexions multi-clients : </li>
        Utilise des threads pour gérer plusieurs clients en parallèle, chaque client ayant son propre thread.
        Cela permet une gestion simultanée de plusieurs connexions.
     <li> Abstraction de la logique métier côté client : </li>
        Les clients n'ont pas besoin de savoir quel serveur gère une opération spécifique. Ils communiquent simplement avec le proxy, qui se charge de rediriger la requête vers le bon serveur.
</ol>


>Cette classe sert donc de cœur de l'architecture client-proxy-serveurs et illustre bien les principes de modularité, de découplage et de gestion réseau centralisée.

<ul>
<li> <strong> Exemple dimplementation d'un serveur (serveur_auth.c) : </strong> </li>
</ul>
     <ol><li> Vérification des identifiants :</li>Le serveur reçoit les identifiants (nom d'utilisateur et mot de passe) du client.Il utilise une fonction appelée authentification pour valider ces informations.
          <li>Filtrage des clients non autorisés :</li>Si l'authentification échoue, le client est invité à réessayer.Le client ne peut pas accéder aux autres services sans une authentification réussie.
          <li>Point d'entrée pour les services :</li>Une fois l'utilisateur authentifié, le serveur fournit un menu d'options indiquant les autres services disponibles (date, liste de fichiers, contenu d’un fichier, etc.).
          <li>Gestion multi-clients :</li>Le serveur utilise des threads pour traiter plusieurs clients simultanément.
     </ol>

## **3.3- Compilation** :
Le fichier make.sh permet de compiler facilement les différents composants du système multiclients/multiserveurs. Il prend un argument pour décider si l'utilisateur veut compiler les serveurs ou le client, simplifiant ainsi le processus de génération des exécutables.
<ul>
<li> <strong> Exemple de fichier make.sh pour Multiclients/multiserveurs : </strong> </li>
</ul>

![make](./assets/make.jpg)
## **3.4- Comparaison** :
![comp](./assets/comparaison.jpg)

>L'utilisation de threads au lieu de fork pour gérer les clients dans un environnement multiclients présente plusieurs avantages significatifs, notamment en termes de performance, de gestion des ressources, et de simplicité.

![threadVSfork](./assets/thread_fork.jpg)

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
