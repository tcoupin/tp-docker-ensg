
*Nous allons prendre en main Docker : ses concepts et son interface CLI.*

## Hello-world

### Testons votre installation

```shell
docker run hello-world
```

La commande par défaut de cette image affiche un message confirmant la bonne installation de *Docker Engine*.
Si l'image n'est pas disponible en local, elle sera téléchargée sans avoir à faire un `docker pull hello-world`

### Gérer les conteneurs

- Observez que le conteneur est bien existant et à l'arrêt

```shell
docker ps
docker ps -a
```

- Supprimez le

```shell
docker container rm NAME
```

- Le conteneur n'existe plus, et l'image ?


### Les images

- Affichez la liste des images, supprimez l'image `hello-world`

```shell
docker image rm hello-world
```

- Téléchargez l'image debian 9 (pour trouver la bonne image et le bon tag, rendez-vous sur hub.docker.com)

```shell
docker image pull IMAGE[:TAG]
```

- Affichez les métadonnées de l'image téléchargée

```shell
docker image inspect IMAGE[:TAG]
```

## Container

- Démarrez un bash interactif de l'image debian, observez le nom d'hôte apparent dans le conteneur

```shell
docker container run -i -t IMAGE[:TAG] bash
```

- dans un autre terminal, observer les listes des conteneurs en fonctionnement

- Stopper le conteneur, le redémarrer et se rattacher au bash. A chaque étape, observez la liste des conteneurs et leur état

```shell
docker container stop NAME
docker container start NAME
docker attach NAME
```

- Se détacher du bash en utilisant les touches `Ctrl+P+Q`

- Cherchez dans l'aide des informations sur les options `-d`, `-w`, `-h`, `--rm` et `--name`

```shell
docker container run --help
```

- Testez ces options

## Volumes

- Démarrez un bash interactif de l'image debian, en montant la racine de la machine hôte sur `/host` en mode lecture seule dans le container

```shell
docker container run -i -t  -v /:/host:ro IMAGE:TAG bash
```

- Démarrez un bash interactif avec un volume docker sur `/data`, créer un fichier avec la commande `touch /data/toto`

```shell
docker container run -i -t  -v monsupervolume:/data IMAGE:TAG bash
$ touch /data/toto
```

- Affichez la liste des volumes

```shell
docker volume ls
```

- Détruisez et relancez le même conteneur, observez le contenu de `/data`
- Démarrez un second conteneur identique et afficher le contenu de `/data`.
- Cherchez dans l'aide des informations sur l'option' `-v` et testez là

```shell
docker container rm --help
```

## Réseau

### Mode réseau
- Affichez la liste des interfaces de votre machine hôte puis d'un conteneur avec la commande `ip a`
- Dans un conteneur avec l'option `--net host`, afficher les interfaces réseaux

### Exposition de ports

- Démarrez un conteneur basé sur l'image [https://hub.docker.com/r/containous/whoami/](https://hub.docker.com/r/containous/whoami/)
- Trouvez l'IP du conteneur sur le réseau `bridge` en inspectant le conteneur

```shell
docker container inspect NAME
```

Dans un navigateur, consultez l'IP du conteneur `http://IP`.

- Relancer un conteneur déclarant l'exposition du port 80 (option `-p 80`), utilisez la commande `docker container port` pour connaître le port d'exposition.

Dans un navigateur, consulter l'IP de *loopback* sur le port trouvé `http://127.0.0.1:PORT`.
Tentez d'accéder au serveur du voisin.

- Cette fois-ci, utilisez l'option `-p` pour exposer le port 80 du conteneur sur le port 8080 de la machine hôte.

```shell
docker container run -p 8080:80 ...
```

Dans un navigateur, consulter l'IP de *loopback* sur le port 8080 `http://127.0.0.1:8080`.
Tentez d'accéder au serveur du voisin.