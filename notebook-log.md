Introduction:


Respiratory complex I is an essential part of the electron transport chain in aerobic cellular respiration. Aerobic cellular respiration is the primary method of chemical energy (ATP) production for the majority of organisms, only excluding prokaryotes which inhabit low-oxygen environments.

Mitochondrial NADH-ubiquinone oxidoreductase 75 kDa subunit (also known as NDUFS1) is an enzyme which serves as the largest subunit of respiratory complex I. It is located on the inner mitochondrial membrane and is crucial for oxidative phosphorylation, the process by which oxygen is consumed and ATP is produced via the movement of electrons through the electron transport chain.

I am interested in understanding the phylogenetic relationship between very similar NDUFS1 proteins encoded by the genomes of different species by constructing a phylogenetic tree for analysis. This analysis will help shed light on the evolutionary history of NDUFS1 by species. It will help us to organize these relationships for future phylogenetic research.


Setup:
# Change to relevant directory
cd Desktop

# Create a class directory
mkdir Botany563

# Create a project directory within the class directory
mkdir MyProject

# Create relevant directories for the project
mkdir data
mkdir figures
mkdir manuscript
mkdir results
mkdir scripts


Data collection:


First, I searched the NIH's NCBI for the protein sequence of human (Homo sapien) NDUFS1:

>NP_004997.4 NADH-ubiquinone oxidoreductase 75 kDa subunit, mitochondrial isoform 1 precursor [Homo sapiens]
MLRIPVRKALVGLSKSPKGCVRTTATAASNLIEVFVDGQSVMVEPGTTVLQACEKVGMQIPRFCYHERLS
VAGNCRMCLVEIEKAPKVVAACAMPVMKGWNILTNSEKSKKAREGVMEFLLANHPLDCPICDQGGECDLQ
DQSMMFGNDRSRFLEGKRAVEDKNIGPLVKTIMTRCIQCTRCIRFASEIAGVDDLGTTGRGNDMQVGTYI
EKMFMSELSGNIIDICPVGALTSKPYAFTARPWETRKTESIDVMDAVGSNIVVSTRTGEVMRILPRMHED
INEEWISDKTRFAYDGLKRQRLTEPMVRNEKGLLTYTSWEDALSRVAGMLQSFQGKDVAAIAGGLVDAEA
LVALKDLLNRVDSDTLCTEEVFPTAGAGTDLRSNYLLNTTIAGVEEADVVLLVGTNPRFEAPLFNARIRK
SWLHNDLKVALIGSPVDLTYTYDHLGDSPKILQDIASGSHPFSQVLKEAKKPMVVLGSSALQRNDGAAIL
AAVSSIAQKIRMTSGVTGDWKVMNILHRIASQVAALDLGYKPGVEAIRKNPPKVLFLLGADGGCITRQDL
PKDCFIIYQGHHGDVGAPIADVILPGAAYTEKSATYVNTEGRAQQTKVAVTPPGLAREDWKIIRALSEIA
GMTLPYDTLDQVRNRLEEVSPNLVRYDDIEGANYFQQANELSKLVNQQLLADPLVPPQLTIKDFYMTDSI
SRASQTMAKCVKAVTEGAQAVEEPSIC

Next, I entered the above amino acid sequence as the query sequence on NCBI's BLASTp. I searched the standard, non-redundant protein sequences database and exluded Homo sapiens from the hits. BLASTp's algorithm parameters were kept as default, with 100 max target sequences and an expect threshold of 0.05. 


Quality control:


I will not be using a software like FastQC or Phyluce as the data I am using were uploaded to databases by other researchers who have done their own QC. Instead, I did further quality control by sifting through the resulting sequences and downloading the first 20 based on the following criteria: 

I excluded sequences from duplicate species.

I excluded 100% sequence matches.

I ordered the sequences in order of ascending E values to ensure that I download those sequences with the lowest probability of BLAST having found them similar to the reference sequence by chance instead of based on true relationships. Each downloaded sequence's E value was below 0.0.

I only included sequences which had 100% query cover to ensure that 100% of the reference sequence was used in comparison for each downloaded sequence.

The NCBI reference codes for the 20 downloaded sequences are in order of ascending E values below:

