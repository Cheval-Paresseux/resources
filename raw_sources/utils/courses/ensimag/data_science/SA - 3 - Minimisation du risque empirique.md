

# 3 - Minimisation du risque empirique (Science des données - MS Big Data)

# Prédicteurs linéaires

Toutes les classes de classifieurs considérées ici sont de la forme : $h_{\mathbf{w},b}\left(\mathbf{x}\right)=\left\langle \mathbf{w},\mathbf{x}\right\rangle +b$ avec $\mathbf{w}\in\mathbb{R}^{d}$ et $b\in\mathbb{R}$. Il est souvent commode d'étendre $\mathbf{w}$ pour y inclure $b$ et ainsi noter $h_{\mathbf{w},b}\left(\mathbf{x}\right)=\left\langle \mathbf{w'},\mathbf{x'}\right\rangle$ avec $\mathbf{w}'=\left(b,w_{1},\cdots,w_{d}\right)\in\mathbb{R}^{d+1}$ et $\mathbf{x}'=\left(1,x_{1},\cdots,x_{d}\right)\in\mathbb{R}^{d+1}$.

Les formes ci-dessus se prêtent à la régression. Notons $L_{d}=\left\{ h_{\mathbf{w},b}\left(\mathbf{x}\right)\right\}$ les applications affines sur des caractéristiques $\mathbf{x}$ de dimension $d$. 

Pour des problèmes de classification, c'est-à-dire lorsque la variable cible $y$ est discrète, cette classe doit être adaptée. Nous nous limitons ici au cas de deux étiquettes. 

Les prédicteurs linéaires s'expriment comme composition d'une fonction scalaire non linéaire $\Phi$ avec $L_{d}$, par exemple :
1. $\Phi=Id$ (fonction identité) pour une régression avec $\mathcal{Y}=\mathbb{R}$.
2. $\Phi={\rm sign}$ (fonction signe) pour une classification binaire avec $\mathcal{Y}=\left\{ -1;+1\right\}$


Commençons par le cas de la régression avant de passer aux problèmes de classification. 

# Régression linéaire


## Régression en dimension 1

Commençons par le plus simple : un régresseur de dimension $1$ : $x\in\mathbb{R}$.

### Régression linéaire en dimension 1

On recherche, dans une classe de prédicteurs $h$ donnée, la meilleure approximation en moyenne quadratique d'un nuage de points $S = \{(x_i,y_i)\in\mathbb{R}^2,i=1\cdots n\}$.

Le risque empirique choisi est l'Erreur Quadratique Moyenne (EQM) : $$ 
R(h) = \mathbb{E} |y_i-h(x_i) |^2 $$
C'est bien l'espérance d'une fonction de perte, quadratique dans ce cas. 

Ce risque est estimé par le risque empirique : $$ \hat{R}_S(h) = \frac{1}{n}  \sum_{i=1}^{n} |y_i-h(x_i) |^2.$$


Le prédicteur optimal est solution de (si cette solution existe) $$ h_\star \in \arg \min_{h\in \cal{H}} \hat{R}_S(h)$$

Pour le choix de la régression linéaire en dimension $1$ : $\cal{H}= \{h:x\rightarrow w_0 + w_1 x \}$ et le risque s'écrit $$ \hat{R}_S(h) = \frac{1}{n} \sum_{i=1}^{n} (w_1 x_i + w_0 - y_i)^2 $$

Trouver les valeurs de $w_0$ et $w_1$ qui rendent la somme $\sum \left(w_1 x_i + w_0 - y_i \right)^2$ minimale conduit à résoudre un système linéaire de $2$ équations à $2$ inconnues. $$
\left\{
\begin{array}{lll} 
\frac{\partial}{\partial w_0} \frac{1}{n} \sum_{i=1}^{n} (w_1 x_i + w_0 - y_i)^2  & = & 0 \\
\frac{\partial}{\partial w_1} \frac{1}{n} \sum_{i=1}^{n} (w_1 x_i + w_0 - y_i)^2 & = & 0
\end{array}
\right.$$

C'est-à-dire
$$
\left\{
\begin{array}{rrll} 
\left(\sum x_i \right) w_0 & + \left(\sum x_i^2 \right) w_1 & = & \sum y_i x_i \\
n \, w_0 &+ \left(\sum x_i \right) w_1 & = & \sum y_i
\end{array}
\right.
$$

On note $$A = \left( 
\begin{array}{ll} 
\sum x_i & \sum x_i^2 \\
n & \sum x_i
\end{array}
\right)
\mbox {, }
\mathbf{b} = \left( 
\begin{array}{l} \sum x_i y_i\\ \sum y_i \end{array}
\right)
\mbox { et  }
\mathbf{w} = \left( 
\begin{array}{l}w_0\\w_1\end{array}
\right).$$

En supposant $A$ inversible, la solution s'écrit $$\mathbf{w} = A^{-1} \mathbf{b}$$

La droite solution est donc obtenue en résolvant un système linéaire de $2$ équations à $2$ inconnues. 


### Remarque sur la régression polynomiale

La méthode se généralise pour un polynôme de degré quelconque.Pour des polynômes du second degré par exemple, la minimisation de $\sum \left(a_2 x_i^2 + a_1 x_i + a_0 - y_i \right)^2$ conduit à résoudre un système linéaire de $3$ équations à $3$ inconnues :

$\left(\sum x_i^4 \right) a_2 + \left(\sum x_i^3 \right) a_1 + \left(\sum x_i^2 \right) a_0 = \sum y_i x_i^2$ 
$\left(\sum x_i^3 \right) a_2 + \left(\sum x_i^2 \right) a_1 + \left(\sum x_i \right) a_0 = \sum y_i x_i$ 
$\left(\sum x_i^2 \right) a_2 + \left(\sum x_i \right) a_1 + \left(\sum x_i^0 \right) a_0 = \sum y_i$ 

Pour un polynôme de degré $k$, le problème sera de résoudre un système linéaire de $k+1$ équations à $k+1$ inconnues. 

Il est important de noter que le problème est linéaire en ses paramètres (les coefficients du polynôme).


## Régression linéaire en dimension $p$

Bien sûr, le régresseur comporte généralement plus d'une composante. La régression linéaire s'appuie alors sur un vecteur de caractéristique de dimension $p$, $\mathbf{x}\in\mathbb{R}^p$.

On observe $n$ vecteurs de caractéristiques : $\mathbf{x_i} = (x_{i,1},\cdots,x_{i,p})$ pour $i=1\cdots n$ et leurs $n$ étiquettes $y_i$ liées par le modèle :

$$
y_i = w_0 + \sum_{j=1}^p w_j x_{i,j} + \sigma \epsilon_i, \, i=1\cdots n
$$

où $\epsilon_i$ suite de v.a. i.i.d. centrées normées, $w_0$ est appelé "intercept".

Le modèle est linéaire en $\mathbf{w}=(w_0 ; w_1,\cdots,w_p)$

$$
\hat{\mathbf{w}} = \arg \min_{\mathbf{w}} \sum_{i=1}^n \left( y_i-w_0-\sum_{j=1}^p w_j x_{i,j}\right)^2
$$

Sous forme matricielle $\mathbf{X}  = \left(\begin{array}{cccc}
1      & x_{1,1} &\cdots & x_{1,p}\\
\vdots & & &\\
1      & x_{n,1} &\cdots & x_{n,p}
\end{array} \right)$ et $Y= (y_1,\cdots,y_n)^T$ d'où l'écriture de la somme des carrés des erreurs 
$$ EQM(\mathbf{w}) = \|\mathbf{Y}-\mathbf{X} \mathbf{w} \|_2^2$$

<!---
Pour $j=1\cdots p+1$ 
$$
<\mathbf{X}^j,Y-X \hat{\mathbf{w}}>= 0
\Rightarrow
(\mathbf{X}^j)^T (Y-\mathbf{X} \hat{\mathbf{w}})= 0
\Rightarrow
\mathbf{X}^T (Y-\mathbf{X} \hat{\mathbf{w}})= 0
$$
d'où
$$
\mathbf{X}^T Y
=\mathbf{X} ^T\mathbf{X} \hat{\mathbf{w}}
$$
-->

Si $\mathbf{X}$ est de rang colonne complet ($p+1$), $\mathbf{X} ^T\mathbf{X}$ est inversible et : $$
\hat{\mathbf{w}} = \left( \mathbf{X} ^T\mathbf{X} \right)^{-1} \mathbf{X}^T Y
$$

Difficultés possibles :
- le rang n'est pas complet : les causes peuvent en être la redondance, le grande dimension, etc,
- grande variance de l'estimation (une ou plusieurs valeurs propres proches de zéro) : instabilité de la solution, surapprentissage.

La régularisation permet de limiter ces problèmes.


<!---
### Moindres carrés

La minimisation du risque empirique, l'EQM dans ce cas conduit à la méthode des moindres carrés
$$
\arg\min_{\mathbf{w}}L_{S}\left(h_{\mathbf{w}}\right)=\arg\min_{\mathbf{w}}\frac{1}{m}\sum_{i=1}^{m}\left(\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle -y_{i}\right)^{2}
$$

L'annulation du gradient donne 
$$
\sum_{i=1}^{m}\left(\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle -y_{i}\right)\mathbf{x}_{i}=\mathbf{0}
$$

En notant $\mathbf{A}=\sum_{i=1}^{m}\mathbf{x}_{i}\mathbf{x}_{i}^{T}$ et $\mathbf{b}=\sum_{i=1}^{m}y_{i}\mathbf{x}_{i}$, ce système s'écrit $\mathbf{A}\mathbf{w}=\mathbf{b}$.

Deux situations sont possibles : 

1. Lorsque $\mathbf{A}$ est inversible, on a simplement $\mathbf{w}=\mathbf{A}^{-1}\mathbf{b}$.
2.  Lorsque $\mathbf{A}$ n'est pas inversible, cela signifie que les cas utilisés pour l'apprentissage n'engendrent pas tout $\mathbb{R}^{d}$. Cela est le cas systématiquement lorsque $m<d$ puisque $m$ est le rang colonne maximum de $\mathbf{A}$. Même pour $m\geq d$, $\mathbf{A}$ peut ne pas être inversible du fait des dépendances entre les $\mathbf{x}_{i}$. $\mathbf{b}$ est toujours dans l'image de $\mathbf{A}$.

La matrice $\mathbf{A}$ est symétrique par construction, elle s'écrit donc $\mathbf{A}=\mathbf{V}\mathbf{\Lambda}\mathbf{V}^{T}$ avec $\mathbf{V}^{T}\mathbf{V}=\mathbf{I}$ et $\mathbf{V}$ diagonale, de colonnes $\mathbf{v}_{i}$.

Construisons la matrice diagonale $\Lambda^+$ dont les éléments diagonaux sont les inverses de ceux de $\Lambda$ si l'inverse existe et valent $0$ sinon : 
$$
\left(\Lambda^{+}\right)_{ii}=
\begin{cases}
0 & \Lambda_{ii}=0\\
\Lambda_{ii}^{-1} & \Lambda_{ii}\neq0
\end{cases}
$$

En définissant $\mathbf{A}^{+}=\mathbf{V}\mathbf{\Lambda}^{+}\mathbf{V}^{T}$ et $\mathbf{\hat{w}}=\mathbf{A}^{+}\mathbf{b}$, on peut écrire $\mathbf{A}\mathbf{\hat{w}}=$$\left(\mathbf{V}\mathbf{\Lambda}\mathbf{V}^{T}\right)$$\left(\mathbf{V}\mathbf{\Lambda}^{+}\mathbf{V}^{T}\right)\mathbf{b}=\mathbf{V}\mathbf{\Lambda}\mathbf{\Lambda}^{+}\mathbf{V}^{T}b=\sum_{i:\Lambda_{ii}\neq0}\left(\mathbf{v}_{i}\mathbf{v}_{i}^{T}\right)\mathbf{b}$, d'où $\mathbf{A}\mathbf{\hat{w}}=\mathbf{b}$.


### Régression linéaire pour des polynômes

Soient
- $\mathcal{H}_{poly}$ la classe des polynôme de degré inférieur ou égal à $n$ en une seule variable. . 

- $\Psi$ l'application de $\mathbb{R}$ dans $\mathbb{R}^{n+1}$définie par 
$$
\Psi:x\longmapsto\left(1,x,\cdots,x^{n}\right)
$$

Un polynôme $p\left(x\right)=a_{0}+a_{1}x+\cdots+a_{n}x^{n}$ de $\mathcal{H}_{poly}$ peut s'écrire $p(x)=\langle \mathbf{a},\Psi(x)\rangle$ avec $\mathbf{a}=(a_0,\cdots,a_n)$. Une régression polynomiale est alors possible en effectuant une régression linéaire en $\mathbf{a}$. 

-->



# Régularisation
 
La minimisation du risque convexifié est plus aisée que celle de la probabilité d'erreur de classification. Reste à préciser l'espace de fonctions sur lequel cette minimisation s'effectue.
<!---
## Choix de l'ensemble des classifieurs

Deux choix classiques sont : 
- Une combinaison linéaire convexe de classifieurs élémentaires (approche typique d'algorithmes comme AdaBoost),
- Un espace de Hilbert à noyau reproduisant (RKHS), en lien avec les méthodes à noyau.
-->
La régularisation peut être réalisée en choisisant ${\cal H}$, elle peut également être réalisée en ajoutant un terme de pénalisation au risque. 

Nous illustrons ce point dans le cas de la régression linéaire.


## Régularisation de la régression linéaire

Idée : introduire un biais sur l'estimation de $\mathbf{w}$ pour réduire la variance.

Régulariser le problème d'estimation en introduisant un terme de pénalisation pour $\mathbf{w}$ : 

$$
\arg \min_{\mathbf{w}} EQM(\mathbf{w}) + \lambda P(\mathbf{w})
$$

Le rôle de ces deux termes : 
- $EQM(\mathbf{w})$ est le terme d'attache aux données,
- $P(\mathbf{w})$ est un *a priori* qui permet de régulariser la solution en introduisant une contrainte sur les coefficients du vecteur $\mathbf{w}$.

- $\lambda>0$ est le coefficient de pénalisation. Son choix résulte d'un compromis entre sur et sous apprentissage. Sa valeur peut être estimée  par validation croisée ou par des technique telles que AIC ou BIC.

### Régularisation $L^2$ : Ridge (Tychonov)

Le choix le plus simple au niveau calculatoire est celui de la norme $l_2$ : $$P(\mathbf{w})=\|\mathbf{w}\|_2^2 = \sum w_i^2$$

Ce choix conduit à la minimisation de la fonction de coût suivante : $$
EQM(\mathbf{w}) + \lambda P(\mathbf{w}) = (\mathbf{Y}-\mathbf{X} \mathbf{w})^T (\mathbf{Y}-\mathbf{X} \mathbf{w})+\lambda \mathbf{w}^T \mathbf{w}$$
Le nouvel estimateur s'écrit :$$
\left( \mathbf{X} ^T\mathbf{X} +\lambda \mathbf{I} \right)^{-1}
\mathbf{X}^T Y$$
- La solution se réduit à la solution classique $\left( \mathbf{X} ^T\mathbf{X}\right)^{-1}\mathbf{X}^T Y$dans le cas $\lambda=0$,
- Le terme additionnel $\lambda \mathbf{I}$ réhausse la diagonale et fait que toutes les v.p. sont strictement positives, donc que la matrice est inversible. 
- Cet estimateur est bien défini et stable pour $\lambda$ suffisamment grand. 


### Régularisation $L^1$ : LASSO

L'estimateur LASSO fait le choix d'une norme de pénalisation qui favorise la parcimonie de $\mathbf{w}$ (c'est-à-dire de nombreuses composantes $w_j = 0$), la norme $l_1$ : $P(\mathbf{w})=\|\mathbf{w}\|_1=\sum |w_j|$. 

Inconvénient du Lasso :
- Pas de formule explicite pour la solution mais des procédures numériques d'optimisation convexe efficaces existent. 

Avantages du Lasso : 
- Converge vers une solution généralement peu dense, c'est-à-dire telle que $w_k = 0$ pour un sous-ensemble d'indice $k$.
- Les variables les moins significatives sont explicitement écartées.
- Stabilité similaire à celle de l'estimateur ridge + sélection des variables. 

<!---
### Régularisation par la parcimonie

Une représentation est dite parcimonieuse lorsque la plupart des coefficients (dans une base donnée) sont nuls.

- La parcimonie est une bonne solution en grande dimension : si l'hypothèse de parcimonie ne tient pas, aucune méthode ne sera capable de récupérer le modèle sous-jacent en haute dimension où $p \approx n$ ou $p > n$,
- mais si l'hypothèse est vraie, alors les paramètres peuvent être efficacement estimés par une méthode qui favorise la parcimonie.
- Le rasoir d'Occam ou les principes KISS (keep it simple, stupid) : même idée que des modèles plus simples sont préférables à des modèles plus complexes.
-->

# Classification 

Ici $\mathcal{X=\mathbb{R}}^{d}$ et $\mathcal{Y}=\{ -1;+1\}$.

## Demi espace

La classe de classifieurs demi-espace $\mathcal{H}_{DE}$ considérée est la composition de $\Phi={\rm sign}$ avec $L_{d}$ : 
$$
\mathcal{H}_{DE}=\left\{ \mathbf{x}\longmapsto {\rm sign}\left(h_{\mathbf{w},b}\left(\mathbf{x}\right)\right)\right\} 
$$
Cette classe est appelée demi-espace car elle divise l'espace en deux. Par exemple, en dimension $d=2$ : $\mathbf{x}=\left(x_{1},x_{2}\right)$ et $\mathbf{x}\longmapsto {\rm sign}\left(w_{1}x_{1}+w_{2}x_{2}+b\right)$ attribue le label $+1$ aux caractéristiques telles que $x_{2}>-\frac{w_{1}}{w_{2}}x_{1}-b/w_{2}$ et le label $-1$ aux autres. Cette classe sépare $\mathbb{R}^{2}$ par une droite (qui coupe $x_{1}=0$ en $x_{2}=-b/w_{2}$). 

En dimension $d$, le vecteur $\mathbf{w}$ définit un hyperplan qui est un espace de dimension $d-1$. Le produit scalaire d'un vecteur de caractéristiques par ce vecteur normal $\mathbf{w}$ permet de déterminer de quel côté de l'hyperplan ce vecteur se trouve. 

La suite donnent quelques exemples de classifieurs.

## Perceptron

Le cas d'une base d'apprentissage séparable par un hyperplan est le cas considéré ici. 

Rosenblatt (1958) propose l'algorithme itératif suivant :
1. Initialisation. $\mathbf{w}_{1}=\mathbf{0}$.
2. Itération $t$. Rechercher dans la base $S$ un exemple mal étiqueté par $\mathbf{w}_{t}$ :
- Si aucun exemple n'est mal classé, la procédure est terminée.
- Si $\mathbf{x}_{i}$ est mal classé, c'est-à-dire si $\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle \neq y_{i}$ : calculer $\mathbf{w}_{t+1}$ par $\mathbf{w}_{t+1}=\mathbf{w}_{t}+y_{i}\mathbf{x}_{i}$ et passer à l'itération suivante.


Intuition du fonctionnement : à l'itération $t$, pour un exemple $i$ mal classé, on a ${\rm sign}\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle \neq y_{i}$ c'est-à-dire $y_{i}\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle <0$. Il est facile de réaliser que chaque itération améliore le séparateur, en effet : 
$$
y_{i}\left\langle \mathbf{w}_{t+1},\mathbf{x}_{i}\right\rangle =y_{i}\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle +y_{i}\left\langle y_{i}\mathbf{\mathbf{x}_{i}},\mathbf{x}_{i}\right\rangle =y_{i}\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle +\left\Vert \mathbf{x}_{i}\right\Vert ^{2}
$$
Autrement dit, à l'itération $t+1$ , $y_{i}<\mathbf{w}_{t+1},\mathbf{x}_{i}>$ est strictement supérieur à $y_{i}\left\langle \mathbf{w}_{t},\mathbf{x}_{i}\right\rangle$ et a donc plus de chance de bien classer l'exemple $i$. 

On peut montrer que le perceptron atteint une solution (dans le cas linéairement séparable) en un nombre fini d'itérations. 

## Régression logistique

Le cas non séparable est plus difficile du point de vue algorithmique. Sa résolution pratique nécessite par exemple de relaxer le coût $0-1$ (c'est-à-dire la fonction signe) en un coût plus facile à prendre en compte.

La régression logistique utilise une version souple de la fonction signe, ce choix permet en particulier d'échapper à la complexité combinatoire. 

La fonction choisie est la sigmoïde (en forme de s) qui vérifie : pour $x\rightarrow+\infty$, $\sigma\left(x\right)\rightarrow1$ et pour $x\rightarrow-\infty$, $\sigma \left( x\right)\rightarrow0$ et $\sigma\left(0\right)=1/2$. Il s'agit d'une forme souple de $\frac{1}{2}\left(1+{\rm {\rm sign}}\left(x\right)\right)$. 
<!---
La fonction logistique est essentiellement une tangente hyperbolique ($2\sigma(x) -1 = \tanh \left(\frac{x}{2}\right)$) et il est possible de passer progressivement de cette sigmoïde à la fonction signe car $\tanh(\alpha u)$ tend vers ${\rm sign} (u)$ lorsque $\alpha$ croît. 

Elle possède les propriétés suivantes :
- Elle s'écrit $\sigma\left(x\right)=\frac{1}{1+e^{-x}}$

- Sa dérivée s'écrit $\sigma'(x)=e^{-x}/(1+e^{-x})^2=\sigma(x)(1-\sigma(x))$

- Sa fonction réciproque s'écrit $\sigma(x) \rightarrow \ln \frac{\sigma(x)}{1-\sigma(x)}.$

La régression logistique repose sur l’hypothèse que le logarithme du rapport des probabilités a posteriori est linéaire par rapport aux caractéristiques $x$. Parmi les distributions qui vérifient cette hypothèse, on retrouve les mélanges de gaussiennes et les caractéristiques à composantes binaires.

Par rapport à l’analyse discriminante, ce ne sont plus les lois conditionnelles aux deux étiquettes qui sont modélisées mais seulement le logarithme de leur rapport.
-->
Les prédicteurs utilisés en régression logistique (composition de la sigmoïde avec les applications linéaires) sont de la forme $$
\mathcal{H}_{log}=\left\{\mathbf{x} \longmapsto h_{\mathbf{w}}\left(x\right) 
= \sigma\left(\left\langle \mathbf{w},\mathbf{x}\right\rangle \right)
= \frac{1}{1+e^{-\left\langle \mathbf{w},\mathbf{x}\right\rangle }}
,\:w\in\mathbb{R}^{d}\right\}.$$

Remarquons que 
- Pour un exemple $x_{i}$ dont l'étiquette $y_{i}$ vaut $y_{i}=+1$, $h_{w}\left(x\right)$ doit être proche de $+1$. 
- Pour un exemple $x_{i}$ dont l'étiquette $y_{i}$ vaut $y_{i}=-1$, $h_{w}\left(x\right)$ doit être proche de $0$, ce qui revient à dire que $1-h_{w}\left(x\right)$ doit être proche de $1$.

Du fait que $$1-h_{\mathbf{w}}\left(x\right)=\frac{e^{-\left\langle \mathbf{w},\mathbf{x}\right\rangle }}{1+e^{-\left\langle \mathbf{w},\mathbf{x}\right\rangle }}=\frac{1}{1+e^{+\left\langle \mathbf{w},\mathbf{x}\right\rangle }},$$
ces deux cas requièrent que $\frac{1}{1+e^{-y_{i}\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle }}$ soit grand (proche de $1$). Il est ainsi possible de construire une fonction monotone croissante de $(1+e^{-y_{i}\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle})^{-1}$ dont la maximisation permet de déterminer une valeur de $\mathbf{w}$. 

De manière équivalente il s'agit de minimiser une fonction croissante de $1+e^{-y_{i}\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle }$. 

Un choix classique est $\log_2\left[1+e^{-y_{i}\left\langle \mathbf{w},\mathbf{x}\right\rangle }\right]$, les solutions qui minimisent le risque empirique s'écrivent alors : $$
w_{\star}\in\arg\min_{w}\frac{1}{m}\sum_{i=1}^{m}\log_2\left[1+e^{-y_{i}\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle }\right]$$


Ce risque empirique est de la forme $$\hat{R}_\phi (h) = \frac{1}{m} \sum_{i=1}^{m}\phi(y_ih(\mathbf{x}_i))$$ avec $\phi(\xi)=\log_2(1+e^{-\xi})$ et $h(\mathbf{x}_i)=\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle$. Autrement dit, la fonction indicatrice des erreurs $\mathbb{1}_{\bullet<0}$ a été remplacée par une nouvelle fonction $\phi$. 

Voyons maintenant cette idée de manière plus générale. 


## Convexification du risque

On a toujours ${\cal X}=\mathbb{R}^d$ pour espace des caractéristiques et ${\cal Y} = \left\{-1,+1\right\}$ comme ensemble d'étiquettes.

<!---
Un algorithme supervisé utilise ${\cal S}=\left\{(x_i,y_i)\subset {\cal X}\times {\cal Y},i=1\cdots n\right\}$ pour estimer un classifieur, i.e. une fonction  $h : {\cal X} \rightarrow  {\cal Y}$. 

Cette fonction $h$ doit classer un nouvel objet (décider si son étiquette est $\pm 1$) à partir de ses caractéristiques $x\in{\cal X}$ en commentant aussi peu d'erreurs que possible.
-->

On transforme le problème pour le remplacer par un problème proche plus maniable en pratique. 

### La probabilité d'erreur, un risque naturel

Bien que pourcentage d'erreurs soit une mesure naturelle du risque, sa minimisation est difficile du fait de sa non convexité et de son manque de régularité qui empêchent l'utilisation de méthodes d'optimisation numériques classiques. 

En vue de rendre le problème convexe, remarquons qu'une erreur, $y_i \neq h(\mathbf{x}_i)$, du fait que $y_i$ et $h(\mathbf{x}_i)$ sont à valeurs dans $\{-1,+1\}$, se traduit par $y_i h(\mathbf{x}_i)=-1$ pour les points mal classés et $+1$ pour les points bien classés. Il est plus commode de plutôt caractériser une erreur par $y_i h(\mathbf{x}_i) < 0$.

En supposant que la base d'exemples ${\cal S}$ est obtenue par échantillonnage i.i.d. selon une loi inconnue $\mathbb{P}$ sur ${\cal X}\times {\cal Y}$, la probabilité de fausse décision s'écrit : 
$$
{\mathbb{P}} \left( Yh(X)<0 \right) 
= {\mathbb{E}}_{\mathbb{P}} 1_{Yh(X)<0}
$$
c'est-à-dire comme l'espérance de la fonction de coût $1_{\bullet<0}$. Cette forme se prête mieux à la généralisation.

### Substitut convexe du risque

 Pour majorer le risque par un risque convexifié, l'approche usuelle consiste à substituer à $1_{\bullet <0}$ une fonction $\phi$ plus grande, dite "calibrée pour la classification" (usuellement cela signifie qu'elle est décroissante, strictement positive, strictement convexe avec $\phi(0)=1$, et $\phi'(0)<0$ avec $\phi(x) \geq 1_{x<0}$). 
 
La figure donne quelques exemples classiques de substituts convexes $\phi$.

![](https://codimd.math.cnrs.fr/uploads/upload_4697fdb7f2e2117ad5ec77bd20cd5798.png)

La fonction indicatrice des erreurs $\mathbb{1}_{\bullet<0}$ (en rouge) est  une fonction de perte également appelée $0/1$, c'est une fonction non convexe qui permet d'évaluer la probabilité d'erreur mais que l'on cherche à remplacer. Les différents substituts convexes classiques sont :
- $\exp(-x)$, fonction exponentielle, c'est la fonction utilisée en boosting,
- $\log_2(1+\exp(-x))$, dite fonction logit, c'est celle de la régression logistique,
- $\max(1-x,0)$ est la fonction ReLU (Rectified Linear Unit) ou Hinge,  très utilisée en réseaux de neurones. Quelques mots sur ReLU : la fonction d'activation ReLU a permis de résoudre plusieurs difficultés pratiques liées à la sigmoïde pour les réseaux neuronaux profonds  :
-- Evanouissement du gradient : un problème avec la fonction logistique est qu'elle sature, cela la rend trop peu sensible aux entrées éloignées de $0$. Dans les couches profondes des grands réseaux, l'information sur le gradient se perd lorsque l'erreur est rétro-propagée à partir des sorties pour mettre à jour les poids, cela empêche d'apprendre efficacement.
La fonction ReLU étant non linéaire mais linéaire par morceaux, elle permet d'optimiser facilement des modèles avec des méthodes basées sur le gradient. Pour les grandes valeurs, sa partie linéaire permet d'éviter l'évanouissement du gradient.
-- ReLU est très peu coûteuse à calculer, son gradient vaut $1$ dans la partie linéaire et $0$ en dehors.

En substituant l'une de ces fonctions à la fonction de perte $0/1$, le risque $R(h) = {\mathbb{E}}_{\mathbb{P}} 1_{Yh(X)<0}$ est remplacé par un risque convexe plus grand : $${\mathbb{E}}_{\mathbb{P}} \phi(Yh(X)<0).$$ 

Il en est de même pour le risque empirique  $\hat{R}(h)=n^{-1} \sum_{i=1}^n 1_{y_ih(\mathbf{x}_i)<0}$ qui est remplacé par  $$ n^{-1} \sum_{i=1}^n \phi(y_ih(\mathbf{x}_i)).$$

Dans cette écriture, il n'est pas nécessaire ni même souhaitable que $h$ soit à valeurs dans $\{-1,+1\}$, il est possible d'utiliser en place de $h$ une fonction de classification $\hbar$ à valeurs réelles, typiquement une fonction $\hbar$ dont le signe donne la décision :  $h = {\rm sign}\circ\hbar$.




# SVM

Les principes des SVM sont brièvement explorés ici dans le cas de données linéairement séparables : les exemples de la base d'apprentissage, $S=\left\{ (\mathbf{x}_{i},y_{i}),i\in\left[m\right]=\left\{ 1,\cdots,m\right\} \right\}$ avec $\mathbf{x}_{i}\in\mathbb{R}^{d}$ et $y_{i}\in\left\{ -1;+1\right\}$, sont séparables linéairement par un hyperplan : 
$$
\exists\mathbf{w}\in\mathbb{R}^{d},\:b\in\mathbb{R}:y_{i}\left(\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle +b\right)>0,\,\forall i\in\left[m\right]
$$

L'importance de cette approche tient en particulier au fait qu'elle permet de prendre en considération et d'améliorer deux aspects essentiels : 

1 - la taille de la base d'apprentissage: le nombre d'exemples nécessaires à l'apprentissage est une caractéristique importante, surtout en grande dimension, les approches à vaste marge permettent de réduire le nombre d'exemples et assurent une certaine robustesse par rapport aux exemples utilisés lors de l'apprentissage, 

2 - la complexité algorithmique: les méthodes SVM donnent des algorithmes efficaces, en particulier en très grande dimension. 

## Choix d'un séparateur à marge maximale

Pour un ensemble $S$ linéairement séparable, le plan séparateur n'est en général pas unique et, si tous les séparateurs annulent le risque empirique, ils n'ont pas tous le même risque de généralisation, ni la même complexité de mise en oeuvre ni d'ailleurs les mêmes exigences sur le cardinal de $S$ pour atteindre une précision donnée.

Parmi les hyperplans qui annulent le risque empirique, tous n'ont pas le même risque de généralisation. On choisit de rechercher celui de plus grande marge, c'est-à-dire le plus éloigné des exemples de $S$, qui, intuitivement, devrait conduire à une erreur de généralisaition plus faible que les autres. C'est un principe des Séparateurs à Vaste Marge (SVM - Support-Vector Machines).

### Distances des exemples au séparateur

La distance entre $\mathbf{x}_{i}$ et le plan $P_{\mathbf{w},b}$ défini par $\left(\mathbf{w},b\right)$, est la plus petite distance entre $\mathbf{x}_{i}$ et les points de $P_{\mathbf{w},b}$, elle s'écrit : $$d\left(\mathbf{x}_{i},P_{\mathbf{w},b}\right)=\min\left\{ \left\Vert \mathbf{x}_i-\mathbf{p}\right\Vert :\left\langle \mathbf{w},\mathbf{p}\right\rangle +b=0\right\}$$

On montre facilement que $d(\mathbf{x}_{i},P_{\mathbf{w},b})=\frac{1}{\Vert\mathbf{w}\Vert }
|\langle\mathbf{w},\mathbf{x}_{i}\rangle +b$. En imposant $\left\Vert \mathbf{w}\right\Vert =1$, cette distance se réduit à $\left|\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle +b\right|$.

### Séparateur de marge maximale

La marge, c'est-à-dire le point de $S$ le plus proche du plan séparateur est à distance : $$
\min_{i\in\left[m\right]=\{ 1,\cdots,m\}:\left\Vert \mathbf{w}\right\Vert =1}\left|\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle +b\right|
$$
et le plan séparateur de marge maximale est donné par :
$$
\arg\max_{\mathbf{w},b:\left\Vert \mathbf{w}\right\Vert =1}\min_{i\in\left[m\right]}\left|\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle +b\right|\::\:y_{i}\left(\left\langle \mathbf{w},\mathbf{x}_{i}\right\rangle +b\right)>0,\,\forall i\in\left[m\right]
$$
<!---
Comme $y_{i}\in\{ -1;+1\}$, si le plan défini par $\mathbf{w},b$ est séparateur, on a 
$$|\langle\mathbf{w},\mathbf{x}_{i}\rangle +b|=y_{i}(\langle \mathbf{w},\mathbf{x}_{i}\rangle +b)>0$$

Ainsi, la recherche du séparateur de plus grande marge s'écrit :
$$
\arg\max_{\mathbf{w},b:\Vert \mathbf{w}\Vert =1}
\min_{i\in[m]}y_{i}(\langle\mathbf{w},\mathbf{x}_{i}\rangle +b).$$
-->
A partir de $S$, l'algorithme SVM calcule le plan séparateur et produit une solution qui appelle plusieurs remarques : 
- Seuls certains exemples qui se trouvent sur la marge, appelés vecteurs support, interviennent dans la solution. 

-  La solution ne dépend que des vecteurs support, les autres points ne jouent aucun rôle. Cette caractéristique a un impact direct sur la complexité de mise en oeuvre et sur la robustesse de la solution. Par exemple, l'ajout de points qui ne sont pas des vecteurs support ne modifie pas la solution.




# Noyau et méthodes à Noyaux

## Espace de redescription.

Supposer que les séparateurs sont linéaires est bien sûr une hypothèse très forte et le plus souvent fausse. Plutôt que de considérer des séparateurs non linéaires dans l'espace de départ, il est préférable de plonger les données dans un espace de dimension plus grande dans lequel les séparateurs sont linéaires. En effet, des frontières non linéaires peuvent souvent être représentées par des frontières linéaires dans un espace de dimension plus grande. Donnons un exemple.

- La transformation de $x_{1},x_{2}$ vers $x_{1}$, $x_{2}$, $x_{1}x_{2}$, $x_{1}^{2}$, $x_{2}^{2}$ permet toujours de représenter des frontières linéaires mais aussi des frontières circulaires : un séparateur circulaire dans l'espace de départ est associé à un séparateur linéaire dans l'espace d'arrivée.

Plus généralement :

1. une application $\psi:\mathcal{X\rightarrow\mathcal{F}}$, plonge les données de $\mathcal{X}$ dans un espace de redescription $\mathcal{F}$.

2. $S$ est transformée en $\hat{S}=\{(\psi(\mathbf{x}_{1}),y_{1}),\cdots,(\psi(\mathbf{x}_{m}),y_{m})\}$

3. L'algorithme d'apprentissage travaille sur $\hat{S}$ et calcule un prédicteur $h$.

4. L'étiquette prédite pour $\mathbf{x}$ est $h(\psi(\mathbf{x}))$

Bien que la qualité du résultat obtenu dépende de la bonne adéquation entre les données et $\psi$, il est souvent possible de choisir des fonctions $\psi$ génériques qui accroissent fortement l'expressivité de l'algorithme. Parmi ces fonctions génériques, l'exemple des polynômes d'une variable réelle peut être facilement étendu aux polynômes multivariables. 

## Noyau et méthodes à Noyaux

L'inconvénient de cette technique de redescription réside dans une forte augmentation de la dimension et donc de la complexité puisque les produits scalaires sont maintenant calculés dans un espace $\mathcal{F}$ de dimension potentiellement très grande.

Il se trouve qu'il est possible de ne pas préciser l'espace $\mathcal{F}$ et de calculer les produits scalaires dans $\mathcal{F}$ directement dans l'espace de départ $\mathcal{X}$. C'est l'astuce des noyaux. 

Un noyau $K$ est défini par :
$$
K\left(\mathbf{x}_{i},\mathbf{x}_{j}\right)=\left\langle \psi\left(\mathbf{x}_{i}\right),\psi\left(\mathbf{x}_{j}\right)\right\rangle 
$$
c'est une mesure de similarité dans $\mathcal{X}$, la transformation $\psi$ assure le passage vers un espace $\mathcal{F}$ dans lequel les similarités sont mesurées par des produits scalaires. 

Il s'avère que beaucoup d'algorithmes d'apprentissage, dont les SVM, peuvent s'écrire en n'utilisant que les valeurs $K\left(\mathbf{x}_{i},\mathbf{x}_{j}\right)$ dans l'espace de départ et sans jamais calculer dans $\mathcal{F}$ ni même préciser $\psi$. 

C'est-à-dire qu'il est possible de ne pas représenter explicitement $\psi$ et de choisir un noyau générique pour peu que celui-ci soit associé à un produit scalaire dans $\mathcal{F}$. 

Pour cela, la fonction $K$ doit vérifier deux conditions : elle doit être symétrique et semi-définie positive.

Choix des noyaux et calcul :
- le calcul s'effectue dans l'espace de départ par une évaluation ponctuelle.
- Parmi les choix génériques (qui ne suppose pas $\psi$ connue) de $K\left(\cdot,\cdot\right)$, trois noyaux classiques sont :
- $K\left(\mathbf{x}_{i},\mathbf{x}_{j}\right)=\left\langle \mathbf{x}_{i},\mathbf{x}_{j}\right\rangle$ : ce noyau correspond à la situation sans redescription, en ce sens les méthodes à noyau généralisent le cas usuel,

    -  $K\left(\mathbf{x}_{i},\mathbf{x}_{j}\right)=\left(\left\langle \mathbf{x}_{i},\mathbf{x}_{j}\right\rangle +1\right)^{p}$,

    - $K\left(\mathbf{x}_{i},\mathbf{x}_{j}\right)=\exp\left[-\frac{\left\Vert \mathbf{x}_{i}-\mathbf{x}_{j}\right\Vert }{2\sigma^{2}}\right]$.

<!---
Notons que cette approche permet même de considérer des espaces de redescription de dimension infinie, comme le montre l'exemple suivant. 

#### Exemple : Noyau Gaussien sur $\mathbb{R}$
$\mathcal{X}=\mathbb{R}$ et $\psi$ telle que pour tout $n\geq0$ il existe $\psi\left(x\right)_{n}=\frac{1}{\sqrt{n!}}\exp\left[-\frac{x^{2}}{2}\right]x^{n}$ alors
\begin{align*}
\left\langle \psi\left(x\right),\psi\left(x'\right)\right\rangle  & =\sum_{n=0}^{\infty}\left(\frac{1}{\sqrt{n!}}\exp\left[-\frac{x^{2}}{2}\right]x^{n}\right)\left(\frac{1}{\sqrt{n!}}\exp\left[-\frac{x'^{2}}{2}\right]x'^{n}\right)\\
 & =\exp\left[-\frac{x^{2}+x'^{2}}{2}\right]\sum_{n=0}^{\infty}\frac{\left(xx'\right)^{n}}{n!}\\
 & =\exp\left[-\frac{\left\Vert x-x'\right\Vert }{2}\right]
\end{align*}
Ici l'espace de redescription est de dimension infinie et néanmoins le calcul est très simple dans l'espace d'origine. 
-->

Les SVM peuvent s'utiliser et s'utilisent presque toujours associée à un noyau. Ainsi, les SVM utilisent pour les idées suivantes :

- hyperplan à marge maximale c'est-à-dire que les exemples de la base d'apprentissage sont les plus éloignés possibles de l'hyperplan séparateur.
 
- Espace de redescription : aplatir la frontière de séparation en passant à un espace de plus grande dimension.

<!---
# Transition vers les réseaux de neurones

## Réseau de neurones à une couche

$x\in\mathbb{R}^p$ et $w\in\mathbb{R}^p$

Combinaison linéaire des entrées de $x$ : $w^Tx$ puis fonction d'activation $\sigma$ non linéaire

$$
y = \sigma \left( w^Tx \right)
$$

Calcul de $N$ sorties selon ce même modèle :

$$
y = \sigma \left( Wx \right)
$$

où $\sigma$ est appliquée composante par composante et $W$ une matrice $p\times N$. 

En ajoutant un biais par composante $b=[b_1,\cdots,b_N]$ on a plutôt $y = \sigma \left( Wx+b\right)$.

En augmentant de $1$ la dimension avec $x^(p+1)=1$ et $W_{j,p+1}=b_j$, cette expression peut àn nouveau s'écrire comme avant. 

---

### Théorème d'approximation

Soit $f : \mathbb{R}^p \rightarrow \mathbb{R}$ mesurable, μ mesure de probabilité sur $\mathbb{R}^p$ , $σ : \mathbb{R} \rightarrow \mathbb{R}$ une sigmoïde telle que $\sigma(t) \rightarrow_{-\infty} 0$ et $\sigma(t) \rightarrow_{+\infty} 1$. 

On definit : 
$$
G = \{ g : x\rightarrow a^T\sigma \left( Wx+b\right), a,b\in  \mathbb{R}^n, W\in\mathbb{R}^{p\times N}\}
$$

$\forall \epsilon>0,\exists g\in G$ et $K\subset \mathbb{R}^p$ tel que $\mu(K)>1-\epsilon$ et 
$$
\mu\left(\{x : |f(x)-g(x)|>\epsilon\} \right) < \epsilon
$$
-->