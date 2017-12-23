# TP Docker à l'ENSG

https://docker-ensg.readthedocs.io

### Suports de cours

- [ASI](https://tcoupin.github.io/presentations/2018-asi-ensg)
- [Docker Engine](https://tcoupin.github.io/presentations/docker-intro)
- [Docker-compose](https://tcoupin.github.io/presentations/docker-compose)
- [Docker en mode swarm](https://tcoupin.github.io/presentations/docker-cluster)

### Construction de la doc

```
docker run --rm -it -p 8000:8000 -v `pwd`:/docs squidfunk/mkdocs-material
```