session 7 : Analyse et validation des bins obtenus

Différentes approches permettent de valider les bins obtenus. Nous allons essayer de passer en revue différentes méthodes permettant de valider notre binning.

•	Marqueurs taxonomiques

Différents programmes existent afin de valider les bins obtenus après partitionnement d'un métagénome. Dans notre cas nous utiliserons checkM. La validation des bins avec ce programme consiste à rechercher un set de gènes bactériens (via des modèles HMM), essentiels et présents en une seule copie dans plus de 97% des génomes bactériens connus.

L’absence/présence et la multiplicité de ces marqueurs permettent ainsi d’évaluer : 

i - la complétude (mesure reliée au nombre de marqueurs au sein d'un bin par rapport au nombre attendu.

ii - la contamination (mesure reliée au nombre de marqueurs en plusieurs copies).

iii - l'hétérogénéité de souches (mesure reliée au nombre de marqueurs en plusieurs copies mais dont la séquence est proche).

Ce sont des calculs lourds qui ont été lancés sur le cluster de calcul de l'Institut Pasteur. Vous trouverez les résultats dans le dossier [checkM_output] qui contient différentes informations sur les bins identifiés.

Nous considèrerons un génome complet quand :

o	sa complétude se situe au-delà de 90%

o	sa contamination se situe en deçà de 10%


Qi32 : Combien de génome(s) reconstruit(s) et complet(s) avez-vous ?

Qi33 : A quoi peut être due la présence de bins contaminés ?

Qi34 : Avez-vous une idée de la manière d'améliorer le processus de binning ?

Vous trouverez différents fichiers correspondant au binning final sur l’espace GAIA/
Étudiez l’évolution de vos bins (taille, complétion, contamination) au cours du processus de binning (exemple ci-dessous)

•	Couverture et contenu en GC

Une autre façon de vérifier la qualité de nos bins est de regarder l’homogénéité de leur couverture et de leur contenu en GC. A l’aide du fichier contig_data.txt , générez les figures selon les modèles suivants :
 
exemple de graphiques à reproduire

Il est également possible de générer des « density plot » pour chaque bin afin de vérifier leur homogénéité.

lancement du script : 

> bash scripts/bin_analysis.sh  targeted_bin  XX/Figure/  XX/output/contig_data.txt 

•	Matrices d’interactions

A partir de n'importe quel réseau ou fichier d’alignement, il est possible de générer une matrice qui est une méthode de visualisation de graphe.

 
Matrices d’interactions de contigs avant (gauche) et après partitionnement par l’algorithme de Louvain (droite).

Pour cela, nous allons utiliser le script bins_matrix_generation.sh écrit en bash et qui permet de recouper les différentes informations et de générer une matrice non réordonnée et une matrice réordonnée des contigs de l’assemblage :

usage du script : bash matrix_generation.sh  [fichier de sortie des données de louvain]  [dossier de l’alignement]  [dossier d’output]  [taille des pixels x 5Kb]

lancement du script :

> bash bins_matrix_generation.sh  XX/binning_output/contig_data.txt  XX/alignement/XX_alignement.txt  XX/figure/  20

NB : il est également possible de générer des matrices d’interactions de chaque contig. Cela peut s’avérer très utile dans certains cas…

lancement du script : 

> bash contig_matrix_generation.sh  targeted_contig  XX/binning_output/contig_data.txt  XX/alignement/XX_alignement.txt  XX/figure/  1 

•	Arbres phylogénétiques

CheckM offre également la possibilité d’étudier le placement des bins étudiés dans « l’arbre de la vie ».

https://itol.embl.de/
Vous trouverez un dossier tree/ dans le dossier correspondant à votre échantillon, il contient les différents fichiers permettant de générer les arbres phylogénétiques des bins correspondants à votre échantillon.

