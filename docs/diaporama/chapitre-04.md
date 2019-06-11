<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 4
### Opérations de base


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Obtenir un dépôt Git

Transformer un dossier en dépôt Git
 - `git init`
 - Le répertoire `.git/` est créé dans le dossier
 - Il ne contient aucun *commit*
 - Les fichiers déjà présents sont considérés comme non suivis par Git (_untracked_)

Cloner un dépôt Git distant
 - `git clone <url>`
 - Le dépôt complet est copié à partir de l’url dans un dossier `.git/` local
  - `git clone ssh://git@git.stable.innovation.insee.eu:22222/wehdrc/formation-git.git`
  - &rarr; `formation-git/.git/`
 - La dernière version de la branche `master` est extraite
 - Le dépôt local reste connecté au dépôt distant
  - `cat .git/config` :

```bash
[remote "origin"]
	url = ssh://git@git.stable.innovation.insee.eu:22222/wehdrc/formation-git.git
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Le cycle de vie du statut des fichiers
<div class="center">
	<img src="images/lifecycle.png" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Connaître l’état des fichiers du dépôt : `git status`
```bash
> git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
	(use "git push" to publish your local commits)
Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)

		modified:		docs/diaporama/slides.css
		new file:		docs/images/basic-rebase-1.png
		modified:		docs/index.html

Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)

		modified:		docs/diaporama/03-configuration.md
		modified:		docs/diaporama/slides.css
		modified:		docs/images/egit-add.png

Untracked files:
	(use "git add <file>..." to include in what will be committed)

		docs/images/basic-rebase-2.png
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Version courte : `git status --short`

```bash
> git status -s
 M	docs/diaporama/03-configuration.md
MM	docs/diaporama/slides.css
A	 docs/images/basic-rebase-1.png
M	 docs/index.html
??	docs/images/basic-rebase-2.png
```

Deux colonnes
 - colonne de gauche = index
 - colonne de droite = copie de travail

Signification :
<table>
	<tr>
		<td>`_M`</td>
		<td>_modified_</td>
		<td>modifié mais pas indexé</td>
	</tr>
	<tr>
		<td>`M_`</td>
		<td>_staged_</td>
		<td>indexé</td>
	</tr>
	<tr>
		<td>`MM`</td>
		<td>_modified_, _staged_</td>
		<td>indexé mais à nouveau modifié après coup</td>
	</tr>
	<tr>
		<td>`A_`</td>
		<td>_added_</td>
		<td>nouveau fichier indexé</td>
	</tr>
	<tr>
		<td>`??`</td>
		<td>_untracked_</td>
		<td>nouveau fichier non indexé</td>
	</tr>
</table>
%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Indexer des fichiers : `git add`
Indexer un fichier en particulier :
```bash
git add src/main/java/fr/insee/bar/controller/AccueilController.java
```

Indexer plusieurs fichiers à la fois :
```bash
# Tous les fichiers du répertoire src/ et de ses sous-répertoires
git add src

# Tous les fichiers se terminant par « .java »
git add "*.java"
```

Indexer tous les fichiers modifiés du répertoire courant :
```bash
git add .
```

Désindexer : `git reset`
```bash
git reset src/main/java/fr/insee/bar/controller/AccueilController.java # un seul fichier
git reset src # tous les fichiers d’un répertoire
git reset "*.java" # tous les fichiers se terminant par « .java »
git reset . # tous les fichiers du répertoire courant
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Indexer avec EGit dans Eclipse

Résultat de la commande `git status -s` :
```bash
 M	docs/diaporama/03-configuration.md
MM	docs/diaporama/slides.css
A	 docs/images/basic-rebase-1.png
M	 docs/index.html
??	docs/images/basic-rebase-2.png
```

<!-- .element: class="icon idea" -->L’interface graphique est ici clairement un atout :
<div class="center">
	<img src="images/egit-add.png" />
</div>

%%%

<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Inspecter les modifications : `git diff`

Modifications non indexées : `git diff`
 - affiche les différences entre la copie de travail et le dernier *commit*

Modifications indexées : `git diff --staged`
 - affiche les modifications que le prochain *commit* va contenir

```patch
diff --git a/src/main/resources/application.properties b/src/main/resources/application.properties
index 3034cd5..e398133 100644
--- a/src/main/resources/application.properties
+++ b/src/main/resources/application.properties
@@ -1,6 +1,6 @@
 application.name=Spring MVC

-spring.profiles.active=responsable
+spring.profiles.active=serveur

 spring.mvc.view.prefix=/WEB-INF/views/
 spring.mvc.view.suffix=.jsp
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Ignorer des fichiers

Certains fichiers ne doivent pas être partagés avec les autres développeurs :

 - fichiers compilés ou packagés
  - `.class`,
  - `.jar`,
  - ...
 - fichiers générés automatiquement
  - `.min.js`,
  - `.min.css`,
  - ...
 - fichiers temporaires
  - `.tmp`,
  - `.swp`,
  - `.lock`,
  - ...
 - fichiers de log ou rapports d’erreurs
  - `.log`, ...
 - fichiers de configuration de l’IDE : Eclipse, Atom, IntelliJ, vim, ...
  - `.project`,
  - `.settings/`,
  - `.classpath`


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Ignorer des fichiers : `.gitignore`

Fichier `.gitignore` à la racine du projet

```ini
# Un fichier en particulier
package-lock.json
.classpath

# Le contenu d’un répertoire
target/
node_modules/

# Un type de fichier
*.jar
*.class

# Un type de fichier à l’exception d’un fichier en particulier
*.log
!install.log

# Dans n’importe quel sous-répertoire
docs/**/*.scss
```

<!-- .element: class="icon warn" -->Le fichier `.gitignore` doit être validé


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Valider des fichiers : `git commit`

Enregistrer le contenu de l’index dans l’historique local :
```bash
git commit
```
 - l’éditeur de texte configuré s’ouvre
 - il est __obligatoire__ de saisir un message de _commit_

Saisir le message tout de suite : `git commit --message` :
```bash
git commit -m "Message de validation"
```

Valider tous les fichiers à l’état modifié : `git commit --all`
 - sans passer par l’index (`git add`)
 - <!-- .element: class="icon warn" -->ne comprend __pas__ les fichiers non suivis (_untracked_)

```bash
git commit -am "Message de validation"
```



%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Remarques sur le message de validation

<!-- .element: class="icon info" -->Le message de validation est très important
 - décrit brièvement les modifications contenues dans le _commit_
 - importance de l’homogénéité des modifications contenues dans un _commit_
 - à l’attention des autres développeurs

Forme d’un message plus détaillé :

```bash
Résumé des modifications

Texte détaillé.
Éventuellement sur plusieurs lignes.
```

Message vide &rarr;  _commit_ annulé
 - les lignes qui commencent par `#` ne comptent pas

<!-- .element: class="icon idea" -->Rappel pour quitter `vi` :
 - sauvegarder et quitter : `Esc` puis `:wq[Enter]` ou `ZZ`
 - quitter sans sauvegarder : `Esc` puis `:q![Enter]`


%%%


<!-- .slide: class="tp" -->
## [TP1](https://git.stable.innovation.insee.eu/wehdrc/formation-git#1-configuration-et-fondamentaux)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>