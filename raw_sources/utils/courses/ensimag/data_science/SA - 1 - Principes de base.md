# 1 - Principes de base (Science des données - MS Big Data)

Le "Machine Learning" ou "Apprentissage statistique" est l'une des nombreuses branches de l'intelligence artificielle (IA).
Il s'agit d'une discipline récente, les premiers papiers spécialisés remontent aux années 70. Beaucoup de directions sont apparues depuis, beaucoup d'explorations sont encore possibles. 

Ce cours concerne uniquement les principes sur lesquels repose l'apprentissage statistique. Quelques exemples d'algorithmes sont donnés en lien avec ces principes généraux. 

Deux références importantes pour une description assez exhaustive des algorithmes courants sont 

- Gareth James, Daniela Witten, Trevor Hastie, Robert Tibshirani. An Introduction to Statistical Learning with Applications in R. Springer Texts in Statistics.

- Kevin P. Murphy. Machine Learning: A Probabilistic Perspective (Adaptive Computation and Machine Learning series). The MIT Press, 2012.

Pour  approfondir les aspects liés à la mise en oeuvre en utilisant des langages et des librairies classiques (Python, Scikit-Learn, Keras, Tensorflow), on pourra se référer par exemple au livre 


- Aurélien Geron. Machine Learning avec Scikit-Learn. Mise en oeuvre et cas concrets. Seconde édition, 2019.

Ce cours traite seulement d'apprentissage supervisé, aussi appelé prédiction. 

# Qu'est-ce que c'est ?

## Ce n'est pas

Ce ne sont pas (du moins pas seulement) des visions de la science-fiction.
Ce domaine s'est développé au travers de nombreuses applications spécialisées à la fois moins spectaculaires et plus omniprésentes. Les premières ont sans doute été :

