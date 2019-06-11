<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 7
### Branches


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" -->
### Stockage des éléments dans Git

Un _commit_
<div class="center">
	<img src="images/commit-and-tree.png" width="800px" />
</div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" -->
### Stockage des éléments dans Git

La succession des _commits_
<div class="center">
	<img src="images/commits-and-parents.png" width="800px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Notion de branche dans Git

Une branche dans Git est simplement un pointeur léger et déplaçable vers un _commit_

À chaque nouveau _commit_, la branche « avance »
 - elle pointe vers le dernier _commit_

Créer une nouvelle branche :
 - `git branch <branch_name>`
 - on reste dans la branche d’origine

Basculer dans une autre branche = remplacer la copie de travail :
 - `git checkout <branch_name>`
 - on ne peut basculer dans une branche que s’il n’y a pas de risque de perdre de modifications
 - sinon : valider (_commit_) ou remiser (_stash_) avant de changer de branche

<!-- .element: class="icon idea" -->Pour créer une branche et basculer dans cette branche :
 - `git checkout -b <branch_name>`


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="slide-in none-out" -->
### Branche : schéma (1)
```bash
git checkout master
```

<div class="fixed-height"><img src="images/branch-and-history.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/master
cat .git/refs/heads/master # f30ab
cat .git/refs/heads/testing # cat: .git/refs/heads/testing: No such file or directory
```


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Branche : schéma (2)

```bash
git branch testing
```

<div class="fixed-height"><img src="images/head-to-master.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/master
cat .git/refs/heads/master # f30ab
cat .git/refs/heads/testing # f30ab
```


%%%

<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Branche : schéma (3)

```bash
git checkout testing
```

<div class="fixed-height"><img src="images/head-to-testing.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/testing
cat .git/refs/heads/master # f30ab
cat .git/refs/heads/testing # f30ab
```


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Branche : schéma (4)

```bash
git commit -m "Commit dans la branche 'testing'"
```

<div class="fixed-height"><img src="images/advance-testing.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/testing
cat .git/refs/heads/master # f30ab
cat .git/refs/heads/testing # 87ab2
```


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Branche : schéma (5)

```bash
git checkout master
```

<div class="fixed-height"><img src="images/checkout-master.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/master
cat .git/refs/heads/master # f30ab
cat .git/refs/heads/testing # 87ab2
```


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="none-in slide-out" -->
### Branche : schéma (6)

```bash
git commit -m "Commit dans la branche 'master'"
```

<div class="fixed-height"><img src="images/advance-master.png" width="700px" /></div>

```bash
cat .git/HEAD # ref: refs/heads/master
cat .git/refs/heads/master # c2b9e
cat .git/refs/heads/testing # 87ab2
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Gestion des branches

Lister les branches `git branch -v`
<div class="center">
	<img src="images/branch-v.png" />
</div>

Uniquement les branches fusionnées dans `HEAD`
 - `git branch --merged`
 - `git branch --no-merged`

Supprimer une branche `git branch -d <branch_name>`
 - si la branche n’a pas été fusionnée :  `git branch -D <branch_name>`
  - <!-- .element: class="icon warn" -->dans ce cas, perte de données possible


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Remarques sur les branches

<!-- .element: class="icon idea" -->Avec Git, travailler avec des branches est recommandé

Rendu possible grâce à la rapidité du système
 - création
 - passage d’une branche à l’autre
 - fusion
  - détermination automatique de l’ancêtre commun
 - ...

<!-- .element: class="icon info" -->La branche *master*
 - a un fonctionnement identique aux autres
 - c’est simplement la branche créée lors d’un `git init`
  - et la branche extraite par défaut après un `git clone`


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="slide-in none-out" -->
### Exemple d’utilisation des branches (1)

Situation initiale
<div class="center"><img src="images/basic-branching-1.png" width="700px" /></div>


%%%

<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (2)

Création d’une nouvelle branche pour le développement du ticket 53
 - `git checkout -b iss53`
<div class="center"><img src="images/basic-branching-2.png" width="700px" /></div>



%%%

<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (3)

Développements du ticket 53 dans la branche `iss53`
 - `git commit -m "ajout d’un pied de page [problème 53]"`

<div class="center"><img src="images/basic-branching-3.png" width="700px" /></div>



%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (4)


<!-- .element: class="icon warn" -->Un problème urgent est signalé en production
 - déployer le correctif sans déployer les développements en cours du ticket 53
 - simple retour sur la branche `master`
  - `git checkout master`

<div class="center"><img src="images/basic-branching-3.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (5)

Création d’une branche `hotfix` pour le correctif urgent à partir de `master`
 - `git checkout -b hotfix`

Correction du problème dans la branche `hotfix`
 - `git commit -m "correction de l’adresse email incorrecte"`

<div class="center"><img src="images/basic-branching-4.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (6)

Test de la correction et fusion dans la branche `master`
 - `git checkout master`
 - `git merge hotfix`

<div class="center"><img src="images/basic-branching-5.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (7)

La fusion se fait en avance rapide (*fast-forward*)

```bash
Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```

<div class="center"><img src="images/basic-branching-5.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (8)

Suppression de la branche `hotfix`
 - `git branch -d hotfix`

Fin des développements du ticket 53 dans la branche `iss53`
 - `git checkout iss53`
 - `git commit -m "Nouveau pied de page terminé [issue 53]"`

<div class="center"><img src="images/basic-branching-6.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="fade" -->
### Exemple d’utilisation des branches (9)

Fusion de la branche `iss53` dans `master`
 - `git checkout master`
 - `git merge iss53`

*Commit* de fusion

<div class="center"><img src="images/basic-branching-7.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" data-transition="none-in slide-out" -->
### Exemple d’utilisation des branches (10)

La fusion est une fusion à trois sources (*three-way merge*)

```bash
Merge made by the 'recursive' strategy.
README | 1 +
1 file changed, 1 insertion(+)
```

<div class="center"><img src="images/basic-branching-8.png" width="700px" /></div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Quand utiliser des branches ?

<!-- .element: class="icon idea" -->Organisation du travail de l’équipe
 - une branche par *user story*
 - une branche par ticket
 - une branche par environnement
 - branche de *dev*, branche de *prod*
 - branche plus ou moins stable
 - branche protégée
  - *merge request*, *pull request*
 - ...


%%%


<!-- .slide: class="slide" data-background-color="#b4b2A9" -->
### Exemple : l’organisation d’api-sirene
<div class="center">
	<img src="images/api-sirene.gif" width="900px" />
</div>
