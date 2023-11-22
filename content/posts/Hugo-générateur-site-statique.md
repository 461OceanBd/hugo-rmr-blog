---
title: 'La création de ce site avec Hugo, générateur de site statique'
date: 2023-09-25T18:38:45+02:00
draft: false
---

Quoi de plus méta dans ce premier article du blog que de parler de la création du blog lui même. Il présente pour moi deux objectifs :

1. Avoir une présence en ligne
2. Pouvoir consigner, ma veille, mon travail ou mes notes

Je voulais pouvoir mettre ça rapidemment en place. Je cherchais une solution statique, sans base de données, facile à héberger. Inutile de sortir un Wordpress overkill pour ça. Je souhaitais pouvoir générer facilement mes posts de blog via des fichiers Markdown.

J'ai choisi d'utiliser **Hugo** un générateur de sites statiques écrit en Go (ou Golang), un langage de programmation compilé reconnu pour sa rapidité. En effet, Hugo est capable de créer la plupart des sites web en quelques secondes, avec un temps de traitement inférieur à 1 milliseconde par page. Cette performance exceptionnelle fait de Hugo le "framework le plus rapide du monde pour la création de sites web".

Il propose des thèmes facilement adaptables. Il est gratuit et open-source.

Le résultat n'est pas parfait, notamment en ce qui concerne la mise en forme automatiques des articles écrits en markdown. Il faudra que je prenne un peu de temps pour voir ce que je peux faire pour améliorer cela. 



Après l'installation du langage voici un résumé des étapes à suivre :

- créer et cloner un empty project github
- creer un nouveau projet hugo dans ce dossier :

```
hugo new site <project-name> -f --format yml
```
"-f" sert a forcer l'écriture dans un dossier non vide, "--format yml" permet d'utilser un fichier de configuration en .yml plutôt que en .toml

- aller dans le projet : 
```bash
cd <project-name>
```

- Ajouter un thème au projet en tant que sous-module git (voir doc du thème) :
```
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```
```
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

- update le theme :
```
git submodule update --remote --merge
```

- Ajouter le theme au fichier de config hugo.yml :
```
theme: "PaperMod"
```

- le theme est ajouté dans le dossier 'themes' puis activé via le fichier de configuration

- la commande suivante permet de lancer le server :
```
hugo server
```
- Aller voir sur 'localhost:1313/' depuis un navigateur. Le server de code recharge à chaud les modifs.


Architecture du projet :
- content : dossier avec le contenu du blog comme les articles, pages et arborescence
- layouts : le dossier contenant les partie override du theme installé
- static : pour les assets statiques comme les images.
- theme : dossier contenant les thèmes

- Ajouter un article : 
```
hugo new posts/<nom-article.md>
```
Le fichier est ajouté dans le dossier "content" (possibilité de le faire à la main)

- Pour connaitre toutes les possibilités de custom des themes il faut se reporter à la documentation du thème choisi

- Possibilité d'overrider les fichiers .html, .css en respectant leur emplacement et nommage dans l'architecture du projet. Copier les fichiers depuis le thème pour les placer dans le projet.

Pour build le projet :
```
hugo
```

Cette commande permet la génération du site web statique à partir de fichiers Markdown et des modèles. Elle compile le contenu, crée des pages HTML, et copie les ressources statiques. Le site généré est prêt à être déployé en ligne !