* la reconnaissance optique des caractères (OCR - Optical Character Recognition) dans les années 50 (travaux de David H. Shepard), 
* les filtres anti spam (du nom d'un personnage de sketch des Monty Python datant de 1970) dans les années 1990.

De très nombreuses applications spécialisées ont suivi : reconnaissance vocale, assistants vocaux, reconnaissance de l'écriture manuscrite, reconnaissance des images, systèmes de recommandation, etc. 

## C'est 

C'est une manière particulière de programmer une machine pour qu'elle apprenne à partir des données.
Une définition donnée en 1959 par Arthur Samuel est  "Apprendre des données sans programmation explicite". 
Plus tard, en 1997, Tom Mitchell en donna une définition plus précise : "Une machine est à même d'apprendre d'une expérience E au sujet d'une tâche T si sa performance P sur la résolution de cette tâche T augmente au fil des expériences E" . 

Des expériences à l'expertise : d'une certaine façon, apprendre consiste à transformer des expériences en une expertise. C'est le rôle d'un algorithme d'apprentissage. L'expérience, ce sont les données (des mails étiquetés (spam vs non spam) par un humain par exemple, ou bien encore des prix de maisons selon différentes caractéristiques). L'expertise c'est l'algorithme (le programme) que l'algorithme d'apprentissage produit : ce programme sera capable, à partir de nouvelles données, de prendre une décision telle qu'une classification en catégories (classification : un mail est ou n'est pas un spam par exemple) ou de prédire une valeur (régression : le prix d'une maison). 

Des questions se posent sur les données (leur volume par exemple), les ressources nécessaires à l'apprentissage (faisable ou non) et sur la manière de mesurer les performances de la solution obtenue.

# Quelques exemples d'application importants

Nous donnons ici quelques exemples classiques d'applications du Machine
Learning. 

## Filtre anti-spam

Un système de reconnaissance des pourriels se construit en demandant d'abord à un utilisateur de taguer les courriers qu'il considère comme étant indésirables. 

Dans une approche classique, il faudrait établir une liste de règles pour caractériser ce qu'est un courrier indésirable. Outre le fait que cette liste serait longue et complexe, elle devrait être en permanence mise à jour, cette opération de maintenance serait difficile. L'idée serait de repérer des motifs qui tendent à indiquer que le courrier est indésirable, motifs présents dans le sujet du message, dans son corps ou bien encore dans l'adresse de l'expéditeur.

Au contraire, une approche basée sur l'apprentissage statistique n'utiliserait pas explicitement une liste de règles, sa mise à jour serait facile, l'apprentissage se ferait à partir des données.

## Problèmes trop complexes ou sans solution connue

Problèmes pour lesquels une solution classique serait trop complexe à mettre en œuvre, ou pour lesquels il n'existe aucune solution classique connue. 

Les problèmes de reconnaissance vocale peuvent être vus comme appartenant à cette catégorie : si la question était seulement de distinguer entre deux mots, une solution basée sur les caractéristiques vocales de ces deux mots serait facile à mettre en œuvre. Malheureusement, une telle solution ne passe pas à l'échelle, lorsque le vocabulaire à reconnaître devient grand il n'est plus possible de procéder de la sorte. Il est alors préférable d'apprendre à partir d'une très grande base de mots prononcés par différents locuteurs.

## Fouille de données

Un système d'apprentissage statistique peut avoir vocation à aider l'humain à apprendre des choses pertinentes à partir de grand volume de données, à mettre en évidence des relations qui ne sautent pas aux yeux *a priori*, c'est le Data Mining (fouille de données). 

## Autres exemples classiques

* Classement d'image en différentes catégories, 
* Diagnostic médical : détection et classification de tumeurs à partir
d'images IRM, 
* Classement des articles de presse en différentes catégories, 
*  Prédictions de prix, 
* Commande vocale, 
* Détection d'anomalies dans une séquence temporelle de données, 
* Segmentation d'un ensemble de clients en différentes catégories, 
* Visualisation et réduction de dimension. 

# Catégories d'algorithmes

Sous le terme Machine Learning se cachent différents types d'algorithmes que nous pouvons classer en grandes catégories de la manière suivante (les détails sont donnés aux paragraphes suivants) : 

* Supervision : **apprentissage supervisé**, apprentissage **non supervisé**, apprentissage **semi supervisé**, apprentissage **par renforcement**.
* Apprentissage **en ligne**, apprentissage **hors ligne**.
* Algorithme **basé sur des exemples**, algorithme **basé sur un modèle**. 
* Un algorithme d'apprentissage **passif** se contente de regarder ce qui se passe dans l'environnement. Un algorithme **actif** construit des expériences aussi instructives que possible : exemple du physicien qui conçoit ses expériences pour obtenir un maximum d'informations. 


## Type de supervision de l'apprentissage.

### Algorithmes supervisés

L'apprentissage s'effectue à partir d'exemples étiquetés.

La base d'apprentissage est composée d'un ensemble d'exemples pour lesquels les étiquettes sont connues (typiquement, un humain a attribué les étiquettes aux exemples), à partir de ces exemples il s'agit de construire un algorithme capable de classer de manière aussi fiable que possible de nouveaux exemples (généralisation à des cas qui n'appartiennent pas à l'échantillon utilisé pour l'apprentissage). La détection de spam rentre dans cette catégorie. 

L'instructeur peut être coopératif (les exemples sont choisis pour être aussi instructifs que possible), indifférent (cas des données naturelles) ou un adversaire (génération de spam de telle sorte qu'ils ne soient pas classés dans la catégorie spam).

Quelques algorithmes utiles : k-NN ("k-nearest neighbors" : k-plus proches voisins), régression linéaire, régression logistique, SVM ("support vector machine" - séparateurs à vaste marge), arbres de décision, random forest , réseaux de neurones. 

### Algorithmes non supervisés

Apprentissage à partir d'exemples sans étiquette. 

Le problème consiste à grouper des objets similaires en paquets (clusters), c'est le clustering. La détection de comportements anormaux rentre dans cette catégorie : par exemple en sécurité informatique, le problème peut consister à détecter des événements anormaux à partir de fichiers de log. 

Quelques algorithmes utiles : visualisation (préserver la structure, conserver les clusters séparés dans la visualisation), réduction de dimension (simplifier les données sans trop perdre d'information, e.g. fusion de "features" proches, "features extraction", la réduction de dimension est souvent un prétraitement), PCA (analyse en composantes principales), kernel PCA.

### Algorithmes semi supervisés

L'exemple typique est celui de la création de groupes de photos de personnes que l'on souhaite classer à l'aide du nom des personnes qui apparaissent dans ces photos. Une fois que les groupes ont été constitués, il suffit d'une étiquette pour un groupe. Les algorithmes semi supervisés sont souvent obtenus en associant une méthode supervisée avec une méthode non supervisée. 

### Algorithmes par renforcement.

L'agent observe son environnement et sélectionne des actions, une récompense lui est alors donnée en fonction de la performance obtenue, l'agent adapte son comportement en fonction de cette récompense. La stratégie de maximisation de la récompense, ou de minimisation de la perte, conduit à une adaptation du comportement. 

Exemple du jeu d'échec : position intermédiaire entre supervisé et non supervisé : pas de supervision immédiate, le résultat (partie gagnée / nulle / perdue) ne sera connu qu'en fin de partie. 

## En ligne / Hors ligne

### Apprentissage hors ligne

Les données sont traitées par lots ("batches"), toutes les données sont traitées en une seule fois. Les algorithmes de type "batch" sont exigeants en termes de ressources informatiques : CPU, RAM, stockage, temps de calcul. De ce fait, la mise à jour de la fonction d'apprentissage doit être plus fréquente, en pratique cela signifie que l'évolution des caractéristiques doit être lente en fonction du temps.

### Apprentissage en ligne

C'est en forgeant qu'on devient forgeron. C'est le flux des données qui est traité, la mise à jour s'effectue au fur et à mesure de l'arrivée de nouvelles données. Ce traitement peut être réalisé à l'arrivée de chaque nouvelle donnée ou encore considérer les données par petits paquets ("mini-batches"). Ce type d'algorithme est adapté à des données qui arrivent en flux continu, des données dont l'évolution au cours du temps est rapide, des données pour lesquelles la base qu'il faudrait stocker en mémoire serait trop grande pour un traitement de type "batch". 

Ces algorithmes sont très exposés à l'arrivée soudaine de données de mauvaise qualité. Cela peut se produire par exemple lorsqu'un capteur est défaillant, ou bien encore du fait de malveillance. Pour cette raison, ces algorithmes doivent souvent être associés à une procédure de contrôle de la qualité des données entrantes (monitoring). 

## Basé sur des cas, basé sur des modèles

### Algorithme basé sur des cas

Un algorithme basé sur les cas se contente de mémoriser l'ensemble des cas mis à sa disposition pendant la phase d'apprentissage. Ensuite, la procédure la plus basique de traitement d'un cas consiste à le rechercher dans la base pour savoir si ce cas a déjà été observé afin de produire le résultat correspondant. 

La capacité de généralisation d'une telle approche est bien évidemment nulle. Pour généraliser un tant soit peu, cette comparaison peut être assouplie en utilisant une mesure de similarité entre le nouveau cas et les cas existants. 

### Algorithme basé sur un modèle

Un algorithme basé sur un modèle construit, à partir des cas mis à sa disposition, un modèle des données. Une fois ce modèle appris, il l'utilise pour prédire la solution pour les nouveaux cas qui lui sont présentés.

Le processus se décompose en plusieurs étapes : étude des données, sélection d'un modèle, entraînement de ce modèle à partir des données d'apprentissage, et finalement la phase d'inférence qui consiste à utiliser le modèle appris sur de nouvelles données.

# Ecueils classiques

Lorsque l'on choisit un **algorithme** pour l'entraîner sur des **données**, deux problèmes peuvent se poser immédiatement : 

1. les données sont mauvaises, 
2. l'algorithme est mauvais.

## Mauvaises données

De quelle façon les données utilisées pendant la phase d'apprentissage peuvent-elles être mauvaises ? Parmi les défauts les plus fréquents :

* Le volume de données disponibles est insuffisant.
* Les données ne sont pas représentatives.
* Les données sont de mauvaise qualité : présence de données aberrantes, présence de bruit, caractéristiques incomplètes. Dans ce cas un nettoyage préalable des données est indispensable. De fait, cette tâche occupe la majeure partie du temps d'un *data scientist*. 
* Les caractéristiques --- *features* --- ne sont pas pertinentes. La phase de sélection et d'extraction des caractéristiques pertinentes est essentielle pour le bon fonctionnement d'un algorithme d'apprentissage. 

## Mauvais algorithme

Typiquement, un algorithme peut effectuer une généralisation médiocre du fait de sa trop forte attache aux données d'apprentissage, c'est le surapprentissage. 
Le défaut opposé est le sous apprentissage qui correspond au cas dans lequel l'approximation est trop simple pour représenter suffisamment finement le lien entre les caractéristiques et le résultat (classement, prédiction d'une valeur numérique) produit.

# Importance fondamentale de l'*a priori*

De la déduction à l'induction : dans l'exemple de la détection de spam, la solution évidente qui consiste à mémoriser une liste de messages étiquetés puis à comparer un nouveau message aux éléments de cette liste ne permet évidemment aucune généralisation à des cas inconnus.

Pour aller au-delà et être à même de généraliser. Une possibilité serait d'introduire une mesure de similarité entre un nouveau message et les messages étiquetés connus en vue d'inférer la classe à laquelle le nouveau message appartient. C'est le passage du raisonnement déductif au raisonnement inductif.

Quelles caractéristiques faut-il prendre en compte ? 

Deux expériences intéressantes :

* Exemple de la superstition des pigeons (Expérience du psychologue Skinner, 1947). Dans une cage, on place des pigeons avec un grand nombre de jouets différents à leur disposition. En haut de la cage, un distributeur de graines s'active à des instants aléatoires. Les pigeons sont ainsi amenés à faire une association trompeuse entre le fait qu'il joue avec un jouet et le fait que des graines tombent. Petit à petit, le pigeon se concentre sur un seul jouet qu'il a associé au fait que des graines tombent. 

* Dans une autre expérience (Garcia, 1996) menée avec des rats, des aliments d'aspect, de goût et d'odeur habituels sont mis à la disposition d'un rat. Sans aucune différence sur ces critères, certains des aliments sont "empoisonnés". Mais au moment où un rat s'approche d'un mauvais aliment, une sonnette retentit. Les rats ne font jamais d'association entre le bruit produit par la sonnette et le fait que l'aliment est empoisonné : cela est dû au fait que le son ne fait pas partie des caractéristiques pertinentes pour le rat quant à la sélection d'un bon aliment.

De ces deux expériences découle la question de savoir quels sont les critères pertinents à prendre en compte pour une prise de décision efficace. Faudrait-il prêter attention à tout ? Evidemment non, car cela reviendrait à traiter tous les cas de la base d'apprentissage comme des cas particuliers. Associer le résultat au nom du voisin de table, la météo du jour ou l'âge du capitaine conduit à des résultats de prédéction aléatoires. 

Ces quelques exemples révèlent l'importance fondamentale de l'*a priori*:

* Lorsque peu d'information *a priori* est disponible, beaucoup de données sont nécessaires à l'apprentissage. 
* Au contraire lorsque l'on dispose d'énormément d'information *a priori*, peu de données sont nécessaires. Il se peut même qu'aucune donnée ne soit nécessaire, c'est typiquement le cas des systèmes experts : ces systèmes prennent leurs décisions uniquement en fonction de règles déterminées *a priori* et n'ont besoin d'aucune donnée pour apprendre.

# Pourquoi a-t-on besoin d'algorithme de ML

* **Complexité**. Certaines tâches que nous savons mener à bien s'avèrent trop complexes à programmer. Même si nous pouvons reconnaître un spam au premier coup d'œil, il est difficile d'expliciter les règles qui nous ont amenés à prendre la décision. Deux autres exemples classiques dans cette catégorie sont la conduite automatique ou bien encore la reconnaissance vocale. 
* **Volumes**. Pourquoi ne pas utiliser des humains ? Certaines taches font appel à des volumes de données qui dépassent les capacités humaines : exemple du placement de publicité ciblée, des données génétiques. 
* **Adaptivité**. Un programme ML peut s'adapter à un environnement changeant. L'utilisateur tague des messages en tant que SPAM, corrige le texte produit par reconnaissance vocale, corrige la reconnaissance d'écriture manuscrite. 


# Liens avec d'autres champs disciplinaires

**IA**. Le ML tombe dans le champ de l'*Intelligence Artificielle*. Ce terme, consacré par l'usage, est peut-être mal choisi pour au moins deux raisons : 
* Un algorithme peut aller au-delà de ce que les hommes peuvent faire, il n'a pas à se limiter à imiter.
* Un algorithme sera certainement incapable d'effectuer certaines taches que font les humains.

**Algorithmes et complexité**. Beaucoup d'algorithmes prometteurs ne peuvent pas être utilisés du fait de leur complexité.

**Statistiques** avec des différences importantes : 
-- Partie algorithmique des statistiques, études et algorithmes indépendants des distributions : on ne sait pas par quelle loi les données sont générées, il faut des algorithmes capables de fonctionner sans connaître la distribution des données. 
-- Echantillons de taille finie. Des résultats asymptotiques classiques sont insuffisants, il faut plus de garanties pour des échantillons de taille finie.

* Algèbre linéaire, Combinatoire, Optimisation. 




# Modèle supervisé basique

Le problème consiste à associer une étiquette à des éléments définis par leurs caractéristiques appartenant à un ensemble arbitraire, la règle d'association est apprise à partir d'une base d'apprentissage (un échantillon). 

Quelques exemples : 

* des images de chiens et de chats doivent être classées en deux catégories et l'on dispose d'une certaine base de données déjà classées, 
* des images qui représentent plusieurs types de fruits, 
* des ECG de coeur sains et de coeurs malades, etc.

## Ingrédients

### Vecteurs de caractéristiques

$\mathcal{X}$ est l'ensemble des états auxquels on souhaite associer une étiquette. 

Chacune de ces données peut être représentée par un vecteur, les composantes de ce vecteur sont ses caractéristiques (features). Il est important de noter que les caractéristiques ne capturent pas toutes les propriétés
de l'objet considéré, le choix et l'extraction de caractéristiques pertinentes quant à l'opération de classification (ou de régression) considérée sont deux étapes qui influent fortement les performances des algorithmes puisque c'est à partir de ces seules caractéristiques que la décision sera prise.

### Etiquettes

$\mathcal{Y}$ est l'ensemble des étiquettes possibles (aussi appelées labels). 

Lorsque le problème de décision est binaire, les deux étiquettes seront alors appelées $0$ et $1$ (ou $+1$ et $-1$). Les étiquettes peuvent posséder un nombre d'états supérieur à deux, voire être à valeurs continues. Pour des étiquettes en nombre fini, on parle de classification ; pour une étiquette à valeurs réelles on utilise plutôt le terme
de régression. 

### Base d'apprentissage

$S$ est une base de données étiquetées, c'est la base d'apprentissage, également appelée base d'entraînement. 
$S$ est composée d'un ensemble d'instances $\mathbf{x}_i$ pour lesquelles on connaît la valeur de l'étiquette $y_{i}$, c'est-à-dire un ensemble de $m$ couple $(\mathbf{x}_{i},y_{i})$ : $$S=\left\{ (\mathbf{x}_1,y_{1}),\cdots,\mathbf{x}_{m},y_{m})\right\}$$

