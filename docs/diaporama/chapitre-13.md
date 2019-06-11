<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 13
### Boîte à outils Git


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Remisage : `git stash`

Changer de branche alors que la copie de travail est instable
 - on est en plein milieu d’un travail
 - valider ne serait pas une bonne idée

```bash
# Remiser les fichiers modifiés
git stash

# Remiser les fichiers modifiés et les fichiers ajoutés
git stash -u
```

Récupérer le contenu de la remise

```bash
# Récupérer la dernière remise
git stash apply

# Supprimer la dernière remise
git stash drop

# Recupérer et supprimer la dernière remise
git stash pop
```

<!-- .element: class="icon idea" -->En général, `git stash` suivi peu après de `git stash pop` suffisent


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Remisage

Lister les remises
```bash
$ git stash list
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051... Revert "added file_size"
stash@{2}: WIP on master: 21d80a5... added number to log
```

Agir sur une remise plus ancienne
```bash
$ git stash drop stash@{1}
Dropped stash@{1} (364e91f3f268f0900bc3ee613f9f733e82aaed43)
```

Récupérer une remise dans une nouvelle branche
 - si on a tardé à récupérer la remise, risque de conflits

```bash
$ git stash branch testchanges
Switched to a new branch "testchanges"
```
<!-- .element: class="icon info" -->La remise est alors supprimée



%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Étiquetage : `git tag`

Marquer un *commit*
 - souvent les versions livrées en production

<!-- .element: class="icon warn" -->Les étiquettes font toujours référence au même *commit*
 - à la différence des branches qui avancent à chaque nouveau *commit*

Créer une étiquette :
```bash
git tag -a v2.1 -m "Message associé à l’étiquette" # Créer une étiquette annotée
git tag v2.1 # Créer une étiquette légère
```

<!-- .element: class="icon idea" -->Pour les version livrées, utiliser des étiquettes annotées
 - `git describe`

Étiqueter après coup
```bash
git tag -a v2.1 9fceb02
```

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Étiquetage


Lister les étiquettes
```bash
git tag
```

Partager ses étiquettes
```bash
# Partager une étiquette
git push origin v2.1

# Partager toutes ses étiquettes
git push origin --tags
```

Supprimer une étiquette
```bash
# Du dépôt local
git tag -d v2.1

# Du dépôt distant
git push --delete origin v2.1
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Revenir en arrière localement
Modifications non poussées vers le dépôt distant
```bash
# Revenir à un commit donné
git reset --hard 9fceb02

# Annuler les modifications de son espace de travail ~ svn revert
git reset --hard

# Pour supprimer également les fichiers et les dossiers ajoutés
git clean -d -f
```
<!-- .element: class="icon warn" -->Perte des modifications non validées
 - certains *commits* deviennent inaccessibles
  - sauf en utilisant `reflog` ou `tag`


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Annuler un rebasage raté

Le rebasage réécrit l’historique
 - si on revient en arrière, on revient dans le « mauvais » passé

La commande `git reflog` affiche l’historique des positions de `HEAD`
 - historique purement local
  - vide après un clone
  - différent pour chaque développeur
 - pas plus de quelques mois

```bash
1e3845d (origin/tp6, github/tp6, tp6) HEAD@{1}: checkout: moving from master to tp6
b306d5b (tp5) HEAD@{2}: commit: Correction dans les exemples de code filter-branch
a14d9b6 HEAD@{3}: commit: Enoncé tp6 : filter-branch
327d7e6 HEAD@{4}: rebase -i (finish): returning to refs/heads/master
327d7e6 HEAD@{5}: rebase -i (squash): Enoncé du TP6, partie rebasage
34098fe HEAD@{6}: rebase -i (continue): Enoncé du TP6, partie rebasage
624d244 HEAD@{7}: rebase -i (start): checkout refs/remotes/origin/master
63c80c4 HEAD@{8}: commit: Enoncé du TP6, partie rebasage
4794f33 HEAD@{9}: checkout: moving from tp6 to master
```

<!-- .element: class="icon idea" -->Ici pour revenir avant le rebasage :
 - `git reset --hard HEAD@{8}`


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Annuler des modifications distantes
Modifications déjà poussées vers un dépôt distant

<!-- .element: class="icon warn" -->On ne peut plus réécrire l’historique

Commande `git revert`
 - annule un *commit* ou une plage de *commits* en appliquant le *patch* inverse
 - &rarr; création de nouveaux *commits* qui annulent des modifications plus anciennes

```bash
git revert 6686231..b24a4d0
```

```bash
67d6edd (HEAD -> master) Revert "Images des exercices"
d772e54 Revert "Icone question"
6327641 (origin/master, origin/HEAD) Diapos exercice !
f84c416 Exercices sur les références et les ranges
b24a4d0 Icone question
a0f2358 Images des exercices
6686231 Plages de commits
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### La commande `git checkout`

