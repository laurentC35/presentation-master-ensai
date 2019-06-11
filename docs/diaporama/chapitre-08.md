<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 8
### Fusion


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Généralités

La fusion est toujours locale
 - aucun risque de casser quoi que ce soit

On peut toujours annuler l’opération
 - `git merge --abort`

<!-- .element: class="icon idea" -->Il est préférable d’avoir une copie de travail propre
 - valider : `git commit`
 - ou remiser : `git stash`

<!-- .element: class="icon warn" -->Un conflit survient quand la __même ligne__ du __même fichier__ a été modifée différemment dans deux branches


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Résoudre un conflit

Lors de la fusion on est averti qu’il y a eu des conflits :
```bash
Automatic merge failed; fix conflicts and then commit the result.
```

État de la copie locale, `git status` :

```bash
both modified:   src/main/java/fr/insee/bar/controller/AccueilController.java
```

Le code contient des marqueurs de conlits :
```java
@GetMapping("/")
<<<<<<< HEAD
@ResponseStatus(HttpStatus.MOVED_PERMANENTLY)
=======
@ResponseStatus(HttpStatus.OK)
>>>>>>> origin/bex2
```

 - modifier le code pour supprimer les conflits et les marqueurs
 - ajouter les fichiers corrigés dans l’index
 - valider une fois que tout est résolu


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Conseils et astuces : avant la fusion

Activer les marqueurs pour voir l’ancêtre commun :
 - `git config --global merge.conflictstyle diff3`

```java
@GetMapping("/")
<<<<<<< HEAD
@ResponseStatus(HttpStatus.MOVED_PERMANENTLY)
||||||| merged common ancestors
@ResponseStatus(HttpStatus.TEMPORARY_REDIRECT)
=======
@ResponseStatus(HttpStatus.OK)
>>>>>>> origin/bex2
```

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Conseils et astuces : pendant la fusion

Voir les parties du code contenant des conflits :
- `git diff` pendant la fusion

```patch
@@@ -16,7 -16,7 +16,13 @@@ public class AccueilController
        private String name;

        @GetMapping("/")
++<<<<<<< HEAD
 +      @ResponseStatus(HttpStatus.MOVED_PERMANENTLY)
++||||||| merged common ancestors
++      @ResponseStatus(HttpStatus.TEMPORARY_REDIRECT)
++=======
+       @ResponseStatus(HttpStatus.OK)
++>>>>>>> origin/bex2
        public String welcome() {
                return "redirect:/accueil";
        }
```

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Conseils et astuces : après la résolution des conflits

Avant *commit*
 - `git diff` ne doit plus rien afficher
 - compiler et lancer l’application
 - exécuter les tests

Après *commit*
 - `git log --cc -p -1` permet d’afficher le patch de la résolution

```patch
        @GetMapping("/")
-       @ResponseStatus(HttpStatus.MOVED_PERMANENTLY)
 -      @ResponseStatus(HttpStatus.OK)
++      @ResponseStatus(HttpStatus.TEMPORARY_REDIRECT)
        public String welcome() {
                return "redirect:/accueil";
        }

```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Ignorer les espaces

Origine de ce type de problèmes :
 - retours à la ligne : Windows &rarr; `CR/LF` ou Linux &rarr; `LF`
 - tabulations ou espaces
 - formatage du code
 - *trailing whitespaces*

Solution :
 - on tente la fusion : `git merge us55`
 - il y a beaucoup de conflits
 - on annule la fusion : `git merge --abort`
 - on effectue la fusion en ignorant les espaces : `git merge -Xignore-space-change us55`
 - la fusion est automatique


```bash
ignore-space-change
ignore-all-space
```


%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Choisir une version

Résoudre un conflit en utilisant l’une ou l’autre version

 - Globalement :

```bash
git merge <branche> # conflits
git merge --abort

git merge -Xours <branche> # garder notre version pour toutes les lignes en conflit

git merge -Xtheirs <branche> # garder leurs version pour toutes les lignes en conflit
```

 - Au cas par cas :

```bash
git merge <branche> # conflits

# garder notre version pour les lignes en conflit dans ce fichier :
git checkout --ours fichier_en_conflit.txt

# garder leurs version pour les lignes en conflit dans ce fichier :
git checkout --theirs autre_fichier_en_conflit.txt

git add .
git commit
```

%%%

<!-- .slide: class="slide" data-background-color="#7580ba" -->
### Annuler une fusion

Pas encore partagée
 - le résultat de la fusion n’a pas encore été envoyé vers le dépôt distant
 - il suffit de revenir au commit précédent la fusion : `git reset --hard HEAD~`

Déjà partagée
 - le résultat de la fusion a déjà été envoyé vers le dépôt distant
 - on ne peut pas réécrire l’historique
 - on va donc lancer un `git revert`
  - &rarr; *revert* = annuler un *commit* en appliquant le *patch* inverse

```bash
git revert --mainline 1 HEAD
```

<div class="center">
    <img src="images/undomerge-revert.png" class="boxed-img" width="500px" />
</div>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Mieux vaut éviter les conflits que les résoudre

Valider souvent
 - des petits lots de modifications homogènes

Préférer de petits fichiers
 - bien découper les classes selon leurs responsabilités

Communiquer avec les autres membres de l’équipe
 - dire sur quoi on travaille
 - bien prévenir en cas de *refactoring* important

Mettre à jour sa copie locale régulièrement
