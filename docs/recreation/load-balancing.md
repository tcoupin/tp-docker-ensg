## Pourquoi ?

Vous venez de voir qu'un simple *scalling* d'une service n'est pas possible si le containeur expose directement sur un port de la machine hôte : on obtient l'erreur "address already in use".

Il faut utiliser un répartiteur de charge, *load-balancer*, qui réceptionnera les requêtes sur le port de la machine hôte et les transférera aux containers capable de répondre, selon les règles établies dans la configuration.

Il existe des loadbalancer différents qui travaillent sur différentes couches du [modèle OSI](https://fr.wikipedia.org/wiki/Modèle_OSI). En web, on travaille généralement au niveau du protocole HTTP (couches 5 à 7).

Parmi les LB disponibles, on peut citer :

- HAProxy : capable de travailler également sur la couche 3 (réseau), très puissant
- Nginx : ce serveur web est également un très bon LB
- Traefik : assez récent et configuration principalement dynamique, il a été pensé pour faciliter le déploiement et le scalling d'application dans des gestionnaires d'application conteneurisées tels que Docker (swarm ou non), Kubernetes, Amazon ECS...

## Un exemple

Le dépôt [tcoupin/slow-whoami](https://github.com/tcoupin/slow-whoami) permet de déployer une application simpliste dont le but est de répondre de plus en plus lentement au fur et à mesure de la montée en charge.

* Cloner le dépôt
* Déployer l'application avec la commande `docker-compose -f docker-compose.lb.yml up  -d`
* Utiliser un utilitaire de benchmark pour simuler la charge (par exemple `siege http://127.0.0.1/ping`)
* Ajouter des instances de l'application pour voir si le temps de réponse évolue `docker-compose -f docker-compose.lb.yml scale app=2`

Liens utiles :

- [Graphique des temps de réponse](http://127.0.0.1/)
- [Affichage du nom du conteneur (et augmentation du temps de réponse)](http://127.0.0.1/ping)
- [Statistiques d'un conteneur au hasard](http://127.0.0.1/localstats)
- [Statistiques de l'ensemble des conteneurs](http://127.0.0.1/stats)