`git checkout` met à jour la copie de travail avec le contenu de la référence passée en paramètre

*checkout* sans chemin spécifié
 - `HEAD` pointe vers la nouvelle branche
 - la nouvelle branche devient la branche courante
 - la copie de travail est entièrement remplacée

Exemples :

```bash
# Extraire une branche existante ou une étiquette
git checkout us100
git checkout v1.0 # En général suivi de git checkout -b correction

# Extraire un commit donné : *detached HEAD*
git checkout b24a4d0

# Extraire un commit donné et travailler dessus dans une nouvelle branche
git checkout -b us101 b24a4d0

# Extraire un tag donné et travailler dessus dans une nouvelle branche
git checkout -b correction v1.0
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### La commande `git checkout`

*checkout* avec chemin spécifié
 - `HEAD` ne bouge pas
 - la branche courante reste la même
 - les fichiers passés en paramètres sont extraits dans la copie locale
  - il sont à l’état modifié

Exemples :

```bash
# Récupérer le fichier application.properties tel qu’il était à la v3.0
git checkout v3.0 -- src/main/resource/application.properties

# Récupérer tous les fichiers du dossier src/main/java/
git checkout b24a4d0 -- src/main/java/

# Récupérer le fichier README.md tel qu’il était lors de l’avant-dernier commit
git checkout HEAD^ -- README.md
```


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Picorage : `git cherry-pick`
Appliquer des modifications contenues dans un *commit* ou une plage de *commits*
 - création d’un nouveau *commit* pour chaque *commit* picoré

<!-- .element: class="icon info" -->Appliquer à une branche ce qui a déjà été fait dans une autre
 - sans fusionner toutes les modifications apportées par la branche

```bash
git cherry-pick e43a6
```

<table>
	<tr>
		<td><img src="images/cherry-pick-1.png" /></td>
		<td><img src="images/cherry-pick-2.png" /></td>
	</tr>
</table>


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Création et application de *patchs*

Plusieurs commits dans un seul fichier
```bash
# Création d’un patch
git format-patch 69f709e..4c70fd2 --stdout > un-seul-fichier.patch

# Application du patch
git apply un-seul-fichier.patch
```
 - le *patch* est appliqué dans la copie de travail
  - il faut indexer et valider
  - utilisable en dehors d’un dépôt Git

Autant de fichiers que de commits
```bash
# Création de plusieurs fichiers de patch
git format-patch 69f709e..4c70fd2