Ce sont les seules données auxquelles l'algorithme d'apprentissage a accès. La restriction $\left. S\right|_{\mathbf{x}}$ de $S$ à $\mathbf{x}$ est un sous-ensemble de $\mathcal{X}$. Le cardinal de cette base d'apprentissage sera noté $\left|S\right|=$$m$.


## Génération des données et des étiquettes

### Génération des données

On suppose que les instances sont générées selon une loi de probabilité $\mathcal{D}$, sous les hypothèses suivantes : 

* La loi $\mathcal{D}$ est inconnue. Ce point est essentiel : nous ne supposons rien sur la loi $\mathcal{D}$, elle est *a priori* quelconque. 
* L'échantillon est obtenu par des tirages i.i.d. : indépendants et identiquement distribués selon la loi $\mathcal{D}$ (tirages avec remise). 

### Génération des étiquettes

On suppose que l'étiquetage est déterminé par une fonction $f\in\mathcal{H}$, de sorte que, pour toutes les instances de $\mathcal{X}$, l'étiquette est une fonction (déterministe) de cette instance. 

Cette hypothèse est très forte pour deux raisons : 

1. On suppose qu'une telle fonction existe, ce qui n'est généralement pas réaliste,
2. On suppose que cette fonction appartient à $\mathcal{H}$. 

L'objectif de l'algorithme d'apprentissage est justement de trouver, ou tout au moins d'approcher, cette fonction inconnue $f$. 

## Classifieur (ou prédicteur, ou hypothèse)

Un algorithme d'apprentissage prend comme entrée une base d'entrainement $S$ et fournit en sortie une règle de prédiction $h_S$, c'est-à-dire une fonction $h$, qui à toute observation $\mathbf{x}\in\mathcal{X}$ fait correspondre une étiquette $h(\mathbf{x})\in\mathcal{Y}$.

$$
S \rightarrow h_S:\mathcal{X}\rightarrow\mathcal{Y}
$$

Cette fonction est également appelée un prédicteur, un classifieur ou une hypothèse.

Le choix de la classe des fonctions autorisées jouera un rôle important dans la suite : par exemple, en classification binaire, pour $\mathcal{\left|X\right|<+\infty}$, le choix le plus riche consiste à considérer les $2^{\left|\mathcal{X}\right|}$ fonctions sur $\mathcal{X}$ à valeurs binaires ; malheureusement, ce choix est le plus souvent inadéquat car il conduit à du surapprentissage et il s'avère préférable de se restreindre à un petit sous-ensemble de prédicteurs $\mathcal{H}\subset\mathcal{Y^{\mathcal{X}}}$. 

## Mesure de performance : risques

On définit une erreur par le fait que le prédicteur n'associe pas la bonne étiquette $y$ à une donnée $\mathbf{x}$, c'est-à-dire que la donnée prédite n'est pas $f(\mathbf{x})$.

La probabilité d'erreur de prédiction (de classification) est ainsi la probabilité pour que l'étiquette prédite diffère de $f(\mathbf{x})$.

### Risque

#### Le risque $0/1$ 

Si $\mathbf{x}$ est échantillonné selon $\mathcal{D}$, la probabilité d'erreur de classification $P_e$ pour un classifieur $h$, qui dépend de la loi $\mathcal{D}$ et de la fonction d'étiquetage $f$, est définie par :

$$
P_e = 
%\mathcal{L}_{\mathcal{D},f}(h) =
\mathcal{D} \left( h(\mathbf{x}) \neq f(\mathbf{x}) \right)
$$

C'est la probabilité pour que l'étiquette prédite $h\left(\mathbf{x}\right)$ diffère de la véritable étiquette $f\left(\mathbf{x}\right)$.

