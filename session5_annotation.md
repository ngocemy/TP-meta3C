Session 5 : Annotation d'un assemblage

L'annotation d'un métagénome a deux objectifs principaux : i - caractériser les différents organismes (annotation taxonomique); ii - caractériser les différentes fonctions (annotation fonctionnelle), présentes dans l'échantillon. L’annotation peut se faire soit au niveau des séquences d'ADN obtenues (cf séance 2), soit au niveau des séquences protéiques putatives. L'utilisation des séquences d'ADN est plus précise mais plus difficile car les séquences d'ADN sont plus divergentes que les séquences protéiques. La première étape va donc consister à caractériser les ORFs putatives présentes dans notre assemblage.

•	Recherche des phases ouvertes de lecture

Différents programmes existent pour rechercher de potentielles phases ouvertes de lecture (ORFs) (genemark, metagenemark, prodigal). Dans le cadre de ce TP nous utiliserons le programme prodigal qui est bien adapté aux métagénomes. Prodigal est un algorithme d'apprentissage automatique non supervisé (unsupervised machine learning). Il apprend de lui-même les propriétés du/des génome(s) à partir de la séquence elle-même, y compris le code génétique, l'utilisation du motif RBS (Ribosome Binding Site), l'utilisation du codon start ainsi que les statistiques d’utilisation des codons.

Prodigal s'utilise en ligne de commande avec les options suivantes :

o	 -a : fichier d'output où seront écrites les séquences de protéines putatives

o 	-p meta : pour les métagénomes

o 	-o : fichier d'output où seront écrites les données sur les ORFs détectées

o 	-d : fichier d'output où seront écrites les séquences des ORFs putatives (ADN)

o	 -i : fichier d'input

créer un répertoire de sortie

> mkdir  -p  annotations/sampleX/

lancer la recherche de phases ouvertes de lecture

> prodigal  -p  meta  -a  annotations/sampleX/sampleX_prot.fa  -o  annotations/sampleX/sampleX.gene  -d  annotations/sampleX/sampleX_gene.fa    -i  assemblage/assemblage_XX_500.fa  >  log_files/prodigal.log  2>&1

En vous servant des fichiers obtenus et de vos connaissances Unix (et du mémo fourni), répondez aux questions suivantes :

Qi15 : Combien de gènes putatifs détectez-vous ?

Qi16 : Quelle est la longueur moyenne des gènes détectés ?

Qi17 : Quel est le plus long gène détecté ?

Qi18 : Quel est la longueur totale des gènes détectés ?

Qi19 : Quelle est la densité en séquences codantes de votre assemblage ? cette valeur vous semble-t-elle cohérente ?

Différents outils existent afin de caractériser les ORFs putatives présentes dans un assemblage (Principalement Blast ou HMM). Dans cette partie, nous allons rechercher les gènes putatifs de résistances aux antibiotiques et comparer ces 2 outils.

•	BLAST

Concernant les bases de données de blast (protéiques ou nucléiques), elles peuvent être très générales (non-redundant nucleotide database sur NCBI) ou plus spécifiques de certains groupes ou familles de gènes (marqueurs taxonomiques, phages, gènes de résistance aux antibiotiques...). Il est également possible de réaliser soi-même sa base de données.

créer un répertoire de sortie pour les bases de données

> mkdir  -p  database/

création de la base de données

> makeblastdb  -in fasta/ARmeta-polypeptides.fa  -input_type fasta  -dbtype prot  -out database/ARmeta  >  log_files/blastdb.log  2>&1

faire le blast

> blastp  -db database/ARmeta  -query annotations/sampleX/sampleX_prot.fa  -evalue 0.0001  -outfmt 6  -out annotations/sampleX/blast_ARmeta.txt  >  log_files/blast_ARmeta.log  2>&1

•	Recherche d'homologie par "hidden Markov model" (HMM)

Un modèle de Markov caché (HMM) est un modèle statistique qui permet de modéliser une séquence cible mais en autorisant un certain degré de variabilité. Les modèles de Markov cachés sont massivement utilisés notamment en reconnaissance de formes, en intelligence artificielle, en traitement automatique du langage naturel et également pour la détection de motifs protéiques. Différents modèles sont disponibles notamment sur la base de données "Pfam" (Protein family).
Nous allons travailler avec le logiciel hmmer qui s'utilise en ligne de commande, les modèles se trouvent dans [database/]. 

Pour le seuil de la recherche de motif, nous avons les deux options suivantes :

o	 -E : au niveau de la protéine entière

o 	--domE : au niveau des domaines protéiques

lancer la détection de motifs

> hmmsearch  -E  0.0001  --domE  0.0001  database/Resfams.hmm  annotations/sampleX_prot.fa  >  annotations/sampleX/HMM_resfam.out

récupérer les séquences d'intérêt

> grep  'NODE'  annotations/sampleX/HMM_resfam.out  |  grep  'e-'  |  awk  '{print  $9}'  >  annotations/sampleX/resfam_prot.txt

Qi20 : Combien de gènes de type AMR retrouvez-vous dans votre échantillon selon l’outil utilisé ? Quel est le nombre de gènes AMR spécifiquement détecté par chaque outil ?

•	Programmes spécifiques

Il existe un grand nombre de programmes dédiés à la caractérisation de certains types d’éléments génétiques tel que les transposons, les plasmides, les phages. Ces programmes s’appuient généralement sur des séquences protéiques, des modèles HMM et d’autres spécificités des éléments étudiés pour caractériser des familles d’éléments bien spécifiques.

Recherches de phages : VIRSorter, VIBRANT …

Recherches de plasmides : PlasmidFinder, Plasflow …

Vous trouverez dans le dossier annotations/ les fichiers de sorties de 2 programmes spécifiques (VIRSorter et PlasFlow). Jetez y un oeil, vous pourrez en avoir besoin dans la suite du TP ...
