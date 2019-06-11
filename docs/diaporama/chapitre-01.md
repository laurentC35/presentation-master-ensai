<!-- .slide: data-background-image="images/ensai-t.png" data-background-size="600px" class="chapter" -->

## 1

### Présentation générale de Git

%%%

<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->

### Système de gestion de versions

Un VCS (_Version Control System_)

- enregistre les modifications successives d’un ensemble de fichiers

Cela permet de :

- revenir à une version spécifique
- revenir à une version antérieure d’un fichier spécifique
- retrouver la dernière modification qui a pu introduire un problème

De plus, on peut en général :

- partager ses modifications et de récupérer celles des autres

Surtout utile pour les fichiers texte

- comme le code source !

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->

### Évolution des systèmes de gestion de versions

<table>
	<tr>
		<td>Local (LVCS)</td>
		<td>Cenralisé (CVCS)</td>
		<td>Distribué (DVCS)</td>
	</tr>
	<tr>
		<td><img src="images/local.png" width="300px" /></td>
		<td><img src="images/centralized.png" width="300px" /></td>
		<td><img src="images/distributed.png" width="300px" /></td>
	</tr>
	<tr>
		<td>RCS</td>
		<td>CVS, __Subversion__, Perforce</td>
		<td>__Git__, Mercurial, Bazaar, Darcs</td>
	</tr>
</table>

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->

### Les avantages de la gestion distribuée

Gestion de versions centralisée :

- &oplus; chacun peut savoir qui fait quoi
- &oplus; on peut partager son travail et récupérer celui des autres
- &ominus; point unique de panne
- coupure du serveur : plus personne ne peut collaborer
- corruption du disque : données définitivement perdues

<!-- .element: class="simple-list" -->

Gestion de version distribuée :

- &oplus; sécurité grâce à la redondance des dépôts
- &oplus; permet l’organisation de « groupes de travail »
- &oplus; rapidité

<!-- .element: class="simple-list" -->

%%%

<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="slide" -->

### Genèse de Git

1991 &ndash; 2002 : Noyau Linux géré via des _patchs_ et des archives

2002 &ndash; 2005 : Utilisation du DCVS Bitkeeper

2005 : Bitkeeper devient payant

À partir de 2005 : Linus Torvalds développe un successeur, objectifs :

- vitesse
- simplicité
- développements non linéaires (branches)
- compacité des données
