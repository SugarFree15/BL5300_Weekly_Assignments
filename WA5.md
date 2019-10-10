# Downloading the Raw Reads

gdown.pl https://drive.google.com/file/d/1AAi_-gKOmu9lEOgTJTrAtg4pHHqxessZ/edit G15_S3_L001_R1_001.fast.gz

gdown.pl https://drive.google.com/file/d/1p5ht1Tm9ZuJmqMroZWh3MbjM0qCpTAuo/edit G15_S3_L001_R1_001.fast.gz

> These commands pull the zipped .fastq files for the forward and reverse reads of this sequencing run off of our Google Drive and onto Colossus.

# Quality Filtering

cutadapt -q 20,20 -m 50 --max-n 0 -o G15_S3_L001_R1_001.cutadapt.fastq -p G15_S3_L001_R2_001.cutadapt.fastq G15_S3_L001_R1_001.fastq.gz G15_S3_L001_R2_001.fastq.gz

> This trims the raw reads from both runs according to a minimum Fredd score of 20, minimum final length of 50 bp, and no "N" calls allowed, depositing the new sequences in new .fastq files.

# De Novo Assembly

conda activate de_novo

spades.py -k 21,51,71,91,111,127 --careful --pe1-1 G15_S3_L001_R1_001.cutadapt.fastq --pe1-2 G15_S3_L001_R2_001.cutadapt.fastq -o G15_spades_output

> These first create a region we can perform SPAdes in, then runs SPAdes to make de bruijn graphs at various k-mer lengths (21, 51, 71, 91, 111, and 127) and create a concensus de novo assembly in a new directory.

# Assembly Quality Assessment

quast G15_spades_output/contigs.fasta

> This runs our concensus contigs through quast to assess their quality and output an .html file of the report. 
