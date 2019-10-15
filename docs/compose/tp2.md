# TP2 : Multi-composants

- Transcrivez [le TP1](/engine/lamp/) dans un fichier docker-compose.yml.
- Testez la commande `docker-compose scale` pour déployer une seconde instance de apache, que se passe-t-il ?


## Récréation : le load-balancing en pratique

[Voir ici...](/recreation/load-balancing/)

## Le loadbalancing en pratique

Modifiez votre docker-compose.yml pour permettre le scalling de apache.

**Ici nous scalons uniquement apache. Le scaling d'une base de données est plus complexes car il faut que la base de données ait des concepts de clustering applicatif pour le partage des données.**