>NP_001266520.1
>PNJ73451.1
>PNI67080.1
>XP_008972488.1
>XP_003907894.1
>P0CB68.1
>Q4R6K9.1
>XP_025261308.1
>XP_010350948.1
>XP_032610702.1
>XP_023075176.1
>XP_030659807.1
>XP_011805264.1
>XP_039325526.1
>XP_033086464.1
>XP_002749725.2
>XP_032134401.1
>XP_015990567.2
>XP_011224853.1
>XP_006921444.1

# Change to the downloads directory, move the sequences file into the data directory, and change to the project directory
cd ../
cd Downloads
mv raw-sequences.txt Botany563/MyProject/data
cd Desktop/Botany563/MyProject
cd data


Multiple sequence allignment:


I will be aligning my sequences using ClustalW2 and MUSCLE with the purpose of comparing the results.

ClustalW2:

#I copy and pasted the raw-sequences.txt file into my directory for ClustalW2.
cp raw-sequences.txt ../Software/ClustalW2

# I run the command to align my sequences.
cd ../
cd Software
cd clustalw2
~/Desktop/Botany563/MyProject/Software/ClustalW2/clustalw2 -ALIGN -INFILE=raw-sequences.txt -OUTFILE=sequences-aligned-clustalw2.fasta -OUTPUT=FASTA

Output:

CLUSTAL 2.1 Multiple Sequence Alignments


Sequence format is Pearson
Sequence 1: NP_001266520.1   727 aa
Sequence 2: PNJ73451.1       741 aa
Sequence 3: PNI67080.1       741 aa
Sequence 4: XP_008972488.1   727 aa
Sequence 5: XP_003907894.1   727 aa
Sequence 6: P0CB68.1         727 aa
Sequence 7: Q4R6K9.1         727 aa
Sequence 8: XP_025261308.1   727 aa
Sequence 9: XP_010350948.1   727 aa
Sequence 10: XP_032610702.1   727 aa
Sequence 11: XP_023075176.1   727 aa
Sequence 12: XP_030659807.1   727 aa
Sequence 13: XP_011805264.1   733 aa
Sequence 14: XP_039325526.1   727 aa
Sequence 15: XP_033086464.1   727 aa
Sequence 16: XP_002749725.2   727 aa
Sequence 17: XP_032134401.1   727 aa
Sequence 18: XP_015990567.2   733 aa
Sequence 19: XP_011224853.1   727 aa
Sequence 20: XP_006921444.1   727 aa
Start of Pairwise alignments
Aligning...

