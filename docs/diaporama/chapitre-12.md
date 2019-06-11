<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 12
### Références à un *commit*


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Faire référence à un *commit*

Références fixes dans le temps :
 - le SHA-1 : `847ef1c44c7ad48c86889e03943bb9d0315dfa1a`
 - une partie du SHA-1 : `847ef1c`
  - minimum 4 caractères et pas d’ambiguïté
 - le nom d’un *tag* : `v3.0`

Références qui évoluent :
 - le nom d’une branche : `tp6`
 - le pointeur `HEAD`
 - une *reflog* : `HEAD@{5}`
  - `git reflog` ou `git log -g` pour les lister

Exemples
 - création d’une branche à partir d’une étiquette :
  - `git branch us104 v3.0`
 - annuler un *commit* :
  - `git revert 847ef1c`

<!-- .element: class="icon idea" -->En général `HEAD` est sous-entendu par défaut


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Faire référence aux ancêtres d’un *commit*

On peut accéder aux ancêtres d’un *commit*
 - le 1<sup>er</sup> parent : `847ef1c~`
 - le 1<sup>er</sup> parent du 1<sup>er</sup> parent : `847ef1c~~` ou `847ef1c~2`
  - et ainsi de suite : `HEAD~23`

Dans le cas particulier d’un *commit* de fusion :
 - le 1<sup>er</sup> parent : `847ef1c^` ou `847ef1c^1`
 - le 2<sup>d</sup> parent : `847ef1c^2`

Exemples
 - annulation du dernier *commit* :
  - `git reset HEAD~`
 - rebasage des trois derniers *commits* :
  - `git rebase -i HEAD~3`
 - rebasage à partir du *commit* `847ef1c` inclus :
  - `git rebase -i 847ef1c^`


%%%


<!-- .slide: data-background-image="images/question.png" data-background-size="600px" class="chapter" -->
## Exercices


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `D^`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `D^ = A`
<div class="center">
	<img src="images/exercice-1.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `K^`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `K^ = J`
<div class="center">
	<img src="images/exercice-2.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `K^2`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `K^2 = F`
<div class="center">
	<img src="images/exercice-3.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `K^2~`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `K^2~ = E`
<div class="center">
	<img src="images/exercice-4.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `K~3`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `K~3 = H`
<div class="center">
	<img src="images/exercice-5.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Plages de commits

`refA..refB`
 - liste des *commits*
  - accessibles depuis `refB`
  - et pas accessibles depuis `refA`

`7568c4d..1a0384f`
 - si ordre chronologique et historique linéaire
  - les *commits* situés entre `7568c4d` et `1a0384f`
  - <!-- .element: class="icon idea" -->`a..b = ]a, b]` et donc `[a, b] = a^..b`

Exemples
 - les commits de `tp5` pas encore fusionnés dans `master`
  - `git log master..tp5`
 - les commits qui seront poussés vers le dépôt distant
  - `git log origin/master..HEAD`
 - annuler une plage de *commits*
  - `git revert 7568c4d^..1a0384f`
 - réappliquer une plage de *commits*
  - `git cherry-pick 7568c4d^..1a0384f`


%%%


<!-- .slide: data-background-image="images/question.png" data-background-size="600px" class="chapter" -->
## Exercices


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `H..M`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `H..M = {L, M}`
<div class="center">
	<img src="images/exercice-range-1.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `N..Q`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `N..Q = {O, P, Q}`
<div class="center">
	<img src="images/exercice-range-2.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `N^..Q`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `N^..Q = {N, O, P, Q}`
<div class="center">
	<img src="images/exercice-range-3.png" />
</div>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="slide-in fade-out" -->
### `Q..K`
<div class="center">
	<img src="images/exercice-0.png" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" data-transition="fade" -->
### `Q..K = {K, F, E, J, L, M, I, H, D}`
<div class="center">
	<img src="images/exercice-range-4.png" />
</div>