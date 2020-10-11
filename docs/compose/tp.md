# TP1 : LAMP

Reproduire [le TP LAMP](/engine/tp-lamp/) dans un fichier docker-compose.yml.


# TP2 : Geoserveur (avec construction d'image)

Reproduire le [TP dockerfiles partie Geoserver,](../../engine/tp-dockerfile/) avec docker-compose en utilisant la fonctionnalité de construction d'image.

*Bonus : vous pouvez ajouter un conteneur [postgis](https://hub.docker.com/r/camptocamp/postgres), configurez geoserver pour l'utiliser et utiliser QGIS pour interagir avec postgis (pour la création des données) et avec geoserver (pour l'affichage).*

# TP3 : scaling

Reprendre le TP1 et utiliser la commande `docker-compose scale ...` pour multiplier le nombre de conteneur web. Que se passe-t-il ?

## Récréation : le load-balancing en pratique

[Voir ici...](/recreation/load-balancing/)

## Le loadbalancing en pratique

Modifiez votre docker-compose.yml pour permettre le scalling du conteneur web.

**Ici nous scalons uniquement la partie web. Le scaling d'une base de données est plus complexes car il faut que la base de données ait des concepts de clustering applicatif pour le partage des données.**