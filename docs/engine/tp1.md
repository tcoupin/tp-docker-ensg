
## Un dockerfile pour Geoserver

Ecrire un dockerfile pour créer une image de Geoserver 2.12, basée sur l'image `tomcat`.
Documentation utile : [http://docs.geoserver.org/2.12.1/user/installation/war.html#installation-war](http://docs.geoserver.org/2.12.1/user/installation/war.html#installation-war).

***Le Dockerfile est à rendre pour la [notation](/notation).***

Dans le mail où vous me ferez parvenir le Dockerfile, indiquer également la commande utilisée pour la construction de l'image et celle pour démarrer Geoserver. N'hésitez pas à ajouter toute information que vous jugerez utile.



## Multi-stage build

*Jekyll* permet de créer un site web statique à partir de fichier texte écrits en markdown. Il est écrit en ruby.

Ressources utiles :

- [Commandes utiles de Jekyll](https://jekyllrb.com/docs/usage/)
- [Thème *minima* pour Jekyll](https://github.com/jekyll/minima)


### Prise en main de Jekyll

Ecrire un Dockerfile se basant sur l'image officielle de Jekyll, qui construit et sert le thème *minima*. On utilisera la commande `jekyll serve` pour démarrer le serveur web inclus dans Jekyll. Le port 4000 sera exposé sur le port 80 de la machine hôte.

### Un serveur web avec juste le site

Dans cette configuration, notre image inclut les dépendances de construction : jekyll. Nous allons utiliser le concept des *multi-stage builds* pour créer une image contenant uniquement un serveur web et les fichiers HTML, JS et CSS de notre site web sans Jekyll et ses dépendances. Cette fois-ci on utilisera la commande `jekyll build` pour uniquement construire le site web. On copiera les fichiers générés dans l'image du serveur web. Le serveur web à utiliser est l'image `httpd:alpine`




