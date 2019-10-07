# Downloading the Reference Genome and Reads of Interest

efetch -db=nucleotide -id=CP000141.1 -format=fasta > C.hydrogenoformans_Z2901.fasta

> With this I downloaded the reference sequence of C. hydrogenoformans from NCBI and placed it into a .fasta file.

gdown.pl https://drive.google.com/file/d/1PWWO5wVRRThLBXXEZjyWZHIb9udVcnCS/edit C.ferrireducens_R1.fastq

gdown.pl https://drive.google.com/file/d/1mZFvpSIctuBihkOlQX9vhrkxng3cRmvK/edit C.ferrireducens_R2.fastq

> These commands download read 1 and 2 for C. ferrireducens from our Google Drive and place them into respective .fastq files.

# Quatily Assessment and Trimming of Raw Reads

fastqc C.ferrireducens_R1.fastq

fastqc C.ferrireducens_R2.fastq

> With these, fastqc was used to run an analysis on the quality of the reads, outputing to a new .html file.
> These raw reads have a very good condifence/quality, which we wouldn't have to trim, but I will below to remove the few calls below a Fredd score of 20 for an improved alignment.

cutadapt -q 20,20 -m 50 --max-n 0 -o C_ferr_R1.cutadapt.fastq -p C_ferr_R2.cutadapt.fastq C.ferrireducens_R1.fastq C.ferrireducens_R2.fastq

> Using cutadapt, the raw reads were trimmed with a minimum Fredd score of 20, a minimum final length of 50, no N calls allowed, and lacking any adaptor sequences since they are unknown. These trimmed sequences are exported into new .cutadapt.fastq files.

# Mapping the Raw Reads to the Reference Genome

bowtie2-build C.hydrogenoformans_Z2901.fasta C.hydro

> This indexes our reference sequence.

bowtie2 -x C.hydro -1 C_ferr_R1.cutadapt.fastq  -2 C_ferr_R2.cutadapt.fastq -S C_ferr.sam

> Now, I mapped and trimmed the reads of C. ferrireducens against the reference genome of C. hydrogenoformans and exported to a .sam file.
> After running this command, the printed output informed me that there was a 76.54% overall alignment rate between the raw reads and our reference genome, leaving 23.46% unpaired.

# Formatting the .sam for Variant Indexing

samtools view -b C_ferr.sam | samtools sort - > C_ferr.bam

samtools index C_ferr.bam

> These commands convert the .sam file into a sorted .bam file of the alignments.

samtools faidx C.hydrogenoformans_Z2901.fasta

> This indexed the reference genome in prep for the variant calling.

# Variant Calling

bcftools mpileup -f C.hydrogenoformans_Z2901.fasta C_ferr.bam | bcftools call -mv -Ob --ploidy 1 -o raw.calls.bcf

bcftools filter --exclud 'QUAL < 30' raw.calls.bcf > raw.calls.vcf

> These commands go through our alignments between species, extracting variants between the two.

bcftools view -v snps raw.calls.vcf > snp.vcf

grep -c  "PASS" snp.vcf

> With these, I filtered out the variants resulting from SNPs and counting them (NOTE: this returns the number of SNPs + 1 for an instance of "PASS" in the information at the top of the file).

# Making Consensus Genome File

bgzip raw.calls.vcf

bcftools index raw.calls.vcf.gz

> These zip and index the sorted variants in prep for consensus construction.

cat C.hydrogenoformans_Z2901.fasta | bcftools consensus raw.calls.vcf.gz > C.ferrireducens_DSMZ.fasta

> This creates a .fasta with a consensus genome assembly.
