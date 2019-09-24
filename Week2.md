# Downloading the Genbank File and Converting to .fasta
efetch -db=nucleotide -id=NC_008535.1 -format=gb>Week2.gbk
python ~/in_class_assignments/handling_seq_data/genbank_to_fasta.py Week2.gbk Week2.fasta
> These commands pull the coffee chloroplast genetic information from GenBank, 
> then convert this data to a .fasta file of all the protein transcripts.

# Counting the Protein Sequences
grep ">" Week2.fasta | wc -l
> These piped commands isolate all the lines with names via the ">" character,
> then counts how many lines are remaining; there are 85.

# Creating a List of Protein Names
grep ">" Week2.fasta | sed 's/>//' > Week2_Pro_Names.txt
> This isolates the names by the ">" character, deletes all ">" characters,
> and outputs the names into a file Week2_Pro_Names.txt

# Counting Photosystem Subunits
grep "photosystem" Week2.fasta | wc -l
> This searches all lines with "photosystem" in the name, then counts these lines.
> There are 22 subunits in this file.

# Move ATP Synthase CF1 Beta Subunit Sequence into its own .fasta File
grep -wEA1 --no-group-separator 'ATP synthase CF1 beta' Week2.fasta > ATP_synthase_CF1_beta.fasta
> This command graps all the lines containing "ATP synthase CF1 beta" and prints them
> (there was only one) along with all the linked sequence line to a new file: ATP_synthase_CF1_beta.fasta.
