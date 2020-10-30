Vous allez travailler avec 4 fichiers de sorties de séquençage : les reads en sens (forward) et en anti-sens (reverse) pour chaque banque construites (ShotGun et 3C). Vos fichiers sont nommés ainsi :

sampleX_SG_for.fastq.gz
sampleX_SG_rev.fastq.gz
sampleX_3C_for.fastq.gz
sampleX_3C_rev.fastq.gz

Avant de procéder à l'analyse ou à l'exploitation d'un ensemble de données de séquençage, il est impératif de réaliser des contrôles de qualité des séquences brutes et d'appliquer des filtres si nécessaires. Cette opération permettra de s'assurer qu'il n'y a pas de problèmes cachés dans vos données initiales et de travailler avec des séquences de bonne qualité.

créer un répertoire sur le bureau de la Machine virtuelle

> cd 

> mkdir TP_Meta3C 

toutes les lignes de commande que vous verrez s'exécuteront depuis cet emplacement

> cd  TP_Meta3C/

explorer l’aborescence

> ls –l  ligne  de  commande

visualiser vos données fastq 

> zcat  fastq/sampleX_SG_for.fastq.gz  |  head
> zcat  fastq/sampleX_SG_rev.fastq.gz  |  head
> zcat  fastq/sampleX_SG_for.fastq.gz  |  head
> zcat  fastq/sampleX_3C_rev.fastq.gz  |  head

