
## Un dockerfile pour Geoserver

Dans ce TP, nous allons créer une image geoserver. Voici la documentation d'installation [https://docs.geoserver.org/latest/en/user/installation/war.html](https://docs.geoserver.org/latest/en/user/installation/war.html).

Geoserver est une application web écrite en java. Elle se déploit sur un serveur `tomcat` (dans le dossier webapps).
Geoserver utilise un dossier `workspace` comme espace de travail. Elle y stocke sa configuration et ses données.

Voici également quelques instruction pour l'écriture du Dockerfile :

- partir de l'image `tomcat`
- la commande `ADD` permet d'ajouter des fichiers depuis internet vers l'image
- déclarer les volumes où sont stockées les données


## Un dockerfile pour GRR

GRR est une application php de gestion de ressources partagées (planning de réservation de salle de réunion etc...).

Ecrire un dockerfile basé sur une image php permettant de lancer l'application GRR. La base de donnée est bien sûr en dehors de ce conteneur.

## Multi-stage build

> *Jekyll* permet de créer un site web statique à partir de fichier texte écrits en markdown. Il est écrit en ruby et est utilisé notamment par github.


### Prise en main de Jekyll

Docs utiles :

- [Commandes utiles de Jekyll](https://jekyllrb.com/docs/usage/)
- [Thème *minima* pour Jekyll](https://github.com/jekyll/minima)
- Image officielle : `jekyll/jekyll`

Ecrire un Dockerfile se basant sur l'image officielle de Jekyll, qui créé un nouveau projet : `jekyll new monsite`.
La commande par défaut de cette image doit être `jekyll serve` qui construit les fichiers html à partir des markdowns et démarre le serveur web inclus dans Jekyll. Le port 4000 sera exposé sur le port 80 de la machine hôte.

### Un serveur web avec juste le site

Dans cette configuration, notre image inclut les dépendances de construction : jekyll. Nous allons utiliser le concept des *multi-stage builds* pour créer une image contenant uniquement un serveur web et les fichiers HTML, JS et CSS de notre site web sans Jekyll et ses dépendances. Cette fois-ci on utilisera la commande `jekyll build` pour uniquement construire le site web. On copiera les fichiers générés dans l'image du serveur web. Le serveur web à utiliser est l'image `httpd:alpine`
