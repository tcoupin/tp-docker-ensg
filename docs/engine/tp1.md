
## Un dockerfile pour Geoserver

Dans ce TP, nous allons créer une image geoserver. Voici la documentation d'installation [https://docs.geoserver.org/latest/en/user/installation/war.html](https://docs.geoserver.org/latest/en/user/installation/war.html).

Voici également quelques instruction pour l'écriture du Dockerfile :

- partir de l'image `tomcat`
- la commande `ADD` permet d'ajouter des fichiers depuis internet vers l'image
- indiquer un nom de contact avec la commande `MAINTAINER`
- déclarer les volumes où sont stockées les données

```
FROM tomcat:8
ARG GEOSERVER_VERSION=2.16.0
MAINTAINER Thibault Coupin <thibault.coupin@gmail.com>
EXPOSE 8080

ADD https://freefr.dl.sourceforge.net/project/geoserver/GeoServer/${GEOSERVER_VERSION}/geoserver-${GEOSERVER_VERSION}-war.zip /tmp

RUN mkdir /tmp/geoserver \
    && unzip /tmp/geoserver-${GEOSERVER_VERSION}-war.zip -d /tmp/geoserver \
    && mv /tmp/geoserver/geoserver.war /usr/local/tomcat/webapps \
    && rm -rf /tmp/geoserver*
```

Explications :

- Avec l'instruction `FROM`, on précise bien le tag `8` car la doc indique que geoserver ne supporte pas la version 9 de java
- On paramétrise notre Dockerfile, ainsi on pourra changer la version de geoserver au moment de construire l'image. La version par défaut est la 2.16.0

```
# Contruction de l'image sans préciser de numéro de version
docker image build --tag geoserver .
# Contruction de l'image avec numéro de version
docker image build --tag geoserver:2.15.0 --build-arg GEOSERVER_VERSION=2.15.0 .
# Lancement d'un conteneur
docker container run -p 8080:8080 geoserver:2.15.0
```

**La création d'un volume n'est pas faite ici...**


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
