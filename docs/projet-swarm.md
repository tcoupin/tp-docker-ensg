# Le projet

## Objectifs

- Mise en place d'un cluster swarm à architecture mixte (ARM + x86_64)
  - Clustering réseau et stockage
  - Monitoring
- Déploiement d'une application web de stockage "cloud" avec édition collaborative et/ou calcul d'itinéraire en ligne
  - Configuration
  - Tests
  
Les notions suivantes seront aussi à utiliser :

- gestion de projet
- communication


## Contraintes

- haute disponibilité de l'application déployée
- répartition sur l'ensemble des noeuds
- scalabilité

## Planning

- Architecture logicielle et matérielle
- Mise en place du cluster
- Déploiement application
- Test de la HA, test de mise à jour et rollback
- Présentation

## Jalons

- T+1j : architecture
- T+2j : cluster fonctionnel
- T+3,5j : application déployée, scalable et disponible
- T+4j : présentation de 20-30 min du projet, des décisions prises, des tests réalisés
- T+4,5j : RetEx

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
