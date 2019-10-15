# Le projet

**Projet 2018-2019, non mis à jour!!** 

## Objectifs

- Mise en place d'un cluster swarm à architecture mixte (ARM + x86_64)
- Déploiement d'une application web de calcul d'itinéraire
- Monitoring des RaspberryPi

## Contraintes

- haute disponibilité de l'application déployée
- répartition sur l'ensemble des Rpi
- scalabilité

## Planning

- Architecture logicielle et matérielle
- Mise en place du cluster
- Déploiement application
- Benchmark
- Test de la HA, test de mise à jour et rollback
- Présentation

## Jalons

- T+0.5j : architecture
- T+1.5j : cluster fonctionnel
- T+3j : application déployée, scalable et disponible
- T+3.7j : présentation de 20-30 min du projet, des décisions prises, des tests réalisés

## Rendu

Un début d'infra qui tourne.

Un dépôt Github :

- votre architecture matérielle, et l'argumentaire qui va avec pour justifier l'ensemble des contraintes
- organisation humaine
- plan de sauvegarde, procédure en cas de panne matérielle...
- script et config pour un redéploiement
- les tests et résultats obtenus
- la présentation finale

...

La contribution de chacun doit pouvoir être évaluée au travers des commit du dépôt.


## Outils

- Benchmark et simulation de trafic : Jmeter
- monitoring : suite influxdb, telegraf, grafana. Traefik branché sur influxdb
- test : bats ?