Sequences (1:2) Aligned. Score:  99
Sequences (1:3) Aligned. Score:  99
Sequences (1:4) Aligned. Score:  99
Sequences (1:5) Aligned. Score:  99
Sequences (1:6) Aligned. Score:  99
Sequences (1:7) Aligned. Score:  99
Sequences (1:8) Aligned. Score:  99
Sequences (1:9) Aligned. Score:  99
Sequences (1:10) Aligned. Score:  99
Sequences (1:11) Aligned. Score:  99
Sequences (1:12) Aligned. Score:  99
Sequences (1:13) Aligned. Score:  99
Sequences (1:14) Aligned. Score:  98
Sequences (1:15) Aligned. Score:  98
Sequences (1:16) Aligned. Score:  98
Sequences (1:17) Aligned. Score:  98
Sequences (1:18) Aligned. Score:  97
Sequences (1:19) Aligned. Score:  98
Sequences (1:20) Aligned. Score:  97
Sequences (2:3) Aligned. Score:  99
Sequences (2:4) Aligned. Score:  99
Sequences (2:5) Aligned. Score:  99
Sequences (2:6) Aligned. Score:  100
Sequences (2:7) Aligned. Score:  99
Sequences (2:8) Aligned. Score:  99
Sequences (2:9) Aligned. Score:  98
Sequences (2:10) Aligned. Score:  99
Sequences (2:11) Aligned. Score:  99
Sequences (2:12) Aligned. Score:  99
Sequences (2:13) Aligned. Score:  98
Sequences (2:14) Aligned. Score:  98
Sequences (2:15) Aligned. Score:  98
Sequences (2:16) Aligned. Score:  98
Sequences (2:17) Aligned. Score:  98
Sequences (2:18) Aligned. Score:  97
Sequences (2:19) Aligned. Score:  97
Sequences (2:20) Aligned. Score:  97
Sequences (3:4) Aligned. Score:  99
Sequences (3:5) Aligned. Score:  99
Sequences (3:6) Aligned. Score:  99
Sequences (3:7) Aligned. Score:  99
Sequences (3:8) Aligned. Score:  99
Sequences (3:9) Aligned. Score:  98
Sequences (3:10) Aligned. Score:  98
Sequences (3:11) Aligned. Score:  98
Sequences (3:12) Aligned. Score:  99
Sequences (3:13) Aligned. Score:  98
Sequences (3:14) Aligned. Score:  98
Sequences (3:15) Aligned. Score:  98
Sequences (3:16) Aligned. Score:  98
Sequences (3:17) Aligned. Score:  98
Sequences (3:18) Aligned. Score:  96
Sequences (3:19) Aligned. Score:  97
Sequences (3:20) Aligned. Score:  97
Sequences (4:5) Aligned. Score:  99
Sequences (4:6) Aligned. Score:  99
Sequences (4:7) Aligned. Score:  99
Sequences (4:8) Aligned. Score:  99
Sequences (4:9) Aligned. Score:  98
Sequences (4:10) Aligned. Score:  99
Sequences (4:11) Aligned. Score:  99
Sequences (4:12) Aligned. Score:  99
Sequences (4:13) Aligned. Score:  98
Sequences (4:14) Aligned. Score:  98
Sequences (4:15) Aligned. Score:  98
Sequences (4:16) Aligned. Score:  98
Sequences (4:17) Aligned. Score:  98
Sequences (4:18) Aligned. Score:  97
Sequences (4:19) Aligned. Score:  97
Sequences (4:20) Aligned. Score:  97
Sequences (5:6) Aligned. Score:  99
Sequences (5:7) Aligned. Score:  99
Sequences (5:8) Aligned. Score:  99
Sequences (5:9) Aligned. Score:  99
Sequences (5:10) Aligned. Score:  99
Sequences (5:11) Aligned. Score:  99
Sequences (5:12) Aligned. Score:  99
Sequences (5:13) Aligned. Score:  99
Sequences (5:14) Aligned. Score:  98
Sequences (5:15) Aligned. Score:  99
Sequences (5:16) Aligned. Score:  98
Sequences (5:17) Aligned. Score:  98
Sequences (5:18) Aligned. Score:  98
Sequences (5:19) Aligned. Score:  98
Sequences (5:20) Aligned. Score:  97
Sequences (6:7) Aligned. Score:  99
Sequences (6:8) Aligned. Score:  99
Sequences (6:9) Aligned. Score:  98
Sequences (6:10) Aligned. Score:  99
Sequences (6:11) Aligned. Score:  99
Sequences (6:12) Aligned. Score:  99
Sequences (6:13) Aligned. Score:  98
Sequences (6:14) Aligned. Score:  98
Sequences (6:15) Aligned. Score:  98
Sequences (6:16) Aligned. Score:  98
Sequences (6:17) Aligned. Score:  98
Sequences (6:18) Aligned. Score:  97
Sequences (6:19) Aligned. Score:  97
Sequences (6:20) Aligned. Score:  97
Sequences (7:8) Aligned. Score:  99
Sequences (7:9) Aligned. Score:  99
Sequences (7:10) Aligned. Score:  99
Sequences (7:11) Aligned. Score:  99
Sequences (7:12) Aligned. Score:  99
Sequences (7:13) Aligned. Score:  99
Sequences (7:14) Aligned. Score:  98
Sequences (7:15) Aligned. Score:  99
Sequences (7:16) Aligned. Score:  98
Sequences (7:17) Aligned. Score:  98
Sequences (7:18) Aligned. Score:  98
Sequences (7:19) Aligned. Score:  97
Sequences (7:20) Aligned. Score:  97
Sequences (8:9) Aligned. Score:  99
Sequences (8:10) Aligned. Score:  99
Sequences (8:11) Aligned. Score:  99
Sequences (8:12) Aligned. Score:  99
Sequences (8:13) Aligned. Score:  99
Sequences (8:14) Aligned. Score:  98
Sequences (8:15) Aligned. Score:  99
Sequences (8:16) Aligned. Score:  98
Sequences (8:17) Aligned. Score:  98
Sequences (8:18) Aligned. Score:  98
Sequences (8:19) Aligned. Score:  97
Sequences (8:20) Aligned. Score:  97
Sequences (9:10) Aligned. Score:  98
Sequences (9:11) Aligned. Score:  99
Sequences (9:12) Aligned. Score:  98
Sequences (9:13) Aligned. Score:  99
Sequences (9:14) Aligned. Score:  98
Sequences (9:15) Aligned. Score:  99
Sequences (9:16) Aligned. Score:  98
Sequences (9:17) Aligned. Score:  98
Sequences (9:18) Aligned. Score:  97
Sequences (9:19) Aligned. Score:  97
Sequences (9:20) Aligned. Score:  97
Sequences (10:11) Aligned. Score:  98
Sequences (10:12) Aligned. Score:  99
Sequences (10:13) Aligned. Score:  98
Sequences (10:14) Aligned. Score:  98
Sequences (10:15) Aligned. Score:  98
Sequences (10:16) Aligned. Score:  98
Sequences (10:17) Aligned. Score:  98
Sequences (10:18) Aligned. Score:  97
Sequences (10:19) Aligned. Score:  97
Sequences (10:20) Aligned. Score:  97
Sequences (11:12) Aligned. Score:  99
Sequences (11:13) Aligned. Score:  99
Sequences (11:14) Aligned. Score:  98
Sequences (11:15) Aligned. Score:  99
Sequences (11:16) Aligned. Score:  98
Sequences (11:17) Aligned. Score:  98
Sequences (11:18) Aligned. Score:  97
Sequences (11:19) Aligned. Score:  97
Sequences (11:20) Aligned. Score:  97
Sequences (12:13) Aligned. Score:  98
Sequences (12:14) Aligned. Score:  98
Sequences (12:15) Aligned. Score:  98
Sequences (12:16) Aligned. Score:  98
Sequences (12:17) Aligned. Score:  98
Sequences (12:18) Aligned. Score:  97
Sequences (12:19) Aligned. Score:  97
Sequences (12:20) Aligned. Score:  97
Sequences (13:14) Aligned. Score:  98
Sequences (13:15) Aligned. Score:  99
Sequences (13:16) Aligned. Score:  98
Sequences (13:17) Aligned. Score:  98
Sequences (13:18) Aligned. Score:  97
Sequences (13:19) Aligned. Score:  97
Sequences (13:20) Aligned. Score:  97
Sequences (14:15) Aligned. Score:  98
Sequences (14:16) Aligned. Score:  99
Sequences (14:17) Aligned. Score:  98
Sequences (14:18) Aligned. Score:  97
Sequences (14:19) Aligned. Score:  97
Sequences (14:20) Aligned. Score:  96
Sequences (15:16) Aligned. Score:  98
Sequences (15:17) Aligned. Score:  97
Sequences (15:18) Aligned. Score:  97
Sequences (15:19) Aligned. Score:  97
Sequences (15:20) Aligned. Score:  97
Sequences (16:17) Aligned. Score:  99
Sequences (16:18) Aligned. Score:  97
Sequences (16:19) Aligned. Score:  97
Sequences (16:20) Aligned. Score:  96
Sequences (17:18) Aligned. Score:  96
Sequences (17:19) Aligned. Score:  97
Sequences (17:20) Aligned. Score:  96
Sequences (18:19) Aligned. Score:  97
Sequences (18:20) Aligned. Score:  99
Sequences (19:20) Aligned. Score:  97
Guide tree file created:   [raw-sequences.dnd]

