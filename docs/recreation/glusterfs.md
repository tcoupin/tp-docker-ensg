
> *GlusterFS est un système de fichiers libre distribué en parallèle, qui permet de stocker jusqu’à plusieurs pétaoctets. C’est un système de fichiers de grappe de serveurs. Il est livré en deux parties : un serveur et un client.* <br>
> <p align="right">*Wikipédia*</p>

# On fait quoi ?

Un [*Vagrantfile*](https://github.com/tcoupin/tp-docker-ensg/tree/master/docs/recreation/glusterfs/) est disponible sur ce dépôt. Il permet de démarrer 4 machines virtuelles offrant chacune 9 Gio de stockage.


Elles forment un cluster GlusterFS et offrent un volume nommé *myvolume* à replica 2.

# Comment ?

* Création des VMs : 
```
vagrant up
```
* Monter le volume sur la machine hôte : 
```
mkdir mymountpoint
sudo mount 192.168.242.10:/myvolume ./mymountpoint
```
* Observer la taille du volume :
```
df -h ./mymountpoint
```
* Surveiller la répartition des données sur chacunes des VMs (commande à exécuter dans 4 terminaux):
```
vagrant ssh node[0-3] -c "watch ls /localstorage"
```
* Remplir le dossier de montage et observer le comportement sur les VMs :
```
for i in `seq 30`; do touch ./mymountpoint/file$i;done
```

# Plus loin

Modifier le volume gluster en modifiant le nombre de réplicat : 1 et 4...