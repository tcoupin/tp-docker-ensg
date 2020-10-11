Le but est de mettre en place NextCloud, un gestionnaire de fichier en ligne.
L'image à utiliser est nextcloud, disponible sur [https://hub.docker.com/_/nextcloud/](https://hub.docker.com/_/nextcloud/). Cette page contient beaucoup de détails que vous pouvez trouver dans les métadonnées de l'image.

## Etape 1 : un serveur simple avec une base de données SQLite (un fichier)

- Lancez un conteneur exposant sur le port 8080 de la machine hôte le serveur nextcloud et rendez-vous sur [http://127.0.0.1:8080](http://127.0.0.1:8080) pour accéder à l'interface d'initialisation du serveur. Suivre les étapes d'installation.
- Ajoutez des volumes pour que les données soient préservées lorsque le conteneur est détruit (et vérifiez que c'est bien le cas...)


## Etape 2 : utiliser une base de données externe MySql ou Postgresql

- Lancez un conteneur MySQL ou Postgresql (n'oubliez pas les volumes...)
- Recréez le conteneur nextcloud avec les bonnes options pour qu'à la configuration, vous puissiez lui dire d'utiliser la base de donnée mise en place.
