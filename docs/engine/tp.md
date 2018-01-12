# TP0 : mes premiers conteneurs

## Hello-world

Pour tester votre installation :

```
docker run hello-world
```

La commande par défaut de cette image affiche un message confirmant la bonne installation de *Docker Engine*.

- Observez que le conteneur est bien existant et à l'arrêt
- Supprimez le.
- Testez l'option `--rm`

## Images

- Affichez la liste des images, supprimez l'image `hello-world`
- Téléchargez l'image debian 9 (pour trouver la bonne image et le bon tag, rendez-vous sur hub.docker.com)
- Affichez les métadonnées de l'image téléchargée

## Container

- Démarrez un bash interactif de l'image debian, observez le nom d'hôte apparent dans le conteneur
- Testez les options `-d`, `-w`, `-h` et `--name` 

## Volumes

- Démarrez un bash interactif de l'image debian, en montant la racine de la machine hôte sur `/host` en mode lecture seule dans le container
- Démarrez un bash interactif avec un volume docker sur `/data`, créer un fichier avec la commande `touch /data/toto`
- Affichez la liste des volumes
- Détruisez et relancez le même conteneur, observez le contenu de `/data`
- Démarrez un second conteneur identique et afficher le contenu de `/data`. 
- Testez l'option `-v` de la commande `docker rm`

## Réseau

- Affichez la liste des interfaces d'un conteneur avec la commande `ip a`
- Dans un conteneur avec l'option `--net host`, afficher les interfaces réseaux
- Démarrez un conteneur basé sur l'image [https://hub.docker.com/r/emilevauge/whoami/](https://hub.docker.com/r/emilevauge/whoami/)
- Dans un navigateur, consultez la page à l'ip du conteneur (aide : [https://github.com/emilevauge/whoamI](https://github.com/emilevauge/whoamI))
- Relancer un conteneur déclarant l'exposition du port 80 (option `-p 80`), utilisez la commande `docker container port` pour connaître le port d'exposition, tentez d'accéder au serveur du voisin
- Cette fois-ci, utilisez l'option `-p` pour exposer le port 80 du conteneur sur le port 8080 de la machine hôte.

# TP1 : un serveur nextcloud

Le but est de mettre en place NextCloud, un gestionnaire de fichier.
L'image à utiliser est nextcloud, disponible sur [https://hub.docker.com/_/nextcloud/](https://hub.docker.com/_/nextcloud/). Cette page contient beaucoup de détails que vous pouvez trouver dans les métadonnées de l'image.

## Etape 1 : un serveur simple avec une base de données SQLite (un fichier)

- Lancez un conteneur exposant sur le port 8080 de la machine hôte le serveur nextcloud et rendez-vous sur [http://127.0.0.1:8080](http://127.0.0.1:8080) pour accéder à l'interface d'initialisation du serveur.
- Ajoutez des volumes pour que les données soient préservées lorsque le conteneur est détruit (et vérifiez que c'est bien le cas...)


## Etape 2 : utiliser une base de données externe MySql

- Lancer un conteneur MySQL
- Recréez le conteneur nextcloud avec les bonnes options pour qu'à la configuration, vous puissiez lui dire d'utiliser la base de donnée mise en place.

# TP3 : un dockerfile pour Geoserver

Ecrire un dockerfile pour créer une image de Geoserver 2.12, basée sur l'image `tomcat`.
Documentation utile : [http://docs.geoserver.org/2.12.1/user/installation/war.html#installation-war](http://docs.geoserver.org/2.12.1/user/installation/war.html#installation-war).
