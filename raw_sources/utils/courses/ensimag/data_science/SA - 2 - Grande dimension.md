# 2 - Grande dimension (Science des données - MS Big Data)
 
 
Référence : Christophe Giraud, Introduction to High-Dimensional Statistics, Chapman and Hall/CRC, 2014

Le terme (curse of dimensionality) est proposé par Richard Bellman en 1961.
Dans des espaces de grand dimension de nouvelles difficultés apparaissent avec des conséquences dans de nombreuses applications, par exemple en apprentissage automatique, en fouille de données ou pour les bases de données. 

Les données (les exemples qui permettent l'apprentissage par exemple) se retrouvent « isolées » et deviennent perdues dans l'espace. Beaucoup de méthodes échouent alors, car le nombre de données pertinentes disponibles est trop faible.


## Exemple illustratif

Leo Breiman donne l'exemple de 100 observations couvrant $[0,1]$ : un histogramme permet une inférence. 

En dimension 10, pour $[0,1]^{10}$, les $100$ observations sont des points isolés dans un vaste espace vide, et ne permettent pas d'inférence fiable. 

Pour réaliser dans $[0,1]^{10}$ une couverture équivalente à celle des 100 points dans $[0,1]$, il faut $10^{20}$ observations.

C'est un obstacle majeur à l'apprentissage : trop peu d'exemples sont disponibles et le nombre d'exemples qui seraient nécessaires est irréaliste. 


## Solutions à la malédiction de la dimension

- Injecter de l'information a priori. C'est un objectif de l'inférence bayésienne. 
- Réduction de la dimensionnalité : remplacer les données originales par des données dans un espace de plus petite dimension, tout en conservant l'essentiel des caractéristiques de celles-ci.  C'est la réduction de la dimensionnalité. Parmi les techniques classiques, citons
-- la sélection de caractéristiques, qui consiste à choisir un petit ensemble de variables représentatives,
-- l'extraction de caractéristiques, qui consiste à définir de nouvelles variables plus pertinentes (exemple l'ACP)


## Quelques propriétés non intuitives en grande dimension.

## Volume de la sphère unité en fonction de la dimension

$$V(r)= \frac{\pi^{d/2}}{\Gamma(1+d/2)}r^d 
$$ 

