<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 6
### Historique des validations


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Lister l’historique des validations : `git log`

Lister les validations réalisées dans l’ordre antichronologique :
 - `git log`

<div class="center">
	<img src="images/log.png" width="800px" />
</div>

<!-- .element: class="icon idea" -->L’historique est affiché avec `less`
 - Utiliser les flèches « &uarr; » et « &darr; » pour naviguer dans l’historique
 - Taper « q » pour quitter


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Afficher plus d’informations dans l’historique

*Patch* de chaque *commit* :
 - `git log --patch` ou `git log -p`
 - permet de connaître toutes les modifications apportées par un *commit*
 - assez verbeux

Liste des fichiers modifiés par chaque *commit* :
 - `git log --name-only`
<div class="center">
	<img src="images/log-name-only.png" width="800px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Affichage compact de l’historique

`git log --oneline`
 - une ligne par *commit*
 - *hash* abrégé sur 7 caractères
 - équivalent à `git log --pretty=oneline --abbrev-commit`

<div class="center">
	<img src="images/log-oneline.png" width="800px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Visualisation des branches dans l’historique
`git log --graph [--oneline]`

<div class="center">
	<img src="images/log-graph.png" width="800px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Personnaliser l’affichage de l’historique

`git log --pretty=format:"%h - %an, %ar : %s"`
 - <!-- .element: class="after link" -->[liste des options usuelles](https://git-scm.com/book/fr/v2/Les-bases-de-Git-Visualiser-l%E2%80%99historique-des-validations#pretty_format)
 - <!-- .element: class="after link" -->[liste complète des options](https://git-scm.com/docs/pretty-formats)
 - <!-- .element: class="after link" -->[liste des couleurs](https://stackoverflow.com/questions/15458237/git-pretty-format-colors/15458378#15458378)

Exemple :
```
log --color --graph --abbrev-commit --pretty=format:'%C(bold magenta)%h%Creset -%C(yellow)%d%Creset %s %C(green)(%cr) %C(cyan)<%an>%Creset'
```

<div class="center">
	<img src="images/log-pretty.png" width="900px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Filtrer l’historique sur les métadonnées

Le nombre : `-(n)`
```bash
git log -5 # Les cinq derniers
```

La date : `--since` et `--until`
```bash
git log --since="2018-04-21" # Depuis le 21 avril 2018
git log --since=1.month # Depuis moins d’un mois
git log --until=2.days # Depuis plus de 2 jours
```

L’auteur : `--author`
 - le nom de l’auteur ou son *email* contient la chaîne de caractères spécifiée

```bash
git log --author="Jean-Pierre"
```

Le message : `--grep`
 - le message de *commit* contient la chaîne de caractères spécifiée

```bash
git log --grep="refacto"
git log --grep="correc" --grep="ortho" --all-match
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Filtrer l’historique sur les modifications

Dans ces deux cas, Git filtre sur le *patch* :

Exactement : `-S"string"`
 - les ajouts ou retraits contiennent la chaîne de caractères spécifiée

```bash
git log -S"public static void main"
```

Avec une expression régulière : `-G"pattern"`
 - les ajouts ou retraits correspondent au motif de l’expression régulière spécifiée

```bash
git log -G"public Cocktail .*\("
```

<!-- .element: class="icon idea" -->Il est souvent judicieux de combiner ces options avec l’option `--patch`

%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Restreindre l’historique à certains fichiers

```bash
git log -- src/main/java/fr/insee/bar/dao/CocktailDao.java
git log -- src/main/java/fr/insee/bar/dao/
git log --oneline --name-only -- src/main/java/fr/insee/bar/controller
```
 - seuls les *commits* qui contiennent des modifications de ces fichiers sont listés


%%%


<!-- .slide: class="tp" -->
## [TP3](https://git.stable.innovation.insee.eu/wehdrc/formation-git#3-historique)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>