Cette probabilité d'erreur est une mesure possible du risque de mauvaise classification, ce risque est appelé risque $0/1$.


#### Réécriture du risque $0/1$ comme espérance d'une fonction de perte. 

La probabilité de l'ensemble $\left\{ h(\mathbf{x}) \neq f(\mathbf{x}) \right\}$ est égale à l'espérance de sa fonction indicatrice, ainsi le risque du classifieur $h$ peut être écrit comme

$$
R(h) = \mathcal{D} \left\{ h(\mathbf{X}) \neq f(\mathbf{X}) \right\} 
= \mathbb{E} \left( 1_{h(\mathbf{X}) \neq f(\mathbf{X})} \right)
$$

Le risque est ainsi vu comme l'espérance d'une fonction de perte (loss function), ici $1_{h(\mathbf{\cdot}) \neq f(\mathbf{\cdot})}$. 

Ce risque vrai, aussi appelé risque de généralisation, est un risque théorique qui n'est pas directement accessible au niveau expérimental.





# Minimisation du Risque Empirique (MRE)

Ainsi, un algorithme d'apprentissage $\mathcal{A}$ prend en entrée une base de donnée étiquetée $\mathcal{S}$ pour produire en sortie un prédicteur $h$ dont le risque doit être aussi faible que possible. 

Le risque n'étant pas accessible, une possibilité pratique consiste à l'estimer en calculant un risque empirique, c'est-à-dire un risque estimé sur la seule base des données étiquetées mises à disposition de l'algorithme d'apprentissage $\mathcal{A}$.

## Risque empirique 

En utilisant l'estimateur de la moyenne empirique pour approcher l'espérance, le  risque peut être approché par un rique empirique qui se formule de la manière suivante :
$$
\hat{R}\left(h\right)= \frac{1}{m} 
\left| x_{i}\in S: h(x_{i}) \neq f(x_{i}) \right| 
= \frac 1m \sum_{i=1}^m 1_{h(\mathbf{x_i}) \neq f(\mathbf{x_i})}
$$

## Minimisation du risque empirique 

On cherche alors à minimiser ce risque empirique en espérant que le prédicteur ainsi obtenu aura de bonnes performances sur de nouvelles données, c'est-à-dire sur des données qui ne font pas partie de la base d'apprentissage $\mathcal{S}$. 

### La minimisation du risque empirique peut mal tourner

Il peut arriver, si l'on n'y prend garde, que la minimisation du risque empirique conduise à un risque de généralisation très fort. 

Pour illustrer ce point, prenons l'exemple du prédicteur suivant :

$$
h_{S}(\mathbf{x}_{i})=
\left\{ 
\begin{array}{c}
    y_{i} \mbox{ pour } \mathbf{x}_{i} \in S \\
    0\,\mbox{sinon}
\end{array}
\right.
$$

Ce prédicteur est parfait sur la base d'apprentissage puisque son risque empirique sur $S$ est nul quel que soit l'échantillon $S$.

Par contre, la valeur prédite sera toujours égale à $0$ pour de nouvelles données, c'est-à-dire pour des exemples qui ne font pas partie de ceux utilisés pour l'apprentissage. Le prédicteur colle trop aux données utilisées pour apprendre et se trouve dans l'incapacité de généraliser à de nouveaux cas. 

Ce problème est appelé surapprentissage.

### Régularisation de la minimisation du risque empirique

Sans abandonner la procédure de minimisation du risque empirique, le surapprentissage doit être évité autant que faire se peut. Une manière de le limiter consiste à restreindre le choix des prédicteurs $h$ à un ensemble $\mathcal{H}$. En d'autres termes : 

* le problème doit être régularisé en supposant $h\in\mathcal{H}$, où $\mathcal{H}$ est un espace de fonctions à définir *a priori* (c'est-à-dire avant de voir les données) 
* le minimiseur du risque empirique minimum doit être évalué sur $\mathcal{H}$ 

Selon cette procédure, le prédicteur estimé est défini par MRE régularisée\index{MRE régularisée} : 
$$
h_{S}=\arg\min_{h\in\mathcal{H}}L_{S}\left(h\right)
$$




# Apprentissage au sens PAC

Nous donnons ici quelques éléments à propos de l'approche dite probablement approximativement correcte. Bien que théorique, cette approche permet de mettre en lumière des points fondamentaux importants en pratique. 

La classe $\mathcal{H}$ peut être apprise au sens PAC (Probablement Approximativement Correct) signifie que s'il existe une fonction $m_{\mathcal{H}}\left(\epsilon,\delta\right):\left(0,1\right)\rightarrow\mathbb{N}$ et un algorithme $\mathcal{A}$ tels que pour tout $\epsilon,\delta>0$, pour toute distribution $\mathcal{D}$ sur $\mathcal{X}$ et toute fonction d'étiquetage $f:\mathcal{X}\rightarrow\mathcal{Y}$
<!--- #, si l'hypothèse de réalisabilité est vérifiée (par rapport à $\mathcal{H}$, $\mathcal{D}$ et $f$) -->

alors

un algorithme de minimisation du risque empirique utilisant un nombre d'exemples $m\geq m_{\mathcal{H}}\left(\epsilon,\delta\right)$ tirés de manière i.i.d. selon la distribution $\mathcal{D}$, donne un prédicteur $h$ tel que $\mathcal{L}_{\mathcal{D},f}\left(h\right)<\epsilon$ avec probabilité supérieure à $1-\delta$.

Pour exprimer le fait qu'une classe peut être apprise au sens PAC, nous dirons simplement que cette classe est PAC.

Cela met en évidence deux limitations : probablement (avec une probabilité supérieure à $1-\delta$) le prédicteur calculé est approximativement correct, c'est-à-dire que sa précision est meilleure que $\epsilon$. 

Ces deux aspects, "probablement correct" et "approximativement correct" sont inévitables car

* L'échantillon $\mathcal{S}$ peut être non représentatif, par exemple si l'on tire toujours le même cas (les tirages qui construisent l'échantillon sont i.i.d., c'est-à-dire avec remise).
* L'échantillon $\mathcal{S}$ peut par exemple être trop petit pour capturer certains détails du problème (distribution et fonction d'étiquetage).

<!--- La fonction $m_{\mathcal{H}}\left(\epsilon,\delta\right)$ n'est pas unique, la complexité de l'échantillon qui est nécessaire pour apprendre est la plus petite fonction $m_{\mathcal{H}}\left(\epsilon,\delta\right)$. -->

<!--- ## Apprentissage PAC d'une classe finie-->


## L'apprentissage n'est pas toujours possible

Seules certaines classes peut être apprises au sens PAC. Il est important de noter que l'apprentissage n'est pas toujours possible. 

Résultat fondamental de l'apprentissage : lorsque la dimension de Vapnik-Chervonenkis est infinie, l'apprentissage est impossible.

Lorsque la dimension de Vapnik-Chervonenkis est finie, l'apprentissage est possible et tout fonctionne : une classe $\mathcal{H}$ est PAC si et seulement si sa dimension Vapnik-Chervonenkis est finie.

Les classes finies sont de dimension de Vapnik-Chervonenkis finie et peut être apprises au sens PAC. 



## No free lunch

Il n'existe pas de meilleur algorithme universel. 
<!---
Le problème étant caractérisé par la distribution $\mathcal{D},$ existe-t-il un prédicteur $h:\mathcal{X\rightarrow\mathcal{Y}}$ dont le risque est faible, c'est-à-dire existe-t-il un algorithme $\mathcal{A}$ et une valeur minimale de $m$ tels que $\mathcal{A}\left(S\right)$ a un risque faible pour $\left|S\right|>m$. Le théorème no free lunch apporte une réponse à cette question.

<!---
Pour tout classifieur binaire (algorithme $\mathcal{A}$ prenant en entrée $S$ et utilisant le coût $0-1$) et pour $m<\left|\mathcal{X}\right|/2$,
il existe une distribution $\mathcal{D}$ sur $\mathcal{X}\times\{0;1\}$ telle que

i) $\exists f:\mathcal{X}\rightarrow\{ 0;1\}$ avec $L_{\mathcal{D}}\left(f\right)=0$