# Application de chacun des fichiers de patch
git am --signoff *.patch
```
 - les commits sont réappliqués un par un dans la copie de travail puis dans le dépôt
 - c’est l’identité de la personne qui a créé le *patch* qui est utilisée


%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Trouver le coupable : `git blame`

Qui a modifié en dernier une ligne donné dans un fichier donné ?
 - `git blame -- path/to/file`
 - quel est le *hash* du *commit* associé à cette modification  ?

<code class="small lang-bash hljs">
<pre>
[...]
a78c2e5e72 (Didier Lefebvre 2014-10-08 22) @Controller
a78c2e5e72 (Didier Lefebvre 2014-10-08 23) public class AccueilController {
a78c2e5e72 (Didier Lefebvre 2014-10-08 24)
c0a8adf307 (Romain Warnan   2015-08-10 25)  @Autowired
c0a8adf307 (Romain Warnan   2015-08-10 26)  private AccueilService accueilService;
e96cb12b05 (Julien Seng     2016-10-27 27)
d1fda3823c (Maxime Beaute   2016-10-07 28)  @Autowired
d1fda3823c (Maxime Beaute   2016-10-07 29)  private UtilisateurService utilisateurService;
c0a8adf307 (Romain Warnan   2015-08-10 30)
74a97baf69 (Bérenger Lodi   2018-07-10 31)  @Autowired
74a97baf69 (Bérenger Lodi   2018-07-10 32)  private PropertiesService propertiesService;
[...]
6f8f48dafe (Romain Warnan   2016-11-21 40)  @RequestMapping({ "/fr/accueil", "/en/accueil" })
d1fda3823c (Maxime Beaute   2016-10-07 41)  public String accueil(ModelMap model, HttpServletRequest request, Langue langue, Utilisateur utilisateur) {
e96cb12b05 (Julien Seng     2016-10-27 42)    utilisateurService.verifierDroitPageAccueil(utilisateur);
366100af54 (Romain Warnan   2016-07-28 43)    Accueil accueil = accueilService.accueil(request.getContextPath(), langue);
366100af54 (Romain Warnan   2016-07-28 44)    model.addAttribute("accueil", accueil);
74a97baf69 (Bérenger Lodi   2018-07-10 46)    model.addAttribute("afficherIndicateurs", Properties.AFFICHER_INDICATEUR_ACCUEIL);
cc2cd70f40 (Romain Warnan   2015-01-26 47)    return "accueil";
cc2cd70f40 (Romain Warnan   2015-01-26 48)  }
a78c2e5e72 (Didier Lefebvre 2014-10-08 49) }
</pre>
</code>

Puis, pour analyser la modification incriminée :
 - `git log -p -1 d1fda3823c`

%%%



<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Dépôt nu

Sur le serveur, le dépôt est nu
 - aucune copie de travail n’est extraite
 - `git init --bare`
 - `git clone --bare <url>`

Ce dépôt peut alors servir de dépôt central
 - on peut y pousser son travail


<!-- .element: class="icon idea" -->Par convention, un dépôt nu possède l’extension `.git`
 - Exemple : `formation-git.git/`

Le contenu d’un dépôt nu est identique au contenu du répetoire `.git/` d’un dépôt normal


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Crochets

Scripts exécutés à un moment précis dans le workflow Git

Exemples dans `.git/hooks/`
 - retirer l’extension `.sample` pour les activer

Cas d’utilisation :
 - vérifier que le code validé respecte certaines règles
  - pas de `TODO`
  - pas `System.out.print`
  - pas d’espaces en trop
  - ...
 - Ajouter automatiquement des informations dans le message de validation
 - Notifier des personnes par email apès un *push*
 - Pousser vers un autre dépôt après un *push*
 - ...

Crochets côté client ou côté serveur


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Liste des crochets

<!-- .element: class="after link" -->[Liste détaillée des *hooks*](https://www.digitalocean.com/community/tutorials/how-to-use-git-hooks-to-automate-development-and-deployment-tasks)

Client :
 - `applypatch-msg` / `pre-applypatch-msg` / `post-applypatch-msg`
 - `pre-commit` / `post-commit`
 - `prepare-commit-msg` / `commit-msg`
 - `post-rewrite`
 - `pre-rebase`
 - `post-checkout`
 - `post-merge`
 - `pre-push`

Serveur :
 - `pre-receive` / `post-receive`
 - `update` / `post-update`

%%%


<!-- .slide: class="tp" -->
## [TP7](https://git.stable.innovation.insee.eu/wehdrc/formation-git#7-boite-à-outils-git)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>