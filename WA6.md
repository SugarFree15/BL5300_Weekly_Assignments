# Downloading Data

wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/Unk_therm.faa

wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/HSP_prot.fasta

> These download the predicted transcripts of our unknown thermophile and query heat shock proteins, respectively.

# Making BLASTable Database of Thermophile Transcripts

makeblastdb -in Unk_therm.faa -dbtype prot -title Unk_therm

> This creates protein sequence database of our thermophile data to let us BLAST our query sequences against.

# BLAST for Heat Shock Proteins in our Unknown Thermophile

blastp -db Unk_therm.faa -query HSP_prot.fasta -out HSP_BLAST.txt -outfmt 7

> This BLASTs our queries over the predicted transcripts and outputs them into a tapped .txt file, which I copied and pasted into Excel for analysis.

# Results

> Based on the results, I would suggest about 13 known heat shock proteins to be within this organism. I took an assumption that an e-value less than 0.25 would be a suitable alignment for this classification especially since most proteins with such a score had similar %IDs above 30-40%.

> Out of my suggested 13 heat shock proteins, 4 appear to be paralogs to our query proteins. I used the Twilight Zone of Homolog curve in the class powerpoint as a reference, classifying my homologs as those in the "Safe Zone" and my paralogs as those in the "Twilight Zone" based on the comparison between the %ID and alignment length.