ii) $Pr_{S\thicksim\mathcal{D}^{m}}\left[L_{\mathcal{D}}\left(\mathcal{A}\left(S\right)\right)\geq\frac{1}{8}\right]\geq\frac{1}{7}$

Un corollaire immédiat est qu'une classe infinie ne peut pas être PAC (Pour $\mathcal{H}$ l'ensemble des fonctions de $\mathcal{X}\rightarrow\left\{ 0;1\right\} $)

Preuve : pas si facile
-->

# Compromis biais variance

L'une des façons de réduire le risque de surapprentissage a été de réduire la classe $\mathcal{H}$ des prédicteurs possibles. Cette réduction correspond à la prise en compte d'une connaissance 
*à priori* quant au problème à résoudre. 

Est-il vraiment nécessaire d'imposer un tel \textit{a priori}  ou au contraire serait-il possible de construire des algorithmes d'apprentissage universels ?


## Décomposition biais - variance

Le risque peut se décomposer en une somme de deux termes significatifs : 
$$
R_{\mathcal{D}}\left(h_{S}\right)
=\min_{h\in\mathcal{H}}R_{\mathcal{D}}\left(h\right)
+\left[R_{\mathcal{D}}\left(h_{S}\right)-\min_{h\in\mathcal{H}}R_{\mathcal{D}}\left(h\right)\right]
$$

Interprétation de ces deux termes : 

- $\min_{h\in\mathcal{H}}R_{\mathcal{D}}\left(h\right)$ est le risque minimum qu'il est possible d'obtenir sur la classe $\mathcal{H}$. Ce terme est indépendant de la taille de $m$ de la base d'apprentissage, il dépend seulement de la taille $\left|\mathcal{H}\right|$ de la classe $\mathcal{H}$. C'est une erreur d'approximation qui dépend de la pertinence et de la taille de la famille de prédicteurs $\mathcal{H}$. Cette erreur est aussi appelée biais d'induction. 

- $R_{\mathcal{D}}\left(h_{S}\right)-\min_{h\in\mathcal{H}}R_{\mathcal{D}}\left(h\right)$ est l'écart entre le risque de la solution MRE par rapport à la solution optimale dans $\mathcal{H}$. Ce terme est une erreur d'estimation : la solution obtenue par minimisation du risque empirique dépend des exemples tirés selon la loi $\mathcal{D}$, c'est une variable aléatoire dont les fluctuations dépendent de $m$ et de la taille de $\mathcal{H}$. 
-- La variance de ce terme est d'autant plus petite que $m$ est grand, 
-- Elle augmente en $\log\left|\mathcal{H}\right|$ pour $\mathcal{\left|H\right|<+\infty}$. 

La question est de trouver un bon compromis entre ces deux termes contradictoires : $\mathcal{H}$ suffisamment grand pour que l'approximation soit bonne et suffisamment petit pour que le terme de fluctuation reste faible. 

<!---
## Performance

L'approche classique pour mesurer la performance consiste à étudier, pour une distribution de probabilité donnée, le comportement asymptotique ($m\rightarrow\infty$ ) d'un estimateur : consistance et vitesse de convergence le plus souvent. 

En apprentissage, la question est plutôt d'étudier le comportement pour des échantillons de taille finie et ce en supposant le moins de choses possibles sur la distribution.

-->
<!---
Soient $\mathcal{X}$ un domaine, $\mathcal{Y}=\left\{0,1\right\}$ deux étiquettes, $\mathcal{H}$ un ensemble fini d'hypothèses (fonctions de $\mathcal{X}$ vers $\mathcal{Y}$),  $\mathcal{S}$ un échantillon (obtenu par tirages i.i.d. selon la loi $\mathcal{D}$ sur $\mathcal{X}$), $f\in\mathcal{H}$ une fonction d'étiquetage, alors la minimisation du risque empirique sur $\mathcal{S}$ fournit un prédicteur $h_{S}$ dont le risque de généralisation est faible pour peu que la taille de la base d'apprentissage soit de taille suffisante. 

Une différence importante avec l'approche statistique classique et que, ici, la fonction $h$ est choisie à partir d'un ensemble $S$ de données, les données de la base d'apprentissage. Seul l'espace $\mathcal{{H}}$ auquel cette fonction appartient est fixé a priori. A contrario, en statistique classique, la fonction (hypothèse) est fixée avant de voir les données, puis cette hypothèse est testée.
-->

<!---
#### Preuve

Notons $\mathcal{H}_{B}$ l'ensemble des mauvais prédicteurs (qui ne respectent pas la contrainte de précision $\epsilon$) $$
\mathcal{H}_{B}=\left\{ h\in\mathcal{H}:\mathcal{L}_{\mathcal{D},f}\left(h\right)>\epsilon\right\}$$ 

Les échantillons $\mathcal{S}$ qui posent problème sont tels que $\left\{ \mathcal{S}:\mathcal{L}_{\mathcal{D},f}\left(h_{S}\right)>\epsilon\right\} $ : sur ces échantillons, la minimisation du risque empirique donne un résultat $h_{S}$ dont le risque a une précision moins bonne que la précision $\epsilon$ requise.

La question est de majorer la probabilité de cet ensemble, c'est-à-dire la probabilité de tirer un échantillon qui donne un prédicteur dont le risque est tel que $\mathcal{L}_{\mathcal{D},f}\left(h_{S}\right)>\epsilon$.

Les échantillons trompeurs $\mathcal{M}$ sont ceux qui, par minimisation du risque empirique, peuvent donner un mauvais prédicteur (au sens du risque de généralisation) : 
$$
\mathcal{M}=\left\{ \mathcal{S}:\exists h\in\mathcal{H}_{B}:\mathcal{L}_{S}\left(h\right)=0\right\} 
$$
Les échantillons $\mathcal{S}$ qui posent problème forment un sous-ensemble de $\mathcal{M}$ : $$
\left\{ \mathcal{S}:\mathcal{L}_{\mathcal{D},f}\left(h_{S}\right)>\epsilon\right\} \subseteq\mathcal{M} $$
Seulement un sous-ensemble en effet car il peut exister un mauvais prédicteur qui n'a pas été choisi (par minimisation du risque empirique).

Ainsi, pour majorer $$\mathcal{D}^{m}[\mathcal{S}:\mathcal{L}_{\mathcal{D},f}(h_{S})>\epsilon],$$ il suffit de majorer $\mathcal{D}^{m}[\mathcal{M}]:$$ 
$$\mathcal{D}^{m}[\mathcal{S}: \mathcal{L}_{\mathcal{D},f}(h_{S})>\epsilon]\leq\mathcal{D}^{m}[\mathcal{M}]=\mathcal{D}^{m}[\mathcal{\cup}_{h\in\mathcal{H}_{B}}\{ \mathcal{S}:\mathcal{L}_{S}(h)=0\}]$$ 
avec $$ \mathcal{D}^{m}[\mathcal{\cup}_{h\in\mathcal{H}_{B}}\{ \mathcal{S}:\mathcal{L}_{S}(h)=0\}]
\leq\sum_{h\in\mathcal{H}_{B}}\mathcal{D}^{m}[\{ \mathcal{S}:\mathcal{L}_{S}(h)=0\}]$$

Or

