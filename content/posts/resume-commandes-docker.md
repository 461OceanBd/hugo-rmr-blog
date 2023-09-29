---
title: 'Résumé / Aide méoire des commandes courantes docker'
date: 2023-09-29T12:03:00+02:00
draft: false
---


# Aide mémoire/Résumé des commandes docker

# Approche conceptuelle rapide de Docker

Docker est une plateforme de virtualisation légère qui permet d'emballer des applications et leurs dépendances dans des conteneurs, offrant une isolation efficace et une portabilité entre les environnements.

La principale différence entre une machine virtuelle (VM) et un conteneur réside dans le niveau d'isolation : les VM virtualisent un système d'exploitation complet, tandis que les conteneurs partagent le même noyau de système d'exploitation, ce qui les rend plus légers et plus rapides. On parle de **virtualisation lourde** pour une VM et une **virtualisation légère** pour un conteneur.

Les principaux concepts de Docker sont les suivants :
- **Image** : Un modèle de système de fichiers léger et autonome qui contient tout ce dont une application a besoin pour s'exécuter, y compris le code, les dépendances et la configuration.
- **Conteneur** : Une instance exécutable d'une image Docker, qui fonctionne de manière isolée par rapport au système hôte et à d'autres conteneurs, tout en partageant le même noyau du système d'exploitation.
- **Volume** : Un mécanisme permettant de stocker des données en dehors du système de fichiers du conteneur, garantissant que les données persistent même lorsque le conteneur est arrêté ou supprimé.
- **Réseau Docker** : Les réseaux Docker permettent aux conteneurs de communiquer entre eux et avec le monde extérieur. Vous pouvez créer des réseaux personnalisés pour isoler des groupes de conteneurs ou utiliser le réseau par défaut.


# Commandes Docker courantes

Pour gérer des conteneurs Docker, vous pouvez utiliser la ligne de commande Docker. Voici quelques commandes courantes pour gérer des images et des conteneurs et obtenir des informations sur les conteneurs en cours d'exécution :

## Voir les images disponibles en local :

```
docker images
```

## aller chercher une image sur le Docker Hub

```
docker pull <nom de l'image>
```

## Pour des build images en locales (images custom) :

```
docker build -t <nom_image> .
```

Cette commande s'execute à la racine de l'image, là où se trouve le dockerfile car le "." est le chemin vers le dockerfile utilisé (possibilité de mettre le path souhaité). Cela va build l'image. Le -t permet de choisir le nom de l'image 


The -t flag tags your image with a name. (welcome-to-docker in this case). And the . lets Docker know where it can find the Dockerfile.


### Démarrer un conteneur :

```
docker run <options> <image>
```

Cette commande démarre un conteneur à partir d'une image Docker spécifiée. Si l'image n'existe pas il va la chercher sur le docker hub automatiquement

### Exemple de docker run avec options

```
docker run -d -p 8600:8080 pengbai/docker-supermario
```

Cette commande execute le conteneur docker à partir de l'image (pengbai/docker-supermario) :
- -d : signifie "détaché". Lorsqu'il est utilisé, le conteneur sera exécuté en arrière-plan, sans verrouiller le terminalpar le conteneur.
- -p 8600:8080 : Cela spécifie le mappage de port entre l'hôte (machine locale) et le conteneur. Le format est -p <port_de_l'hôte>:<port_du_conteneur>. Dans ce cas, le port 8600 de la machine locale est mappé sur le port 8080 du conteneur. Cela signifie qu'en accédant à http://localhost:8600 dans un navigateur, cela sera redirigé vers le port 8080 du conteneur.

### Lister les conteneurs en cours d'exécution :

```
docker ps
```

Cette commande affiche une liste des conteneurs actuellement en cours d'exécution.

### Lister tous les conteneurs (y compris ceux arrêtés) :

```
docker ps -a
```

Cette commande affiche une liste de tous les conteneurs, qu'ils soient en cours d'exécution ou arrêtés.

### Arrêter un conteneur :

```
docker stop <container_id ou nom>
```

Cette commande arrête un conteneur en cours d'exécution. Vous pouvez spécifier soit l'ID du conteneur, soit son nom.

### Redémarrer un conteneur :

```
docker restart <container_id ou nom>
```

Cette commande redémarre un conteneur qui a été arrêté.

### Supprimer un conteneur arrêté :

```
docker rm <container_id ou nom>
```

Cette commande supprime un conteneur arrêté. Assurez-vous qu'il est arrêté avant de le supprimer.

### Afficher les journaux d'un conteneur :

```
docker logs <container_id ou nom>
```

Cette commande affiche les journaux de sortie d'un conteneur en cours d'exécution.

### Afficher des informations détaillées sur un conteneur :

```
docker inspect <container_id ou nom>
```

Cette commande fournit des informations détaillées sur un conteneur, y compris sa configuration, son réseau, ses volumes, etc.

### Exécuter une commande dans un conteneur en cours d'exécution :

```
docker exec -it <container_id ou nom> <commande>
```

Cette commande vous permet d'exécuter une commande à l'intérieur d'un conteneur en cours d'exécution. L'option -it permet d'ouvrir un terminal interactif dans le conteneur.

### Arrêter tous les conteneurs en cours d'exécution :

```
docker stop $(docker ps -q)
```

Cette commande arrête tous les conteneurs en cours d'exécution.


## Nettoyer son système :

```
docker image prune -a
```
Cette commande supprime toutes les images non utilisées (attention à ne pas en abuser)

```
docker system prune
```
Supprime les conteneurs stoppés, les réseaux non utilisés, les images et le build cache (idem ++)

