*Le but de ce TP est de mettre en place les éléments nécessaires d'un serveur web de type LAMP.*

> LAMP :
>
> - **L**inux
> - **A**pache
> - **M**ySql
> - **P**HP

## Apache

L'image à utiliser ici est `httpd` :

1. Lancez un conteneur exposant le port `80` du conteneur sur le port `8080` de la machine. Qu'affiche la page `http://127.0.0.1:8080` ?
2. Cette image utilise le contenu du dossier `/usr/local/apache2/htdocs/` pour répondre aux requêtes. Relancez un nouveau conteneur en utilisant un volume hôte (un dossier de la machine).
3. Dans ce dossier placez le fichier index.html et observez le résultat :
        
        <body style="background-color: yellow;">
        <h1 style="font-family: sans;padding-top: 20vh;text-align: center;font-size: 5em;">
        Salut
        </h1>
        </body>

## Un peu de php

1. Remplacez le fichier html par `index.php`

        <body style="background-color: green;">
        <h1 style="font-family: sans;padding-top: 20vh;text-align: center;font-size: 5em;">
        <?php
        echo "Salut, voici l'heure : " . date("H:i:s");
        ?>
        </h1>
        </body>

2. ça ne fonctionne pas... Pourquoi ?
3. Utilisez plutôt l'image `lavoweb/php-7.1`. Ca ne fonctionne toujours pas... utilisez les logs pour comprendre et corriger (`docker container logs...`).


## Avec une base de données

Notre site web évolue ! il va maintenant afficher une carte. Un clic permet de créer un point, sauvegardé en base de données. Un clic sur un point le supprime. Au chargement de la page, on affiche tous les points de la base de données.

1. Remplacez le contenu du fichier `index.php` par

        <?php
        
        $bdd = new PDO('mysql:host=database;dbname=mymap;charset=utf8', 'user', 's3cr3t');
        $bdd->exec("CREATE TABLE IF NOT EXISTS point (id INT KEY AUTO_INCREMENT, lon FLOAT, lat FLOAT);");
        
        switch ($_GET['action']) {
        	case 'add':
        		if (isset($_GET['lon']) && isset($_GET['lat'])){
        			$bdd->exec(sprintf("INSERT INTO point (lon, lat) values (%F , %F)", $_GET['lon'], $_GET['lat']));
        		}
        		exit;
        	case 'delete':
        		if (isset($_GET['id'])){
        			$bdd->exec(sprintf("DELETE FROM point where id = '%d'", $_GET['id']));
        		}
        		exit;
        	case 'get':
        		$result = $bdd->query("select * from point;");
        		$features = array();
        		while ($donnees = $result->fetch()){
        			$features[] = array(
        				'type' => 'Feature',
        				'properties' => array('id' => intval($donnees['id'])),
        				'geometry' => array(
        					'type' => 'Point',
        					'coordinates' => array(floatval($donnees['lon']), floatval($donnees['lat']))
        				)
        				);
        		}
        		$new_data = array(
        			'type' => "FeatureCollection",
        			'features' => $features,
        		  );
        		header("Content-type: application/json");
        		echo json_encode($new_data, JSON_PRETTY_PRINT);
        		exit;
        }
        ?>
        
        <!DOCTYPE html>
        <html>
        <head>
        	
        	<title>MyMap</title>
        
        	<meta charset="utf-8" />
        	<meta name="viewport" content="width=device-width, initial-scale=1.0">
        	
        	<link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico" />
        
            <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin=""/>
        	<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js" integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og==" crossorigin=""></script>
        	<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        
        	<style>
        		html, body, #mapid {
        			margin: 0;
        			padding: 0;
        			width: 100%;
        			height: 100%;
        		}
        	</style>
        </head>
        <body>
        <div id="mapid"></div>
        <script>
        
        	var mymap = L.map('mapid').setView([46, 0], 6);
        	var datalayer;
        	var needzoom = true;
        
        	L.tileLayer('http://basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
        		maxZoom: 21,
        		attribution: "<?php echo 'Page générée à ' . date("H:i:s");?>"
        	}).addTo(mymap);
        
        	function getData(){
        		if (datalayer){
        			datalayer.remove()
        		}
        		$.get('/?action=get',function(data){
        		datalayer = L.geoJson(data,{
        			onEachFeature: function(feat, layer){
        				layer.on('click',function(e){
        					$.get('/?action=delete&id='+feat.properties.id,()=>getData());
        				})
        			}
        		}).addTo(mymap)
        		if (needzoom){
        			needzoom = false;
        			mymap.fitBounds(datalayer.getBounds())
        		}
        		})
        	}
        
        	mymap.on('click', function(e){
        		$.get('/?action=add&lon='+e.latlng.lng+'&lat='+e.latlng.lat,()=>getData());
        	})
        
        	getData()
        </script>
        </body>
        </html>

2. Pour respecter le principe d'un seul processus par conteneur, il nous faut lancer un second conteneur pour notre base de données. Utilisez l'image `mariadb`. Vous trouverez des informations sur la configuration de cette image sur [hub.docker.com](https://hub.docker.com/_/mariadb). Configurez la base de données de façon à ce que le code php fonctionne (nom d'utilisateur, mot de passe et base de données).

3. Avec la commande `docker exec ...`, lancez le client mysql en ligne de commande pour explorer la base de données et observez le contenu de la table point au fur et à mesure des interactions avec la carte.

>  mysql -u LOGIN -D DATABASE --password="PASSWORD"

## Base de DONNEES

1. Arrêtez et relancez le conteneur mariadb
2. Est-ce que les données qui avaient été saisies sont encore présentes ?
3. Oui
4. Arrêtez, supprimez et recréez le conteneur mariadb
5. Est-ce que les données qui avaient été saisies sont encore présentes ?
6. Non
7. Modifier la commande docker de mariadb pour placer un volume au bon endroit et retentez la suppression et recréation du conteneur mariadb.