Pour $d$ grand : $V(r) \sim (\frac{2\pi e}{d})^{d/2} (d\pi)^{-1/2} r^d$
![](https://codimd.math.cnrs.fr/uploads/upload_a7a18f54bd53d19d6682dd880af016f8.png)

Le volume de boule unité décroît très rapidement vers $0$ lorsque la dimension $d$ croît. Une conséquence importante de cette décroissance est que la notion de proche voisin perd son sens.

## Pas de plus proche voisin

On veut couvrir $[0,1]^d$ par $n$ points $x^i$ de sorte que $$\forall x\in[0,1]^d, \exists x^i \in \{x^1,\cdots,x^n\} : \left\|x^i-x\right\| \leq 1$$ $$[0,1]^d \subset \cup_i^n B_d(x_i,1) \Rightarrow n V(1) \geq 1$$ $$ n\geq \frac{\Gamma(1+d/2)}{\pi^{d/2}} \sim \left(\frac{d}{2\pi e}\right)^{d/2 }\sqrt{d\pi}$$

Quelques valeurs numériques : pour d=$20$ : le nombre d'exemples nécessaires est $39$, pour d=$50$ : $5.10^{12}$ et pour d=$100$ : $4.10^{39}$. En pratique, il est impossible de posséder autant d'exemples.

## Répartition de la masse 
  
### Presque tout le volume est dans la croute
  
$B_d(0,r)$ la boucle de rayon $r$, $C_d(0,r) = B_d(0,r) \setminus B_d(0,0.99r)$ $$ \frac{\mbox{Volume de }C_d(0,r)}{\mbox{Volume de }B_d(0,r)} = 1-0.99^d$$

![](https://codimd.math.cnrs.fr/uploads/upload_dbaa23306e757548431ee9fb838f2665.png)

  
### Petite dimension : masse d'une gaussienne dans la cloche
  
  $X \sim {\cal N}(0,1)$ de d.d.p. $p(x)=(2\pi)^{-1/2} \exp\left(-\left\|x\right\|^2/2\right)$

La probabilité pour la v.a. $X\sim {\cal N}(0,1)$ de tomber dans $\{x\in\mathbb{R} : p(x)\geq \delta p(0)\}$ est proche de $1$ pour $\delta$ proche de $0$.


![](https://codimd.math.cnrs.fr/uploads/upload_0cc5fb2a954338ada4285cd2864e44d7.png)


### Grande dimension : masse d'une gaussienne dans les queues}

$X \sim {\cal N}(0,I)$ de d.d.p. $p(x)=(2\pi)^{-p/2} \exp\left(-\left\|x\right\|^2/2\right)$

En grande dimension, contrairement à ce qui est habituel en basse dimension, pour $\delta>0$ petit, la probabilité pour $X$ de tomber dans $$\{x\in\mathbb{R}^d : p(x)\geq \delta p(0)\}= \{ x\in\mathbf{R}^d :\left\|x\right\|^2\leq 2\log\delta^{-1} \} $$ 
n'est pas proche de $1$ : $$ \mathbb{P}\left(\exp \left(-\left\|X\right\|^2/2\right)  \geq \delta\right)
  \leq \frac{1}{\delta}\mathbb{E}
  \left( \exp \left(-\left\|X\right\|^2/2 \right) \right) = \frac{1}{\delta 2^{d/2}}$$
  
L'essentiel de la masse est dans les queues de distribution.
  
  
## Distance entre paires i.i.d. $\mathcal{N}(0,I)$

 $n=5000$, $d=250$
 
 ![](https://codimd.math.cnrs.fr/uploads/upload_d84f7d6e69a2803d4f20ef09268d850c.png)

  $n=5000$, $d=2500$
  
  ![](https://codimd.math.cnrs.fr/uploads/upload_0feb297faa1328afc9b15db685be776d.png)


### Exercice

Programation pour mettre en évidence cette évolution de la distance en fonction de la dimension.
  
## Spectre covariance empirique - Marcenko-Pastur 1967
  
Soit la matrice $$X=[x_1 | \cdots | x_n] \in \mathbf{R}^{d\times n}$$ à entrées aléatoires i.i.d. centrées réduites : pas d'hypothèse gaussienne. 
 
 $n$ vecteurs aléatoires de dimension $d$ i.i.d..
  
Covarianvce empirique : $$ \frac{1}{n}\sum_{i=1}^n x_i x_i^T = \frac{1}{n} X X^T\in \mathbb{R}^{d\times d}$$ 

De rang au mieux $n$ : 
- Classique : $n>>d$, loi des grands nombres
- Applications récentes $n$ de l'ordre de grandeur de $d$ voire $n<d$


$\lambda_1\leq \cdots \leq \lambda_d$ valeurs propres de la covariance empirique

Spectre empirique $$\mu_n=\frac{1}{d}\sum_{i=1}^d \delta_{\lambda_i}$$  
pour $n \rightarrow +\infty$ avec $d/n \rightarrow c\in(0,1]$ ? (classique  $n \rightarrow +\infty$ à $d$ constant)

  Singularité en zéro si $d>n$ : $$\mu_n(\{0\})\rightarrow \mu(\{0\}) = \max(0,1-c^{-1}))$$

  Densité sur $(a,b)=((1-\sqrt c)^2,(1+\sqrt c)^2)$ (support de largeur $4\sqrt{c}$):  $$\frac{1}{2\pi cx} \sqrt{(b-x)(x-a)} 1_{a\leq x \leq b}$$
  
  Exemple de distibution spectrale de la covariance empirique de $x\in \mathbb{R}^d$ de covariance indentité pour $d=2000$, $n=18000$.
  
  L'étalement vaut $4\sqrt{d/n}= 4/3$

![](https://codimd.math.cnrs.fr/uploads/upload_825fa715786ca4629ef07d1036d23b37.png)

#### Exercice : estimer numériquement le spectre de la covariance emipirique pour différentes tailles d'échantillons et différentes dimensions.

Si les paramètres étaient parfaitement estimés, une méthode plus sophistiquée utilisant la moyenne et la covariance ferait mieux qu'une méthode utilisant seulement la moyenne. 

Avec une très mauvaise estimation de la covariance, ce n'est pas toujours le cas. 





# Réduction de dimension

## Motivation de la réduction de dimension

- Lutter contre la malédiction de la dimensionnalité.

- Obtenir un modèle plus simple qui possède une variance plus faible.

- Explicabilité : un faible de nombre de variables peut laisser espérer une possibilité d'explicabilité. 

- Elimination des variables non pertinentes (exemple 2D vers 1D) pour améliorer la qualité des modèles. 

- Les données multivariées vivent le plus souvent sur une variété de dimension inférieure à celle des données brutes mais celle-ci est le plus souvent inconnue : la dimensionnalité intrinsèque est souvent très inférieure à la dimension de la représentation utilisée. 

- Le bruit occupe toutes les dimensions : la réduction de dimension est ainsi une forme de réduction du bruit. 

- Compression avec perte (réduction de la taille des données) 

- Visualisation des données



## Sélection de variables

### Filtrage

On applique un critère de sélection à chacune des variables pour mesurer la pertinence de chacune. Seules une petite partie des variables est sélectionnée. 

Parmi les critères utilisés : la corrélation entre une composante de la caractéristique et l'étiquette, l'information mutuelle. 

Le fait de ne considérer les variables que une à une conduit parfois à manquer des liens importants. 

### Conteneur

On recherche un bon (le meilleur) sous ensemble de variables. 
(wrapper methods, subset selection)
Le nombre de sous ensemble étant $2^p-1$ on recherche plutôt des heuristiques. 

#### Recherche ascendante ou descendante

forward / backward search

On ajoute des variables tant qu'un ajout permet de réduire le risque. 

On supprime une variable tant que sa suppression permet de réduire le risque. 


### Méthodes embarquées (embedded)

Apprentissage conjoint du modèle et des variables à utiliser. 

Exemple de LASSO (contrainte L1)



## Extraction de variables

Construire de nouvelles variables qui capturent de l'information pertinente. 

### Techniques d'extraction (apprentissage multiple)

- Méthodes basées sur la physique, distances géodésiques

- Méthodes statistiques, apprentissage par dictionnaire

- Filtrage (linéaire/non linéaire)


###  Analyse en Composantes Principales (ACP)

<!---
### Approche la plus simple : supposer
- Sous-espace euclidien
- distribution gaussienne pour les variables latentes
- dépendances linéaires gaussiennes des variables observées et de l'état des variables latentes.
-->

Le but de l'ACP est de trouver une transformation linéaire pour réduire la dimensionnalité des données $x$. $$x\in\mathbb{R}^d\rightarrow z \in \mathbb{R}^p \mbox{ avec } p<<d$$

Les variables $z_i$ sont des projections sur les vecteurs $v_i$ : $$z_i=<v_i,x>$$

L'objectif est de trouver un nouveau vecteur de caractéristiques $z$ de plus faible dimension qui capture la plus grand part de la variabilité des données. On veut :

- $z_1,z_2,\cdots,z_p$ sont décorrélées

- Les variances de $z_i$ sont aussi grandes que possible avec $\mbox{Var}(z_1) \geq \mbox{Var}(z_2) \geq \cdots \mbox{Var}(z_p)$


#### Première composante principale

Trouver $v_1$ tel que $z_1$ soit de variance maximale sous la contrainte $\|v_1\|^2=1$

$$
\mbox{Var}(z_1) = \mbox{Var}(<v_1,x>) = \mathbb{E} (v_1^T x x^T v_1) = v_1^T \Gamma v_1
$$

Le Lagragien, pour la maximisation $\mbox{Var}(z_1)$ sous la contrainte $\|v_1\|^2=v_1^Tv_1=1$  s'écrit : 
$$L(v_1,\lambda_1) = v_1^T \Gamma v_1 + \lambda_1 (1-v_1^Tv_1)$$


$$\nabla_{v_1} L = 2 \Gamma v_1 - 2 \lambda_1 v_1=0 \Rightarrow \Gamma v_1=\lambda_1 v_1$$

C'est-à-dire que $v_1$ est un vecteur propre de la matrice de covariance $\Gamma$.

La variance de $z_1$ vaut $$
\mbox{Var}(z_1) =  v_1^T \Gamma v_1 =  v_1^T \lambda_1 v_1 = \lambda_1
$$


#### Deuxième composante principale

Trouver $v_2$ tel que $z_2$ soit de variance maximale sous les deux contraintes :  
$\|v_2\|^2=1$ et $<v_1,v_2>=0$.

Le Lagragien s'écrit : 
$$L(v_2,\lambda_2) = v_2^T \Gamma v_2 + \lambda_2 (1-v_2^Tv_2) + \beta (0-v_2^Tv_1)$$

$$\nabla_{v_2} L = 2 \Gamma v_2 - 2 \lambda_2 v_2 - \beta v_1=0$$

$$\Gamma v_2 = \lambda_2 v_2 + \frac{\beta}{2} v_1$$


En multipliant à gauche par $v_1^T$ : 

$$v_1^T \Gamma v_2 = \lambda_2 v_1^Tv_2 + \frac{\beta}{2} v_1^Tv_1= \frac{\beta}{2}
$$

Or on a aussi 
$$
v_1^T \Gamma v_2 = (\Gamma v_1)^T v_2 = (\lambda_1 v_1^T) v_2 = 0
$$

d'où $\beta = 0$ et donc $\Gamma v_2=\lambda_2 v_2$ : 
$v_2$ est le deuxième plus grand vecteur propre de la matrice de covariance $\Gamma$.




<!---
## En pratique

Estimation empirique de la moyenne et de la covariance.

Calcul des $p$ plus grandes valeurs propres et vecteurs propres de $\Gamma$. 

Choix de la valeure de $p$ : 

$$
\frac{\sum_{k=1}^p \lambda_k}{\sum_{k=1}^d \lambda_k}
$$

Attention les mises à l'échelle et les normalisations ont de l'importance. 


# Avec noyau

Étend l'analyse en composantes principales (ACP) conventionnelle à un espace de caractéristiques de haute dimension en utilisant le "kernel trick".


Peut extraire jusqu'à N (nombre d'échantillons) composantes principales non linéaires d'un espace de caractéristiques NON Linéaire.

* sans calculs coûteux.

* La réduction de dimension sera NON-LINAIRE dans l'espace original

Soit k une fonction noyau semi-définitive positive : 

$$
K(x,y) = <\Phi(x),\Phi(y)>
$$

On suppose que 

$$
m = \frac{1}{N} \sum_{n=1}^N \Phi(x_n)=0
$$
-->