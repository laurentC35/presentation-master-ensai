<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 11
### Réécriture de l’historique


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Modifier la dernière validation

<!-- .element: class="icon idea" -->Après avoir validé, on se rend compte d’une erreur :
 - faute dans le message
 - fichiers oubliés ou en trop
 - ...

Modifier simplement le message
 - `git commit --amend`
  - l’éditeur de texte s’ouvre, il contient le dernier message de *commit*
 - Autre possibilité : `git commit --amend --message "Message de commit"`

Modifier aussi le contenu
 - indexer ou supprimer des modifications au préalable
  - `git add` ou `git rm`
 - puis `git commit --amend`

<!-- .element: class="icon warn" -->Interdit si les modifications ont déjà été poussées vers le dépôt distant


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Réécrire des modifications plus anciennes

Pas d’outil spécifique mais « rebasage interactif »
 - pour modifier les `n` derniers *commits* : `git rebase -i HEAD~n`

Pour chacun des `n` derniers *commits* on a le choix entre :

<table class="left small">
	<tr>
		<th><code>pick</code></th>
		<th><code>p</code></th>
		<th>Garder le commit tel quel</th>
	</tr>
	<tr>
		<td><code>reword</code></td>
		<td><code>r</code></td>
		<td>Changer le message</td>
	</tr>
	<tr>
		<td><code>edit</code></td>
		<td><code>e</code></td>
		<td>S’arrêter pour modifier le <i>commit</i></td>
	</tr>
	<tr>
		<td><code>squash</code></td>
		<td><code>s</code></td>
		<td>Fusionner ce <i>commit</i> avec le précédent</td>
	</tr>
	<tr>
		<td><code>fixup</code></td>
		<td><code>f</code></td>
		<td>Fusionner ce <i>commit</i> avec le précédent et utiliser le message précédent</td>
	</tr>
	<tr>
		<td><code>exec</code></td>
		<td><code>x</code></td>
		<td>Exécuter une commande</td>
	</tr>
</table>

On peut en outre :
 - réordonner les *commits* en changeant l’ordre des lignes
 - supprimer des *commits* en supprimant les lignes correspondantes

Annuler le rebasage :
 - `git rebase --abort`


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Programme de rebasage interactif

```bash
git log --oneline
```

<div class="center">
	<img src="images/rebase-i-log.png" width="400px" />
</div>

```bash
git rebase -i 7afc44a^
```

<div class="center">
	<img src="images/rebase-i-todo.png" width="400px" />
</div>

<!-- .element: class="icon warn" -->L’ordre des *commits* est inversé par rapport à `git log`
 - ordre chronologique &rarr; « on réécrit l’histoire »


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Fusionner des *commits*

`fixup`
 - c’est le message du plus ancien *commit* qui sera utilisé
  - on peut en profiter pour modifier ce message

<table class="medium">
<tr>
<td>avant</td>
<td>programme</td>
<td>après</td>
</tr>
<tr>
<td><pre><code class="lang-bash hljs">fe0d95c JPA : Role
090b778 JPA : Employe
4f99ebc JPA : Cocktail
7afc44a JPA : Client</code></pre></td>
<td><pre><code class="lang-bash hljs">reword 7afc44a JPA : Client
fixup 4f99ebc JPA : Cocktail
fixup 090b778 JPA : Employe
fixup fe0d95c JPA : Role</code></pre></td>
<td><pre><code class="lang-bash hljs">67d60cc Ajout des annotations JPA sur les entités</code></pre></td>
</tr>
</table>

`squash`
 - l’éditeur de texte s’ouvre
  - il contient les trois messages, on peut en faire ce qu’on veut

<table class="medium">
<tr>
<td>avant</td>
<td>programme</td>
<td>après</td>
</tr>
<tr>
<td><pre><code class="lang-bash hljs">4b5e1b5 Ignorer le dossier docs/
6e47d26 Ménage : servlet-dispatcher.xml
0d37c11 Suppression d’un vieux fichier</code></pre></td>
<td><pre><code class="lang-bash hljs">pick 0d37c11 Suppression d’un vieux fichier
squash 6e47d26 Ménage : servlet-dispatcher.xml
squash 4b5e1b5 Ignorer le dossier docs/</code></pre></td>
<td><pre><code class="lang-bash hljs">346113b Ménage</code></pre></td>
</tr>
</table>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Fusionner des *commits* automatiquement

<!-- .element: class="icon idea" -->Option `--autosquash` de `git rebase -i`
 - activer l’option par défaut : `git config --global rebase.autosquash true`

Oubli dans un *commit* qu’on ne peut plus amender :

```bash
git add a.txt && git commit -m "Modification a.txt"
git log --oneline -1 # 32f91fd Modification a.txt

git add src/ && git commit -am "Correction problème Y"
git log --oneline -1 # cba893a Correction problème Y

vi a.txt # Correction d’un oubli dans le fichier a.txt
git add a.txt
git commit --fixup 32f91fd # <== option '--fixup'
git log --oneline -1 # 7fef6a9 fixup! Modification a.txt

git rebase -i master
```

