<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 9
### Branches distantes


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Généralités

Branche de suivi : référence locale vers l’état d’une branche du dépôt distant

Non modifiable par l’utilisateur
 - uniquement par la communication avec le dépôt distant

Nommée `repository_name/branch_name`
 - `origin/master`
 - `origin/dev`
 - `github/master`
 - ...

<!-- .element: class="icon info" -->Le dépôt distant `origin` n’est pas particulier
 - c’est seulement le nom donné par défaut au dépôt que l’on a cloné


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Création d’une branche de suivi

Automatiquement, après un clone, la branche `master` suit `origin/master`

Suivre une autre branche distante existante :

```bash
git checkout --track origin/branch_name
```

 - équivalent à `git checkout -b branch_name origin/branch_name`
 - ou même plus simplement : `git checkout branch_name`
  - il existe une branche `branch_name` dans le dépôt `origin`
  - il n’existe pas de branche locale `branch_name`

Créer une branche locale et la pousser vers le dépôt distant :
```bash
git checkout -b branch_name
git push -u origin branch_name
```

<!-- .element: class="icon info" -->Par la suite on utilise simplement `git push`

%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Gestion des branches de suivi

Lister les branches et leurs éventuelles « branches amont » (*upstream*) :
```bash
git branch -vv
```
<div class="center">
    <img src="images/branch-vv.png" class="boxed-img" width="800px" />
</div>

Une fois le suivi activé, `fetch` et `push` fonctionnent sans précision supplémentaire
 - rappel : `fetch` met jour `remote/branch_name`
 - il faut ensuite fusionner dans la branche locale : `git merge`

<!-- .element: class="icon idea" -->En utilisant `pull`, on réalise les deux opérations d’un coup


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" -->
### Divergence des historiques

<table>
<tr>
<td>
<img src="images/remote-branches-2.png" />
</td>
<td>
<img src="images/remote-branches-3.png" />
</td>
</tr>
</table>

<!-- .element: class="icon warn" -->Source potentielle de conflits

<!-- .element: class="icon info" -->Source de *commits* de fusion

%%%


<!-- .slide: class="tp" -->
## [TP4](https://git.stable.innovation.insee.eu/wehdrc/formation-git#4-branches)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>