Nous allons utiliser Docker dans un environnement Linux avec la distribution Ubuntu. 

> Le projet [PWD](http://play-with-docker.com) permet également de tester Docker sans l'installer au travers d'une interface web. Les sessions de travail durent 4h et la vitesse de l'interface dépend souvent de l'activité des autres utilisateurs...

## Variante

Docker Engine est disponible en 2 variantes :

- CE : *community edition* qui est la version gratuite que nous allons utiliser ;
- EE : *entreprise edition* qui est plus évoluée avec des fonctionnalités supplémentaires et une certification de fonctionnement sur certain matériel.

## Version

Depuis mars 2017, la nomenclature des versions suit la forme des versions de Ubuntu à savoir *AA.MM* avec AA l'année et MM le mois (ex. : 17.04 pour la version d'avril 2017).

- une version *stable* est compilée tous les trimestre (ex : 17.03, 17.06, 17.09, 17.12...) ;
- une version *edge* est compilée tous les mois et contient les nouvelles fonctionnalitées.

## Installation

La procédure est fournie dans la documentation : [https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#docker-ee-customers](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#docker-ee-customers).

Pour résumer :

```bash
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo usermod -a -G docker $USER
```

Pour que la dernière commande soit prise en compte, il faut fermer la session et la rouvrir.

A l'ENSG, l'accès à internet nécessite l'utilisation du proxy. Il faut configurer docker pour l'utiliser. 

1. Localiser le fichier de service avec `sudo systemctl status docker` : `/lib/systemd/system/docker.service`

2. Dans la section `[service]`, ajouter :

    ```
    Environment="HTTP_PROXY=http://10.0.4.2:3128/"
    Environment="HTTPS_PROXY=http://10.0.4.2:3128/"
    ```

3. On en profitera pour ajouter la configuration pour le registry docker de l'ENSG, dans l'ExecStart ajouter : `--insecure-registry dockerforge.ensg.eu:5000`

4. Enfin, redémarrer le daemon docker : `sudo systemctl restart docker`


Pour vérifier l'installation :
```
docker run hello-world
```