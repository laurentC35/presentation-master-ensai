<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 2
### Fonctionnement de Git


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Mode de stockage

Stockage sous forme d’instantanés (_snapshots_)
 - et non de différentiels (_deltas_)

Système de références (_cf._ lien symbolique)
 - pour éviter de stocker plusieurs fois un fichier non modifié


%%%


<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->
### Exemple de *patch*


```patch
diff --git a/src/.../controller/ClientsController.java b/src/.../ClientsController.java
index 4bc826f..54cf87a 100644
--- a/src/main/java/fr/insee/bar/controller/ClientsController.java
+++ b/src/main/java/fr/insee/bar/controller/ClientsController.java
@@ -7,18 +7,18 @@ import org.springframework.stereotype.Controller;
 import org.springframework.ui.Model;
 import org.springframework.web.bind.annotation.GetMapping;

-import fr.insee.bar.dao.ClientDao;
 import fr.insee.bar.model.Client;
+import fr.insee.bar.repository.ClientRepository;

@Controller
public class ClientsController {

	@Autowired
-	private ClientDao clientDao;
+	private ClientRepository clientRepository;

@GetMapping("/clients")
public String clients(Model model) {
-	List<Client> clients = clientDao.findAll();
+	List<Client> clients = clientRepository.findAll();
 	model.addAttribute("clients", clients);
 	return "clients";
}
```


%%%


<!-- .slide: class="slide" data-background-color="#7580ba" -->
### Schéma du mode de stockage

Différentiels (Subversion)
<div class="center">
	<img src="images/deltas.png" width="550px" />
</div>

Instantanés (Git)
<div class="center">
	<img src="images/snapshots.png" width="550px" />
</div>


%%%


<!-- .slide: class="slide" -->
### Aperçu de la structure du dépôt Git

Le dépôt Git local est situé dans le répertoire `.git/` du projet :
<div class="center">
	<img src="images/content-git.png" width="400px" />
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Travailler en local

La plupart des opérations se déroulent localement
 - car tout l’historique est stocké localement
 - donc pas de latence réseau
 - donc très rapide
 - et possibilité de travailler hors connexion
  - dans les transports (avion, train)
  - hors du réseau de l’Insee
  - quand GForge est tombé

Exemples
 - afficher l’historique
 - récupérer une ancienne version
 - générer un _patch_ entre deux versions d’un fichier




%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Intégrité des données

Tout est vérifié par une somme de contrôle (_checksum_)
 - algorithme `SHA-1`
  - `[0-9a-f]{40}`
  - exemple : `0dbfc1be5cb26d6325978929debf753681af7b69`

Les objets sont identifiés par la somme de contrôle de leur contenu
 - il est impossible de modifier le contenu d’un fichier ou d’un dossier sans que Git ne le détecte
 - il ne peut pas y avoir de corruption de données sur le réseau

Sauf exception, Git ne fait qu’ajouter de nouvelles données
 - il est presque impossible de perdre son travail
 - on court peu de risques de faire une grosse bêtise


%%%


<!-- .slide: class="slide" -->
### Les trois états d’un fichier

<div class="center">
	<img src="images/three-states.png" />
</div>


%%%


<!-- .slide: class="tp" -->
## [TP0](https://git.stable.innovation.insee.eu/wehdrc/formation-git#0-installation)
<div class="center">
	<img src="images/keyboard.png" width="600px" />
</div>