Le programme de rebasage est déjà bon :

```bash
pick 32f91fd Modification a.txt
fixup 7fef6a9 fixup! Modification a.txt
pick cba893a Correction problème Y
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Diviser un *commit* en plusieurs

`edit`
 - le programme s’arrête et nous donne la main
 - on en profite pour revenir un cran en arrière : `git reset HEAD^`
  - l’index est vide
  - la copie de travail contient les modifications
 - on indexe puis on valide les fichiers que l’on souhaite
  - possibilité d’indexer des parties de fichier avec `git add --patch`
 - on répète les opérations d’indexation et de validation autant de fois que l’on souhaite
 - on laisse le rebasage se poursuivre : `git rebase --continue`

<table class="medium">
<tr>
<td>avant</td>
<td>programme</td>
<td>après</td>
</tr>
<tr>
<td><pre><code class="lang-bash hljs">b5f409e Titre README.md et corrections</code></pre></td>
<td><pre><code class="lang-bash hljs">edit b5f409e Titre README.md et corrections</code></pre></td>
<td><pre><code class="lang-bash hljs">6e47d26 Titre dans README.md
346113b Orthographe</code></pre></td>
</tr>
</table>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Réécrire complètement l’historique

<!-- .element: class="icon boom" --> L’option nucléaire : `filter-branch`

<table class="left medium">
	<tr>
		<th>Objectif</th>
		<th>Filtre à utiliser</th>
	</tr>
	<tr>
		<td>modifier l’arborescence dans l’historique</td>
		<td><code>--index-filter</code></td>
	</tr>
	<tr>
		<td>modifier le contenu de fichiers dans l’historique</td>
		<td><code>--tree-filter</code></td>
	</tr>
	<tr>
		<td>modifier les métadonnées de l’historique</td>
		<td><code>--env-filter</code></td>
	</tr>
	<tr>
		<td>faire d’un sous-répertoire la nouvelle racine</td>
		<td><code>--subdirectory-filter</code></td>
	</tr>
	<tr>
		<td>modifier tous les messages de validation</td>
		<td><code>--msg-filter</code></td>
	</tr>
</table>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Exemples de code (1)

Supprimer le fichier `password.txt` de tout l’historique :
```bash
git filter-branch -f --index-filter '
	git rm --cached --quiet --force "password.txt"
' --prune-empty -- HEAD
```

Supprimer le dossier `target/` de tout l’historique :
```bash
git filter-branch -f --index-filter '
	git rm --cached --quiet --force -r "target/"
' --prune-empty -- HEAD
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Exemples de code (2)

Remplacer le texte correspondant à un motif donné :
  - `pattern_a_remplacer` &rarr; `*****` dans le fichier `fichier.txt` :

```bash
git filter-branch -f --tree-filter '
	sed -i -E "s/pattern_a_remplacer/*****/g" "fichier.txt"
' --prune-empty -- HEAD
```

Supprimer la ligne correspondant à un motif donné :
```bash
git filter-branch -f --tree-filter '
	sed -i -E "/pattern_ligne_a_supprimer/d" "fichier.txt"
' --prune-empty -- 092a022^..HEAD
```

%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Exemples de code (3)

Faire du sous-dossier `frontend/` la nouvelle racine du dépôt :
```bash
git filter-branch -f --subdirectory-filter "frontend/" --prune-empty -- HEAD
```

Modifier l’adresse mail d’un développeur :
 - `ancien.mail@insee.fr` &rarr; `nouveau.mail@insee.fr`

```bash
git filter-branch -f --env-filter '
old_mail="ancien.mail@insee.fr"
new_mail="nouveau.mail@insee.fr"
if [ "$GIT_AUTHOR_EMAIL" = "$old_mail" ] || [ "$GIT_COMMITTER_EMAIL" = "$old_mail" ]
then
	export GIT_AUTHOR_EMAIL="$new_mail"
	export GIT_COMMITTER_EMAIL="$new_mail"
fi
' -- HEAD
```

Ajouter le texte `© Insee` à la fin de chaque message :
```bash
git filter-branch -f --msg-filter '
	cat && echo && echo "© Insee"
' -- HEAD
```

%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Précautions d’usage

<!-- .element: class="icon info" -->`filter-branch` permet de réécrire tout l’historique à partir d’un certain point dans le temps

Pour partager le nouvel historique : `git push --force`
 - ôter la protection de la branche dans le dépôt distant (Gihub, Gitlab, GForge)

<!-- .element: class="icon time" -->Se synchroniser
 - chaque développeur devra supprimer sa copie locale et cloner le nouvel historique du dépôt


%%%


<!-- .slide: class="tp" -->
## [TP6](https://git.stable.innovation.insee.eu/wehdrc/formation-git#6-r%C3%A9%C3%A9crire-lhistorique)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>
