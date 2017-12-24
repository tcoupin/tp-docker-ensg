## Installation

La procédure est fournie dans la documentation : [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/).

Pour résumer :

```
export HTTP_PROXY=http://10.0.4.2:3128 # Proxy ENSG
sudo -E curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```


Pour vérifier l'installation :
```
docker-compose --version
```