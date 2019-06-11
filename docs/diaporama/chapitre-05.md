<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 5
### Dépôts distants


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Travailler avec des dépôts distants

Collaborer au même projet
 - partager son travail
  - `git push` = « pousser » ses modifications
 - récupérer le travail des autres développeurs
  - `git fetch` « récupérer » les modifications des autres

Il peut exister plusieurs dépôts distants
 - droits en lecture seule ou en lecture / écriture
 - exemple de la contribution à un projet libre


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Connexion à un dépôt distant

Automatiquement lors d’un `git clone`
 - après le clonage, le dépôt local est automatiquement relié au dépôt distant
 - alias du dépôt distant : `origin`

Explicitement
 - exemple 1 : suite à `git init`, aucun dépôt distant n’est configuré

```bash
git remote add origin https://git.stable.innovation.insee.eu/wehdrc/formation-git.git
```

 - exemple 2 : si on contribue à un projet libre

```bash
git clone git@github.com:romain/react.git # lecture / écriture (fork)
git remote add upstream https://github.com/facebook/react.git # lecture seule
```

On peut lister les dépôts distants avec leurs adresses :

```bash
$ git remote -v
origin	git@github.com/romain/react.git (fetch)
origin	git@github.com/romain/react.git (push)
upstream	https://github.com/facebook/react.git (fetch)
upstream	https://github.com/facebook/react.git (push)
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Récupérer et tirer depuis un dépôt distant

Mettre à jour sa copie de travail avec les modifications du dépôt distant

`git fetch`
  - équivalent à `git fetch origin`
  	- équivalent à `git fetch origin master`

Les modifications sont récupérées localement dans une branche spéciale
  - `origin/master`
  - la copie de travail n’est pas modifiée

Pour intégrer les modifications distantes dans la copie de travail : `git merge`
  - équivalent à `git merge origin/master`

<!-- .element: class="icon idea" -->`git pull`
 - équivalent à `git fetch origin master` puis `git merge origin/master`


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Inspecter un dépôt distant : `git remote show`

<div class="center">
	<img src="images/remote-show.png" width="700px" />
</div>

<table>
<tr>
	<td></td>
	<td>branche locale</td>
	<td>branche distante</td>
</tr>
<tr>
	<td>_tracked_</td>
	<td>✔</td>
	<td>✔</td>
</tr>
<tr>
	<td>_new_</td>
	<td>✘</td>
	<td>✔</td>
</tr>
<tr>
	<td>_stale_</td>
	<td>✔</td>
	<td>✘</td>
</tr>
</table>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Inspecter un dépôt distant avec Gitlab

Onglets « Branches » : [Gitlab](https://git.stable.innovation.insee.eu/wehdrc/formation-git/branches) | [Github](https://github.com/romain-warnan/formation-git/branches)

<div class="center">
	<img src="images/remote-show-gitlab.png" width="700px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Modifier un dépôt

Renommer :
```bash
git remote rename gh github
```

Supprimer :
```bash
git remote rm github
```

Modifier l’url :
```bash
git remote set-url origin ssh://gforge.insee.fr/.../formation-git.git
```


%%%


<!-- .slide: class="tp" -->
## [TP2](https://git.stable.innovation.insee.eu/wehdrc/formation-git#2-dépôts-distants)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>
