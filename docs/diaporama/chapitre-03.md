<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 3
### Configuration et personnalisation


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Le système de configuration

Système de surcharge à trois niveaux
 - quatre en comptant `git -c section.key=value`

`--system` : pour tous les utilisateurs
 - `/c/ProgramData/Git/config`

```ini
core.symlinks=false
core.autocrlf=true
```

`--global` : pour tous les dépôts de l’utilisateur
 - `~/.gitconfig`

```ini
user.name=Prénom Nom
user.email=prenom.nom@insee.fr
```

`--local` : uniquement pour un dépot
 - `./.git/config`

```ini
remote.origin.url=ssh://git@git.stable.innovation.insee.eu:22222/wehdrc/formation-git.git
branch.master.remote=origin
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Configuration de base

<!-- .element: class="icon warn" -->Configuration obligatoire pour valider :
```bash
git config --global user.name "Prénom Nom"
git config --global user.email "prenom.nom@insee.fr"
```

<!-- .element: class="icon idea" -->Configuration bien utile :
```bash
# Éditeur de texte pour les messages de commit, etc.
git config --global core.editor vim

# Pour utiliser nano
git config --global core.editor nano

# Paraméter le proxy de l’Insee
git config --global http.proxy http://proxy-rie.http.insee.fr:8080

# Alias pour commit : git co
git config --global alias.co commit

# Alias composé de plusieurs commandes : utiliser « ! »
git config alias.pp '!git push origin ; git push github'
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Consulter la configuration
Résultat dans les fichiers de configuration, par exemple `~/.gitconfig` :

```ini
[user]
	name = Romain Warnan
	email = romain.warnan@insee.fr
[merge]
	conflictstyle = diff3
[core]
	editor = vim
[http]
	proxy = http://proxy-rie.http.insee.fr:8080
[alias]
	co = commit
```

Afficher la valeur d’une propriété :
```bash
git config user.name
```

<!-- .element: class="icon info" -->Lister toute la configuration avec le nom du fichier :
```bash
git config --list --show-origin
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Accéder à la documentation

Documentation complète dans le terminal :
```bash
git help <verb>
```

Autant aller voir sur internet en français :
 - <!-- .element: class="after link" -->[Git Book (fr)](https://git-scm.com/book/fr/v2)

Ou en anglais :
 - <!-- .element: class="after link" -->[Git Book (en)](https://git-scm.com/book/en/v2)

<!-- .element: class="icon info" -->Pour un aide-mémoire rapide :
```bash
git <verb> -h
```