$$\mathcal{D}^{m}\left[\left\{ \mathcal{S}:\mathcal{L}_{S}\left(h\right)=0\right\} \right]=\mathcal{D}^{m}\left[\left\{ \mathcal{S}:h\left(\mathbf{x}_{1}\right)=f\left(\mathbf{x}_{1}\right),\cdots,h\left(\mathbf{x}_{m}\right)=f\left(\mathbf{x}_{m}\right)\right\} \right]
$$
d'où $$
\mathcal{D}^{m}\left[\left\{ \mathcal{S}:\mathcal{L}_{S}\left(h\right)=0\right\} \right]=\left(1-\epsilon\right)^{m}
$$
et finalement
$$
\mathcal{D}^{m}\left[\mathcal{\left\{ \mathcal{S}:\mathcal{L}_{\mathcal{D},f}\left(h_{S}\right)>\epsilon\right\} }\right]\leq\left|\mathcal{H}\right|\left(1-\epsilon\right)^{m}\leq\left|\mathcal{H}\right|e^{-\epsilon m}
$$
Pour $m$ suffisamment grand la probabilité pour que le prédicteur
ne respecte pas la précision $\epsilon$ est faible. $\square$
--> 


<!---
# Nouveaux ingrédients

Passons en revue les ingrédients dans ce nouveau cadre.

$\mathcal{X}$, $\mathcal{Y}$, $S$ et le prédicteur restent inchangés par rapport au cadre "apprentissage PAC" précédent. 

## Génération des données et des étiquettes

On suppose maintenant que les instances ET les étiquettes sont générées selon une certaine loi de probabilité $\mathcal{D}_{\mathbf{x},y}$ que nous noterons souvent plus simplement $\mathcal{D}_{\mathbf{}}$. 
Cette loi peut être quelconque, et surtout, elle est inconnue. 

L'échantillon étiqueté est obtenu par des tirages i.i.d. selon cette loi.

Les étiquettes ne sont plus une fonction (déterministe) des caractéristiques, elles sont générées aléatoirement avec les instances selon la loi conjointe $\mathcal{D}_{\mathbf{x},y}$. 

## Risque théorique et risque empirique

