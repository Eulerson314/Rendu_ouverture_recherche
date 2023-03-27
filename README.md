
# Ouverture à la recherche 2022/23

## Estimation de volumes de diragramme de voronoï en haute dimension et variables de controle en rendu monte-carlo

### Baptiste GENEST - David COEURJOLLY - Vincent NIVOLIERS

#### Résumé des thématiques du projet

Le coeur du sujet de recherche se concentre sur la question de l'intégration numérique
par des méthodes aléatoires (monte-carlo). En particulier, dans des espaces à dimensions arbitrairement grandes mais en pratique de l'ordre de la dizaine.

La question de la dimension est le point central de la reflexion car la plupart des query géométriques basiques dépendant exponentiellement de la dimension, ainsi, tout le challenge réside dans la recherche de techniques indépendante de la dimension dans leur robustesse et dans leur complexité. Au dela de la difficulté technique une grande partie de la difficulté du projet réside dans le fait que de nombreuses intuitions géométriques deviennent fausses en haute-dimension.

La méthode de Monte-Carlo consiste à approximer
$$I = \int_{\Omega} f dx $$
par 
$$ I \approx I_N = \frac{1}{N}\sum f(x_i) \text{, où } (x_i)_i \sim U(\Omega) $$
Pour améliorer la vitesse de convergence de $I_N$ vers $I$, on explore ici la méthode des variables de contrôle, qui consiste à transformer à $I$ en:
$$I = \int (f - g) dx  + \int g dx$$

où $g$ est aussi "proche" de $f$ possible de telle sorte qu'en intégrant par MC  $\int f - g dx$ l'erreur soit plus petite et de telle sorte que $\int g dx$ porte en elle une grande partie de la valeur de $I$.

Bien sûr, cette méthode impose le fait de supposer $\int g dx$ intégrable explicitement ou facilement approximable.

<ins>L'intérêt du sujet réside donc dans la construction d'une fonction $g$ pertinante sous ces critères et de son intégration. </ins>

D'un point de vue pratique, on cherche à construire $g$ à partir d'un ensemble de $N$ points $(x_i)_i$ où $f(x_i)$ est connue. 

Une approche proposée dans [la thèse de Remi Leluc](https://www.theses.fr/s235377) consiste à construire g comme 
$$g(x) = f(x_i) \text{ où } x_i = \argmin_i d(x_i,x)$$

Cette partition de l'espace par plus proche voisin mène naturellement à la notion de diagramme de voronoï, l'ensemble des points $x$ qui sont plus proches de $x_i$ que des autres points $x_j$ étant la $i$ ème cellule du diagramme de voronoi des $(x_i)_i$.

Ainsi, notre recherche s'est scindée en deux temps:
- Estimation des volumes des cellules du diagramme de voronoi, car intégrer $g$ revient à 
  $$ \int g dx = \sum_i f(x_i) \text{Vol(Vor}_i)$$
- Construction d'une nouvelle fonction $g$ plus fine, similaire mais qui se base sur un algorithme de calcul d'intersection entre un rayon et le diagramme développé par M.Nivoliers.

Toutes nos approches se basent sur l'algorithme de rayshooting car il permet d'explorer les propriétés des diagrammes de voronoï sans avoir à les construire explicitement.

#### Compte-rendu du travail effectué (implémenté)

Références: chaque lien hypertexte mène vers l'article concerné.

- Développement d'une infrastructure d'exploration et de mesure de vitesse de convergence d'estimations de différentes quantités géométriques:
  - Comparaison de vitesse de convergence d'estimation de volume:
    - Méthode de rejet global
    - [Estimation de volume par lancé de rayons](https://www.sciencedirect.com/science/article/pii/S1877050911002092)
    - [Méthode MMC](http://augustin-chevallier.fr/mc/mmc-convex-volume-estimation) (problème d'implémentation très difficile à débug )
  - Comparaison de vitesse de convergence d'estimation de barycentres:
    - Méthode de rejet global
    - échantillionnage de chaque volume par [marche billard](https://www.sciencedirect.com/science/article/pii/S1474667016425711)
  - Comparaison de vitesse de convergence d'erreur d'intégration:
    - Méthode monte carlo classique
    - Méthode CV Voronoï
    - Méthode CV par [regression polynomiale](https://sampling.mpi-inf.mpg.de/2022-salaun-regressionmc.html)
    - Nouvelle méthode CV proposée

#### Code extérieur

- Code pour la suite de halton, une suite à faible discrépance qui a pour propriété une meilleure répartition spatiale et donc une meilleure capacité d'estimation de volume: https://people.sc.fsu.edu/~jburkardt/cpp_src/halton/halton.html
- Code pour la construction exacte du diagramme de voronoi pour avoir une ground truth en 3D https://github.com/BrunoLevy/geogram/wiki/Delaunay3D

### Effort de recherche

L'algorithme de rayshooting permettant de nombreuses applications dans des dimensions jusqu'alors principalement inaccessibles, il a été décidé de rédiger un article le concernant. Ayant participé à l'effort expérimental et ayant proposé une nouvelle application qui emploie l'algorithme je participe à la rédaction de l'article et serai cité comme co-auteur.