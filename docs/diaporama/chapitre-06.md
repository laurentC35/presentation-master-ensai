<!-- .slide: data-background-image="images/ensai.png" data-background-size="600px" class="chapter" -->

## 6

<h1>Application de gestion de spécification</h1>

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Choix de l'architecture

#### Architecture de type client-serveur Web

#### Communication par l'intermédiaire du protocole http au travers d'une API

#### Respect de l'environnement applicatif de l'Insee : CCT (Cadre de cohérence technique)

<div class="center">
	<img src="images/appli-back.jpg" width="600px" />
</div>

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->
### Une API : qu'est-ce que c'est

API : Application Programming Interface

- partie de l'application qui expose les services à l'extérieur, c'est la porte d'accès au back-office
- permet de séparer les responsabilités entre le client et le serveur
- meilleure portabilité et évolutivité
- chaque partie peut évoluer séparément

API de type REST

- API sans état
- chaque requête doit contenir toutes les informations nécessaires
- plus requête en simultané


%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Le Front-Office

Application vu par le client, visuel, faite pour intéragir avec le client :

- Interface graphique en JavaScript
- Utilisation des libraries React et Redux
- Ecriture des composants avec React et JSX
- Gestion de l'état de l'application avec Redux
- Librairie Bootstrap pour gérer les CSS

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Fonctionnement du front-office

<div class="center">
	<img src="images/diag_redux_final.jpg" width="800px" />
</div>

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Le Back-Office

Application hebergée côté serveur, n'est pas accessible directement par le client, s'occupe des traitements.
Elle respecte une architecture en 3 couches fonctionnelles :

- Couche web-services : l'API
- Couche de services : les traitements
- Couche de persistance : la base de données

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Fonctionnement du back-office

<div class="center">
	<img src="images/diag_back_office_service.jpg" width="800px" />
</div>

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### La base de donneés

Seulement deux tables :

- les questionnaires
- les versions de questionnaires

<div class="center">
	<img src="images/table_data.jpg" width="600px" />
</div>


%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Les bénéfices obtenus grâce au découpage du Back-Office

Le développement en couches permet d'obtenir :

- une forte cohérence au sein d'une couche
- un faible couplage entre les couches
- une grande modularité

Pourquoi c'est bien ?

- Cela permet de développer plus facilement, plus rapidement
- le code est beaucoup plus lisible et maintenable par une autre personne
- on peut facilement ajouter de nouvelles fonctionnalités car c'est bien découpé

%%%

<!-- .slide: class="slide" data-background-image="images/ensai.png" data-background-size="600px" -->

### Le module de comparaison de version

Le module permettant de comparer plusieurs versions du document de spécifcation est intégré dans l'application.
Cette comparaison faite en Java dans l'appli back-office avec une librairie spéciale (XMLUnit)

On peut personnaliser l'affichage car on maîtrise la comparaison :

<div class="center">
	<img src="images/modif.jpg" width="600px" />
</div>