* Le risque (théorique ou risque de généralisation) doit être redéfini en prenant l'espérance par rapport à la loi conjointe $\mathcal{D}_{\mathbf{x},y}$ : $\mathcal{L}_{\mathcal{D}}\left(h\right)=\mathcal{D}_{x,y}\left(\left\{ h\left(\mathbf{x}\right)\neq y\right\} \right)=Pr_{\left(\mathbf{x},y\right)\sim\mathcal{D}}\left[h\left(\mathbf{x}\right)\neq y\right]$.
* Le risque empirique reste inchangé (à cela près que $y_{i}$ n'est plus une fonction de $\mathbf{x}_{i}$) $L_{S}\left(h\right)=\frac{1}{m}\left|\mathbf{x}_{i}\in S:h\left(\mathbf{x}_{i}\right)\neq y_{i}\right|$


## Expression des risques par des coûts moyens

Il est utile de reformuler ces risques afin de permettre une extension du formalisme dans au moins deux directions : 

1. Prédiction multi classes. Souvent le nombre de classes est supérieur à deux. Par exemple, le classement de documents en différentes catégories telles que sport, politique, international, science, culture, etc.
2. Régression : les labels sont dans $\mathbb{R}.$ Ce type de problème diffère d'une prédiction à plus de deux classes car dans le cas d'une prédiction à plusieurs classes, lorsque la classe prédite n'est pas la bonne, c'est une erreur. Dans le cas d'une régression, la manière de pénaliser les erreurs peut être différente selon l'amplitude de l'erreur.

Ces situations (et bien d'autres) peuvent être formalisées en exprimant les risques par des coûts moyens. 

Soient :

- une classe d'hypothèses $\mathcal{H}$, 

- des données générées selon une distribution inconnue $\mathcal{D}$ sur un domaine Z ,

- une fonction de coût $l:\mathcal{H}\times Z\rightarrow\mathbb{R}^{+}$ 

Le risque est défini par l'espérance du coût par rapport à la distribution $\mathcal{D}$ sur $Z$ : 

$$
\mathcal{{L}_{\mathcal{{D}}}}\left(h\right)=\mathbb{E}_{\mathbf{z}\sim\mathcal{D}}\left[l\left(h,\mathbf{z}\right)\right]
$$

Le risque empirique sur $\mathcal{S}=\left(\mathbf{z}_{1},\cdots,\mathbf{z}_{m}\right)$ est défini par :

$$
\mathcal{{L}_{\mathcal{{S}}}}\left(h\right)=\frac{1}{m}\sum_{i=1}^{m}l\left(h,\mathbf{z}_{i}\right)
$$

### Exemples de coûts

#### Coût $0-1$ \index{Coût $0-1$}- Classification

Dans le cas particulier d'une prédiction d'étiquettes dans $\mathcal{Y}$ à partir de données dans $\mathcal{X}$, on peut choisir $Z=\mathcal{X\times\mathcal{Y}}$.

En choisissant $\mathbf{z}=\left(\mathbf{x},y\right)\in Z=\mathcal{X\times\mathcal{Y}}$, la classification binaire telle que nous l'avons présentée correspond au risque $\mathcal{{L}_{\mathcal{{D}}}}\left(h\right)=\mbox{Pr}_{S\sim\mathcal{D}^{m}}\left[h(\mathbf{x})\neq y\right]$ qui est exactement l'espérance du coût (binaire) :

$$
l_{0-1}\left(h,\left(\mathbf{x},y\right)\right)=\left\{ \begin{array}{lll}
1 & \mbox{si} & h(\mathbf{x})\neq y\\
0 & \mbox{sinon}
\end{array}\right.
$$

Pour une classification à plus de deux classes, il reste possible de choisir $Z=\mathcal{X\times\mathcal{Y}}$ et $l_{0-1}$.

#### Coût quadratique\index{Coût quadratique} - Régression

Dans le cas d'une régression, on a $Z=\mathcal{X\times\mathcal{\mathbb{R}}}$.
Le choix le plus fréquent est celui du coût quadratique : 

$$
l\left(h,\left(\mathbf{x},y\right)\right)=\left(h(\mathbf{x})-y\right)^{2}
$$

D'autres choix sont possibles pour pénaliser différemment les écarts à la bonne valeur, un exemple courant est $l\left(h,\left(\mathbf{x},y\right)\right)=\left|h(\mathbf{x})-y\right|$.
La complexité numérique de l'optimisation et les performances peuvent varier fortement selon la nature de la fonction de coût. 
-->



# Prédicteur optimal de Bayes

Pour une prédiction binaire, le prédicteur optimal au sens de la probabilité d'erreur minimale est le prédicteur de Bayes :

$$
f_{\mathcal{D}}(\mathbf{x})=
\left\{
\begin{array}{c}
    1 \mbox{ pour } p(y|\mathbf{x}) > 1/2\\
    0 \mbox{ pour } p(y|\mathbf{x}) \leq 1/2
\end{array}
\right.
$$

Le meilleur choix correspond au choix de la probabilité a posteriori maximale.

S'il était possible de mettre en oeuvre le prédicteur de Bayes, le machine learning serait inutile. 
Mais évidemment, la règle de Bayes n'est pas applicable car la distribution $\mathcal{D}$ est inconnue, la seule chose qui est observable est un échantillon $\mathcal{S}$ généré par la distribution $\mathcal{D}$. 



# Modèle génératifs

Pour éviter le surapprentissage, une possibilité est de restreindre la classe des prédicteurs (cf. apprentissage PAC), une autre consiste à faire des hypothèses locales sur la distribution (cf. méthodes des plus proches voisins). 

Une troisième possibilité consiste à se placer dans une famille de lois fixée a priori, il s'agit d'une contrainte plus faible que de supposer la connaissance de la loi, la classe des lois pouvant être grande. 

Le prédicteur de Bayes est optimal, la classe qu'il choisit est celle dont la probabilité a posteriori est la plus grande, cette probabilité s'écrit :
$$
Pr(y=k|\mathbf{x})=
\frac{Pr(\mathbf{x}|y=k)Pr(y=k)}{\sum_{j}Pr(\mathbf{x}|y=j)Pr(y=j)}
$$

En notant

- $\pi_{k}=Pr\left(y=k\right)$, la probabilité a priori de la classe $k$,

- $p_{j}\left(\mathbf{x}\right)=Pr\left(\mathbf{x}|y=j\right)$ la distribution de probabilité des cas de la classe $j$, 

la probabilité a posteriori s'écrit :
$$ Pr(y=k|\mathbf{x})=\frac{\pi_{k}p_{k}(\mathbf{x})}{\sum_{j}\pi_{j}p_{j}(\mathbf{x})}$$

Le prédicteur de Bayes choisit la classe $k$ de probabilité a posteriori maximale, il s'appuie sur la connaissance de la loi des données, raison pour laquelle il n'est pas directement utilisable en apprentissage. 

Une possibilité intéressante en apprentissage consiste à se placer dans une famille de lois fixée a priori.


Une manière d'assurer la régularisation du problème consiste à supposer que les différentes classes sont distribuées selon des lois choisies a priori. 

Un choix courant consiste à supposer ces lois normales et à procéder à une estimation de leurs paramètres : supposons donc que les $p_{k}\left(\mathbf{x}\right)$ suivent des lois normales de moyennes $\mathbf{\mu}_{k}$ et de covariance
$\mathbf{\Sigma}_{k}$ c'est-à-dire que la densité de probabilité
de $\mathbf{x}$ pour la classe $k$ est de la forme 
$$
p_{k}\left(\mathbf{x}\right)=\frac{1}{\left(2\pi\right)^{d/2}\left|\mathbf{\Sigma}_{k}\right|^{1/2}}\exp\left[-\frac{1}{2}\left(\mathbf{x}-\mathbf{\mu}_{k}\right)^{T}\mathbf{\Sigma}_{k}^{-1}\left(\mathbf{x}-\mathbf{\mu}_{k}\right)\right]
$$

La mise en oeuvre d'un prédicteur proche du prédicteur de Bayes suppose que $p_{k}\left(\mathbf{x}\right)$ et $\pi_{k}$ soient estimés à partir de la base d'apprentissage $S$. Ici, les paramètres à estimer sont $\pi_{k}$, $\mathbf{\mu}_{k}$ et $\mathbf{\Sigma}_{k}$, notons $\hat{\pi}_{k}$, $\mathbf{\hat{\mu}}_{k}$ et $\mathbf{\hat{\Sigma}}_{k}$ leurs estimateurs. 

La règle de décision devient :
$$
\hat{k}=\arg\max_{k\in\mathcal{Y}}\delta_{k}\left(\mathbf{x}\right)
$$
avec 
\begin{align*}
\delta_{k}\left(\mathbf{x}\right) & =\log Pr\left(y=k|\mathbf{x};\hat{\pi}_{k},\mathbf{\hat{\mu}}_{k},\mathbf{\hat{\Sigma}}_{k}\right)\\
 & =-\frac{1}{2}\log\left|\mathbf{\hat{\Sigma}}_{k}\right|-\frac{1}{2}\left(\mathbf{x}-\mathbf{\hat{\mu}}_{k}\right)^{T}\mathbf{\hat{\Sigma}}_{k}^{-1}\left(\mathbf{x}-\mathbf{\hat{\mu}}_{k}\right)+\log\hat{\pi}_{k}-\frac{d}{2}\log\left(2\pi\right)
\end{align*}


## QDA

Nous supposons que les classes sont distribuées selon des lois normales, chacune des classes ayant sa propre moyenne et sa propre covariance. 

### Estimation des paramètres

Les paramètres à estimer sont $\pi_{k}$, $\mathbf{\mu}_{k}$ et $\mathbf{\Sigma}_{k}$, notons $\hat{\pi}_{k}$, $\mathbf{\hat{\mu}}_{k}$ et $\mathbf{\hat{\Sigma}}_{k}$ leurs estimateurs. 

#### Estimation de la fréquence des classes

Notons $y_{i}=k$ les $m_{k}$ cas de $S$ qui appartiennent à la classe $k$. L'estimateur empirique de la fréquence $\pi_{k}$ de chaque classe est : 
$$
\hat{\pi}_{k}=\frac{m_{k}}{m}
$$
où $m_{k}$ désigne, parmi les $m$ cas que compte $S$, le nombre de ceux qui appartiennent à la classe $k$. 

#### Estimations des moyennes des classes

L'estimateur empirique de la moyenne s'écrit : 
$$
\mathbf{\hat{\mathbf{\mu}}}_{k}=\frac{1}{m_{k}}\sum_{y_{i}=k}\mathbf{x}_{i}
$$

#### Estimation des covariances

L'estimateur empirique non biaisé (en utilisant la moyenne empirique) des covariances est :
$$
\mathbf{\hat{\mathbf{\Sigma}}}_{k}=\frac{1}{m_{k}-1}\sum_{y_{i}=k}\left(\mathbf{x}-\mathbf{\hat{\mu}}_{k}\right)\left(\mathbf{x}-\mathbf{\hat{\mu}}_{k}\right)^{T}
$$

### Frontières quadratiques de décision

La frontière de décision entre les classes $k$ et $l$ est définie par $\delta_{k}\left(\mathbf{x}\right)=\delta_{l}\left(\mathbf{x}\right)$, c'est-à-dire par l'équation quadratique :
$$
c_{k,l}+\mathbf{l}_{k,l}^{T}\mathbf{x}+\mathbf{x}^{T}\mathbf{Q}_{k,l}\mathbf{x}=0
$$
avec  $$
c_{k,l}=-\frac{1}{2}\log\frac{\left|\mathbf{\hat{\Sigma}}_{k}\right|}{\left|\mathbf{\hat{\Sigma}}_{l}\right|}+\log\frac{\hat{\pi}_{k}}{\hat{\pi}_{l}}-\frac{1}{2}\mathbf{\hat{\mu}}_{k}^{T}\mathbf{\hat{\mathbf{\Sigma}}}_{k}^{-1}\mathbf{\hat{\mu}}_{k}+\frac{1}{2}\mathbf{\hat{\mu}}_{l}^{T}\mathbf{\hat{\mathbf{\Sigma}}}_{l}^{-1}\mathbf{\hat{\mu}}_{l}
$$

$$
\mathbf{l}_{k,l}=\mathbf{\hat{\mathbf{\Sigma}}}_{k}^{-1}\mathbf{\hat{\mu}}_{k}-\mathbf{\hat{\mathbf{\Sigma}}}_{l}^{-1}\mathbf{\hat{\mu}}_{l}
$$
$$
\mathbf{Q}_{k,l}=\frac{1}{2}\left(\mathbf{\hat{\mathbf{\Sigma}}}_{l}^{-1}-\mathbf{\hat{\mathbf{\Sigma}}}_{k}^{-1}\right)
$$

Ainsi, en modélisant la distribution des classes par des lois normales de moyennes et de covariances différentes, les frontières entre classes sont quadratiques. C'est l'analyse discriminante quadratique (Quadratic Discriminant Analysis - QDA)

## LDA

Il est possible de simplifier un peu plus le problème d'estimation en contraignant davantage les lois sur chacune des classes : supposons que la covariance est la même pour toutes les classes.

### Estimation des paramètres

Les estimateurs des fréquences des classes et des moyennes restent inchangés, l'estimateur de la covariance globale est maintenant 
$$
\mathbf{\hat{\mathbf{\Sigma}}}=\frac{1}{m-K}\sum_{k=1}^{K}\sum_{y_{i}=k}\left(\mathbf{x}_{i}-\mathbf{\hat{\mu}}_{k}\right)\left(\mathbf{x}_{i}-\mathbf{\hat{\mu}}_{k}\right)^{T}
$$
où $K$ désigne le nombre de classes. 

### Frontières linéaires de décision

Les frontières sont maintenant définies par une équation linéaire : $$c_{k,l}+\mathbf{l}_{k,l}^{T}\mathbf{x}=0$$
avec $$c_{k,l}=\log\frac{\hat{\pi}_{k}}{\hat{\pi}_{l}}-\frac{1}{2}\mathbf{\hat{\mu}}_{k}^{T}\mathbf{\hat{\mathbf{\Sigma}}}^{-1}\mathbf{\hat{\mu}}_{k}+\frac{1}{2}\mathbf{\hat{\mu}}_{l}^{T}\mathbf{\hat{\mathbf{\Sigma}}}^{-1}\mathbf{\hat{\mu}}_{l}
$$ $$
\mathbf{l}_{k,l}=\mathbf{\hat{\mathbf{\Sigma}}}^{-1}\left(\mathbf{\hat{\mu}}_{k}-\mathbf{\hat{\mu}}_{l}\right)
$$
Si les paramètres étaient parfaitement estimés, les performances de cette méthode seraient inférieures à celle de la méthode QDA. Néanmoins, les paramètres étant estimés à partir des $m$ exemples que compte $S$, il est possible que les matrices de covariance soient très mal estimées lorsque le nombre d'exemples $m$ n'est pas suffisamment grand par rapport à la dimension $d$. Dans ce cas, il n'est pas évident a priori que la méthode QDA soit préférable à LDA, et ceci d'autant plus que la dimension est grande. 

### Bayes naïf

Pour simplifier encore plus, il est possible de supposer que les covariances sont diagonales. 




# Méthodes des plus proches voisins

Contrairement aux algorithmes basés sur des modèles qui utilisent la base d'apprentissage pour identifier les paramètres de leur modèle, les algorithmes de type plus proches voisins sont basés sur des cas, c'est-à-dire, sur la mémorisation de la base d'apprentissage. 

Lorsqu'un nouvel exemple est présenté à l'algorithme, cette base est utilisée pour y rechercher des cas proches afin d'associer à ce nouvel exemple une étiquette liée à celle de ces cas.

Pour être à même de mesurer cette proximité, posons une métrique $\rho$ sur $\mathcal{X}$. Pour fixer les idées, dans ce chapitre, nous supposons que $\mathcal{X}=\mathbb{R}^{d}$, dans ce cas la métrique peut typiquement être la distance euclidienne. 

Remarque sur la régularisation des méthodes de plus proches voisins :

- Les méthodes de plus proches voisins ne supposent pas qu'une classe $\mathcal{H}$ d'hypothèses est fixée a priori. 

- La recherche du meilleur prédicteur peut-être régularisée en restreignant la classe des prédicteurs possibles. Néanmoins, ce n'est pas la seule façon de formuler la régularisation. Une autre façon de procéder pourrait consister tout simplement à dire que des points proches ont des étiquettes qui doivent être proches.


## Principe

La base d'apprentissage est  $$\mathcal{S}=\left\{ \left(\mathbf{x}_{i},y_{i}\right),i=1\cdots m\right\},$$
l'exemple nouveau (hors de la base) sur lequel porte la prédiction est noté $\mathbf{x}$. Classons les cas de $\mathcal{S}$ en fonction de leur éloignement croissant de $\mathbf{x}$ : $x_{\pi_{1}\left(\mathbf{x}\right)},\cdots,x_{\pi_{m}\left(\mathbf{x}\right)}$ où $\{\pi_1(\mathbf{x}),\cdots,\pi_m(\mathbf{x})\}$ est une permutation de $1,\cdots,m$.

Considérons $V_k=\{y_{\pi_i(\mathbf{x})},i\leq k\}$ l'ensemble des $k$ plus proches voisins de $\mathbf{x}$. 

### Classification k-NN (Nearest Neighbor)

Le classifieur k-NN associe à $\mathbf{x}$ l'étiquette majoritaire dans $V_{k}$.

Exemple : pour $k=1$, $h_{S}\left(\mathbf{x}\right)=y_{\pi_{1}\left(\mathbf{x}\right)}$.

### Régression k-NN

La prédicteur calcule une moyenne des étiquettes associées aux $k$ plus proches voisins de $\mathbf{x}$ :  $$ h_{S}\left(\mathbf{x}\right)=\frac{1}{k}\sum_{i=1}^{k}y_{\pi_{i}\left(\mathbf{x}\right)}$$

Des variantes peuvent bien sûr être envisagées, par exemple :

- il est possible de pondérer les valeurs $y_{i}$ en fonction de leur distance à $\mathbf{x}$, 

- il est également possible d'utiliser n'importe quelle fonction de $\mathbf{x}_{\pi_{i}\left(\mathbf{x}\right)},y_{\pi_{i}\left(\mathbf{x}\right)},i=1\cdots k$.

<!---
### Borne

La régularisation du problème va ici être réalisée en contraignant d'une certaine façon la probabilité a posteriori $\eta\left(\mathbf{x}\right)=Pr\left(y=1|\mathbf{x}\right)$. Cette probabilité a posteriori est un sous-produit de la distribution des caractéristiques et des étiquettes. 

Rappelons que le prédicteur optimal est le prédicteur de Bayes défini par 
$$
h_{\star}\left(\mathbf{x}\right)=1{}_{\eta\left(\mathbf{x}\right)>1/2}
$$

L'hypothèse raisonnable qui consiste à supposer que des caractéristiques proches ont probablement des étiquettes proches se traduit par une hypothèse Lipschitzienne sur $\eta$ : 
$$
\forall\mathbf{x},\mathbf{x}'\in\mathcal{X},\left\Vert \eta\left(\mathbf{x}\right)-\eta\left(\mathbf{x'}\right)\right\Vert \leq c\left\Vert \mathbf{x}-\mathbf{x}'\right\Vert 
$$

Il est possible d'établir des résultats du type :

Théorème. $\mathcal{X}=[0,1]^{d},\mathcal{Y}=\{ 0,1\}$,les données sont distribuées selon une loi $\mathcal{D}$ qui est telle que $\eta$ est $c$-Lipschitzienne. 

$h_{S}$ est le classifieur du plus proche voisin. Alors

$$
\mathbb{E}_{S\sim\mathcal{D}^{m}}\left[L_{\mathcal{D}}\left(h_{S}\right)\right]\leq2L_{\mathcal{D}}\left(h_{\star}\right)+4c\sqrt{d}m^{-\frac{1}{d+1}}
$$

Asymptotiquement

$$
\mathbb{E}_{S\sim\mathcal{D}^{m}}\left[L_{\mathcal{D}}\left(h_{S}\right)\right]\rightarrow2L_{\mathcal{D}}\left(h_{\star}\right).
$$


### Malédiction de la dimension

Si l'on veut que le deuxième terme de la borne supérieure reste inférieur
à $\epsilon$, c'est-à-dire que $4c\sqrt{d}m^{-\frac{1}{d+1}}<\epsilon$,
il faut que $m$ soit suffisamment grand :
$$
m\geq\left(\frac{4c\sqrt{d}}{\epsilon}\right)^{d+1}
$$

 
Autrement dit, la taille de l'échantillon croît exponentiellement avec la dimension. Malheureusement cela ne résulte pas d'une faiblesse de la borne supérieure (qui serait peu serrée) c'est effectivement un problème fondamental. 

 -->
 

