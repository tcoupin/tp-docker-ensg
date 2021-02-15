# Le projet

## Sujet

**Vous devez déployer un système de tchat qui sera le support principal de la continuité d'activité de votre établissement pendant le confinement.**

A votre disposition :
- plusieurs datacenters
- plusieurs serveurs
- le personnel de votre DSI

## Contraintes

- Vous avez une semaine !
- Mise en place d'un cluster swarm à architecture mixte (ARM + x86_64)
    - Clustering réseau et stockage
    - Monitoring
- Déploiement d'une application de tchat
    - Configuration
    - Tests
- haute disponibilité de l'application déployée
- répartition sur l'ensemble des noeuds
- scalabilité
  
Les notions suivantes seront aussi à utiliser :

- gestion de projet
- communication


## Planning

- Architecture logicielle et matérielle
- Mise en place du cluster
- Déploiement application
- Test de la HA, test de mise à jour et rollback
- Présentation

## Jalons

- T+2j : architecture & cluster fonctionnel
- T+3,5j : application déployée, scalable et disponible
- T+4,5j : présentation de 20-30 min du projet, des décisions prises, des tests réalisés

## Rendu

Un compte rendu contenant :

- votre architecture matérielle, et l'argumentaire qui va avec pour justifier l'ensemble des contraintes
- organisation humaine
- plan de sauvegarde, procédure en cas de panne matérielle...
- script et config pour un redéploiement
- les tests et résultats obtenus
- la présentation finale

...



## Outils

- Benchmark et simulation de trafic : Jmeter
- monitoring : suite influxdb, telegraf, grafana. Traefik branché sur influxdb
- test : bats ?