There are 19 groups
Start of Multiple Alignment

Aligning...
Group 1: Sequences:   2      Score:15699
Group 2: Sequences:   3      Score:15709
Group 3: Sequences:   2      Score:15747
Group 4: Sequences:   3      Score:15718
Group 5: Sequences:   2      Score:15750
Group 6: Sequences:   5      Score:15758
Group 7: Sequences:   2      Score:15718
Group 8: Sequences:   7      Score:15694
Group 9: Sequences:   2      Score:15735
Group 10: Sequences:   3      Score:15743
Group 11: Sequences:   2      Score:15721
Group 12: Sequences:   3      Score:15717
Group 13: Sequences:   4      Score:15724
Group 14: Sequences:   7      Score:15719
Group 15: Sequences:  14      Score:15681
Group 16: Sequences:  17      Score:15645
Group 17: Sequences:   2      Score:15711
Group 18: Sequences:   3      Score:15619
Group 19: Sequences:  20      Score:15591
Alignment Score 839412
firstres = 1 lastres = 741
FASTA file created!

Fasta-Alignment file created    [sequences-aligned-clustalw2.fasta]

MUSCLE:

# I copy and pasted the raw-sequences.txt file into my directory for MUSCLE.
cp raw-sequences.txt ../Software/MUSCLE

