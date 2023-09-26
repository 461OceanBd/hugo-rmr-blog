# hugo-rmr-blog
This is my Hugo GO blog

## tutorial

- créer et cloner un projet github
- creer un nouveau projet hugo dans ce dossier :

```bash
hugo new site <project-name> -f --format yml
```
"-f" sert a forcer l'écriture dans un dossier non vide, "--format yml" permet d'utilser un fichier de configuration en .yml plutôt que en .toml

- aller dans le projet : 
```bash
cd <project-name>
```

- Ajouter un thème au projet en tant que sous-module git (voir doc du thème) :
     ```BASH
     git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
    git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
    ```

- update le theme :
     ```BASH
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
```BASH
hugo new posts/<nom-article.md>
```
Le fichier est ajouté dans le dossier "content" (possibilité de le faire à la main)

- Pour connaitre toutes les possibilités de custom des themes il faut se reporter à la documentation du thème choisi

- Possibilité d'overrider les fichiers .html, .css en respectant leur emplacement et nommage dans l'architecture du projet. Copier les fichiers depuis le thème pour les placer dans le projet.