# Run the following command to allign data
~/Desktop/Botany563/MyProject/Software/MUSCLE/muscle5.1.win64 -align raw-sequences.txt -output sequences-aligned-muscle.fasta

Output:

Input: 20 seqs, avg length 729, max 741

00:00 3.4Mb  CPU has 8 cores, running 8 threads
00:02 76Mb    100.0% Calc posteriors
00:02 8.9Mb   100.0% Consistency (1/2)
00:02 8.9Mb   100.0% Consistency (2/2)
00:02 9.0Mb   100.0% UPGMA5
00:03 12Mb    100.0% Refining


Distance-based method


# Installing necessary packages
install.packages("adegenet", dep=TRUE)
install.packages("phangorn", dep=TRUE)

# Loading packages
library(ape)
library(adegenet)
library(phangorn)

# Change working directory to clustalw2 directory and run commands to create distance-based tree of clustalw2 aligned data
aa_alignment_clustalw2 <- read.phyDat("sequences-aligned-clustalw2.fasta", format = "fasta", type = "AA")

# calculate distance
aa_clustalw2 <- as.AAbin(aa_alignment_clustalw2)

# create AAbin object using WAG AA model
D_aa_clustalw2 <- dist.ml(aa_clustalw2, model="WAG")

tre_aa_clustalw2 <- nj(D_aa_clustalw2)
tre_aa_clustalw2 <- ladderize(tre_aa_clustalw2)

plot(tre_aa_clustalw2, cex=.2)
title("NJ distance-based tree (aligned with ClustalW2)")

# Change working directory to MUSCLE directory and run commands to create distance-based tree of MUSCLE aligned data
aa_alignment_MUSCLE <- read.phyDat("sequences-aligned-muscle.fasta", format = "fasta", type = "AA")

# calculate distance
aa_MUSCLE <- as.AAbin(aa_alignment_MUSCLE)

# create AAbin object using WAG AA model
D_aa_MUSCLE <- dist.ml(aa_MUSCLE, model="WAG")

tre_aa_MUSCLE <- nj(D_aa_MUSCLE)
tre_aa_MUSCLE <- ladderize(tre_aa_MUSCLE)

plot(tre_aa_MUSCLE, cex=.2)
title("NJ distance-based tree (aligned with MUSCLE)")


Parsimony-based method

# Change working directory back to Clustalw2 directory and run commands to create parsimony-based tree of Clustalw2 aligned data using JTT model
aa2_clustalw2 <- as.phyDat.AAbin(aa_clustalw2)

tre.ini_aa_clustalw2 <- nj(dist.ml(aa_clustalw2, model="JTT"))
parsimony(tre.ini_aa_clustalw2, aa2_clustalw2)
# [1] 73

tre.pars_aa_clustalw2 <- optim.parsimony(tre.ini_aa_clustalw2, aa2_clustalw2)
plot(tre.pars_aa_clustalw2, cex=0.2)
# Final p-score 73 after  0 nni operations 

# Change working directory back to MUSCLE directory and run commands to create parsimony-based tree of MUSCLE aligned data using JTT model
aa2_MUSCLE <- as.phyDat.AAbin(aa_MUSCLE)

tre.ini_aa_MUSCLE <- nj(dist.ml(aa_MUSCLE, model="JTT"))
parsimony(tre.ini_aa_MUSCLE, aa2_MUSCLE)
# [1] 71

tre.pars_aa_MUSCLE <- optim.parsimony(tre.ini_aa_MUSCLE, aa2_MUSCLE)
plot(tre.pars_aa_MUSCLE, cex=0.2)
# Final p-score 71 after  0 nni operations 

# All 4 trees saved in figures directory with "tree type (distance/parsimony)-tree-alignment method (clustalw2/MUSCLE)" file name
