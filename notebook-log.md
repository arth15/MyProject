# Introduction:


Respiratory complex I is an essential part of the electron transport chain in aerobic cellular respiration. Aerobic cellular respiration is the primary method of chemical energy (ATP) production for the majority of organisms, only excluding prokaryotes which inhabit low-oxygen environments.

Mitochondrial NADH-ubiquinone oxidoreductase 75 kDa subunit (also known as NDUFS1) is an enzyme which serves as the largest subunit of respiratory complex I. It is located on the inner mitochondrial membrane and is crucial for oxidative phosphorylation, the process by which oxygen is consumed and ATP is produced via the movement of electrons through the electron transport chain.

I am interested in understanding the phylogenetic relationship between very similar NDUFS1 proteins encoded by the genomes of different species by constructing a phylogenetic tree for analysis. This analysis will help shed light on the evolutionary history of NDUFS1 by species. It will help us to organize these relationships for future phylogenetic research.


# Setup:


##### Change to relevant directory
```
cd Desktop
```

##### Create a class directory
```
mkdir Botany563
```

##### Create a project directory within the class directory
```
mkdir MyProject
```

##### Create relevant directories for the project
```
mkdir data
mkdir figures
mkdir manuscript
mkdir results
mkdir scripts
```

# Data collection:


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


# Quality control:


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

##### Change to the downloads directory, move the sequences file into the data directory, and change to the project directory
```
cd ../
cd Downloads
mv raw-sequences.txt Botany563/MyProject/data
cd Desktop/Botany563/MyProject
cd data
```


# Multiple sequence allignment:


I will be aligning my sequences using ClustalW2 and MUSCLE with the purpose of comparing the results.

### ClustalW2

##### I copy and pasted the raw-sequences.txt file into my directory for ClustalW2.
```
cp raw-sequences.txt ../Software/ClustalW2
```

##### I run the command to align my sequences.
```
cd ../
cd Software
cd clustalw2
~/Desktop/Botany563/MyProject/Software/ClustalW2/clustalw2 -ALIGN -INFILE=raw-sequences.txt -OUTFILE=sequences-aligned-clustalw2.fasta -OUTPUT=FASTA
```
Output:

>CLUSTAL 2.1 Multiple Sequence Alignments


>Sequence format is Pearson
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

>Sequences (1:2) Aligned. Score:  99
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

>There are 19 groups
>Start of Multiple Alignment

>Aligning...
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

>Fasta-Alignment file created    [sequences-aligned-clustalw2.fasta]

### MUSCLE

##### I copy and pasted the raw-sequences.txt file into my directory for MUSCLE and change to that directory.
```
cp raw-sequences.txt ../Software/MUSCLE
cd ../MUSCLE
```

##### Run the following command to allign data
```
~/Desktop/Botany563/MyProject/Software/MUSCLE/muscle5.1.win64 -align raw-sequences.txt -output sequences-aligned-muscle.fasta
```

Output:

>Input: 20 seqs, avg length 729, max 741

>00:00 3.4Mb  CPU has 8 cores, running 8 threads
00:02 76Mb    100.0% Calc posteriors
00:02 8.9Mb   100.0% Consistency (1/2)
00:02 8.9Mb   100.0% Consistency (2/2)
00:02 9.0Mb   100.0% UPGMA5
00:03 12Mb    100.0% Refining


# Distance-based method


##### Installing necessary packages
```
install.packages("adegenet", dep=TRUE)
install.packages("phangorn", dep=TRUE)
```

##### Loading packages
```
library(ape)
library(adegenet)
library(phangorn)
```

##### Change working directory to clustalw2 directory and run commands to create distance-based tree of clustalw2 aligned data
```
cd ../ClustalW2
aa_alignment_clustalw2 <- read.phyDat("sequences-aligned-clustalw2.fasta", format = "fasta", type = "AA")
```

##### calculate distance
```
aa_clustalw2 <- as.AAbin(aa_alignment_clustalw2)
```

##### create AAbin object using WAG AA model
```
D_aa_clustalw2 <- dist.ml(aa_clustalw2, model="WAG")

tre_aa_clustalw2 <- nj(D_aa_clustalw2)
tre_aa_clustalw2 <- ladderize(tre_aa_clustalw2)

plot(tre_aa_clustalw2, cex=.2)
title("NJ distance-based tree (aligned with ClustalW2)")
```

##### Change working directory to MUSCLE directory and run commands to create distance-based tree of MUSCLE aligned data
```
cd ../MUSCLE
aa_alignment_MUSCLE <- read.phyDat("sequences-aligned-muscle.fasta", format = "fasta", type = "AA")
```

##### calculate distance
```
aa_MUSCLE <- as.AAbin(aa_alignment_MUSCLE)
```

##### create AAbin object using WAG AA model
```
D_aa_MUSCLE <- dist.ml(aa_MUSCLE, model="WAG")

tre_aa_MUSCLE <- nj(D_aa_MUSCLE)
tre_aa_MUSCLE <- ladderize(tre_aa_MUSCLE)

plot(tre_aa_MUSCLE, cex=.2)
title("NJ distance-based tree (aligned with MUSCLE)")
```

# Parsimony-based method

##### Change working directory back to Clustalw2 directory and run commands to create parsimony-based tree of Clustalw2 aligned data using JTT model
```
cd ../ClustalW2
aa2_clustalw2 <- as.phyDat.AAbin(aa_clustalw2)

tre.ini_aa_clustalw2 <- nj(dist.ml(aa_clustalw2, model="JTT"))
parsimony(tre.ini_aa_clustalw2, aa2_clustalw2)
```
>[1] 73

```
tre.pars_aa_clustalw2 <- optim.parsimony(tre.ini_aa_clustalw2, aa2_clustalw2)
plot(tre.pars_aa_clustalw2, cex=0.2)
```

>Final p-score 73 after  0 nni operations 

##### Change working directory back to MUSCLE directory and run commands to create parsimony-based tree of MUSCLE aligned data using JTT model
```
cd ../MUSCLE
aa2_MUSCLE <- as.phyDat.AAbin(aa_MUSCLE)

tre.ini_aa_MUSCLE <- nj(dist.ml(aa_MUSCLE, model="JTT"))
parsimony(tre.ini_aa_MUSCLE, aa2_MUSCLE)
```

>[1] 71

```
tre.pars_aa_MUSCLE <- optim.parsimony(tre.ini_aa_MUSCLE, aa2_MUSCLE)
plot(tre.pars_aa_MUSCLE, cex=0.2)
```

>Final p-score 71 after  0 nni operations 

All 4 trees saved in figures directory as PDFs with "tree type (distance/parsimony)-tree-alignment method (clustalw2/MUSCLE)" as the file name

# Maximum Likelihood method


I will be using IQ-Tree to construct my maximum-likelihood trees.

##### I copy and pasted both of the aligned sequences files into my directory for IQ-Tree. Also move into the IQ-Tree directory.
```
cp sequences-aligned-muscle.fasta ../IQTree
cd ../ClustalW2
cp sequences-aligned-clustalw2.fasta ../IQTree
cd ../IQTree
```

##### Run the commands to create maximum likelihood trees for sequences of both alignment methods. These commands utilize ModelFinder Plus, which tells IQ-Tree to perform analysis using the substitution model with the minimum Bayesian information criterion score.
'''
bin/iqtree -s sequences-aligned-muscle.fasta
'''

>IQ-TREE multicore version 1.6.12 for Windows 64-bit built Aug 15 2019
Developed by Bui Quang Minh, Nguyen Lam Tung, Olga Chernomor,
Heiko Schmidt, Dominik Schrempf, Michael Woodhams.

> Host:    DESKTOP-6RSS9IC (AVX2, FMA3, 15 GB RAM)
Command: C:\Users\19202\desktop\Botany563\myproject\software\IQTree\bin\iqtree.exe -s sequences-aligned-muscle.fasta
Seed:    37761 (Using SPRNG - Scalable Parallel Random Number Generator)
Time:    Mon May 09 17:28:33 2022
Kernel:  AVX+FMA - 1 threads (8 CPU cores detected)

> HINT: Use -nt option to specify number of threads because your CPU has 8 cores!
HINT: -nt AUTO will automatically determine the best number of threads to use.

> Reading alignment file sequences-aligned-muscle.fasta ... Fasta format detected
Alignment most likely contains protein sequences
Alignment has 20 sequences with 741 columns, 84 distinct patterns
30 parsimony-informative, 26 singleton sites, 685 constant sites
                Gap/Ambiguity  Composition  p-value
   1  XP_025261308.1    1.89%    passed    100.00%
   2  XP_032134401.1    1.89%    passed    100.00%
   3  XP_015990567.2    1.08%    passed    100.00%
   4  PNI67080.1        0.00%    passed    100.00%
   5  XP_011224853.1    1.89%    passed    100.00%
   6  XP_033086464.1    1.89%    passed    100.00%
   7  PNJ73451.1        0.00%    passed    100.00%
   8  XP_011805264.1    1.08%    passed    100.00%
   9  XP_023075176.1    1.89%    passed    100.00%
  10  P0CB68.1          1.89%    passed    100.00%
  11  XP_030659807.1    1.89%    passed    100.00%
  12  NP_001266520.1    2.02%    passed    100.00%
  13  XP_032610702.1    1.89%    passed    100.00%
  14  XP_002749725.2    1.89%    passed    100.00%
  15  XP_008972488.1    1.89%    passed    100.00%
  16  XP_003907894.1    1.89%    passed    100.00%
  17  XP_006921444.1    1.89%    passed    100.00%
  18  XP_039325526.1    1.89%    passed    100.00%
  19  XP_010350948.1    1.89%    passed    100.00%
  20  Q4R6K9.1          1.89%    passed    100.00%
****  TOTAL             1.63%  0 sequences failed composition chi2 test (p-value<5%; df=19)


> Create initial parsimony tree by phylogenetic likelihood library (PLL)... 0.009 seconds
NOTE: ModelFinder requires 3 MB RAM!
ModelFinder will test 546 protein models (sample size: 741) ...
 No. Model         -LnL         df  AIC          AICc
      BIC
  1  Dayhoff       2751.889     37  5577.779     5581.779     5748.275
  2  Dayhoff+I     2732.428     38  5540.857     5545.079     5715.961
  3  Dayhoff+G4    2734.338     38  5544.675     5548.897     5719.779
  4  Dayhoff+I+G4  2731.951     39  5541.901     5546.352     5721.613
  5  Dayhoff+R2    2730.888     39  5539.775     5544.226     5719.487
  6  Dayhoff+R3    2729.677     41  5541.354     5546.281     5730.282
 14  Dayhoff+F     2713.824     56  5539.648     5548.981     5797.696
 15  Dayhoff+F+I   2695.881     57  5505.762     5515.443     5768.418
 16  Dayhoff+F+G4  2697.232     57  5508.464     5518.145     5771.120
 17  Dayhoff+F+I+G4 2695.304     58  5506.609     5516.644     5773.873
 18  Dayhoff+F+R2  2693.090     58  5502.179     5512.214     5769.443
 19  Dayhoff+F+R3  2692.735     60  5505.470     5516.235     5781.950
 27  mtMAM         2899.071     37  5872.141     5876.141     6042.637
 28  mtMAM+I       2875.806     38  5827.611     5831.833     6002.715
 29  mtMAM+G4      2876.947     38  5829.894     5834.116     6004.998
 30  mtMAM+I+G4    2873.631     39  5825.263     5829.714     6004.975
 31  mtMAM+R2      2862.824     39  5803.649     5808.100     5983.361
 32  mtMAM+R3      2862.596     41  5807.193     5812.120     5996.121
 40  mtMAM+F       2739.468     56  5590.937     5600.270     5848.985
 41  mtMAM+F+I     2717.549     57  5549.098     5558.779     5811.754
 42  mtMAM+F+G4    2718.617     57  5551.235     5560.915     5813.891
 43  mtMAM+F+I+G4  2715.590     58  5547.179     5557.214     5814.443
 44  mtMAM+F+R2    2705.100     58  5526.199     5536.235     5793.463
 45  mtMAM+F+R3    2704.863     60  5529.726     5540.491     5806.206
 53  JTT           2710.108     37  5494.216     5498.216     5664.712
 54  JTT+I         2695.037     38  5466.074     5470.296     5641.178
 55  JTT+G4        2695.789     38  5467.577     5471.800     5642.681
 56  JTT+I+G4      2694.506     39  5467.013     5471.464     5646.725
 57  JTT+R2        2693.164     39  5464.329     5468.779     5644.041
 58  JTT+R3        2693.077     41  5468.154     5473.081     5657.082
 66  JTT+F         2696.294     56  5504.587     5513.920     5762.635
 67  JTT+F+I       2681.998     57  5477.996     5487.677     5740.652
 68  JTT+F+G4      2682.526     57  5479.051     5488.732     5741.707
 69  JTT+F+I+G4    2681.409     58  5478.819     5488.854     5746.083
 70  JTT+F+R2      2679.940     58  5475.879     5485.914     5743.143
 71  JTT+F+R3      2679.834     60  5479.669     5490.433     5756.149
 79  WAG           2721.434     37  5516.867     5520.867     5687.363
 80  WAG+I         2706.045     38  5488.090     5492.312     5663.194
 81  WAG+G4        2706.884     38  5489.768     5493.990     5664.872
 82  WAG+I+G4      2705.496     39  5488.992     5493.443     5668.704
 83  WAG+R2        2703.773     39  5485.546     5489.997     5665.258
 84  WAG+R3        2703.719     41  5489.438     5494.365     5678.366
 92  WAG+F         2702.872     56  5517.744     5527.078     5775.793
 93  WAG+F+I       2688.397     57  5490.794     5500.475     5753.450
 94  WAG+F+G4      2688.973     57  5491.946     5501.627     5754.602
 95  WAG+F+I+G4    2687.790     58  5491.581     5501.616     5758.845
 96  WAG+F+R2      2685.985     58  5487.969     5498.005     5755.233
 97  WAG+F+R3      2685.910     60  5491.819     5502.584     5768.299
105  cpREV         2725.636     37  5525.271     5529.271     5695.767
106  cpREV+I       2712.184     38  5500.369     5504.591     5675.473
107  cpREV+G4      2712.489     38  5500.977     5505.200     5676.081
108  cpREV+I+G4    2711.442     39  5500.883     5505.334     5680.595
109  cpREV+R2      2709.138     39  5496.276     5500.727     5675.988
110  cpREV+R3      2709.009     41  5500.018     5504.945     5688.946
118  cpREV+F       2697.992     56  5507.984     5517.317     5766.032
119  cpREV+F+I     2684.372     57  5482.743     5492.424     5745.399
120  cpREV+F+G4    2684.694     57  5483.389     5493.069     5746.045
121  cpREV+F+I+G4  2683.617     58  5483.235     5493.270     5750.499
122  cpREV+F+R2    2681.298     58  5478.596     5488.631     5745.860
123  cpREV+F+R3    2681.199     60  5482.397     5493.162     5758.877
131  mtREV         2871.249     37  5816.497     5820.497     5986.993
132  mtREV+I       2856.055     38  5788.110     5792.332     5963.214
133  mtREV+G4      2856.551     38  5789.101     5793.324     5964.205
134  mtREV+I+G4    2855.245     39  5788.489     5792.940     5968.201
135  mtREV+R2      2852.649     39  5783.297     5787.748     5963.009
136  mtREV+R3      2851.896     41  5785.792     5790.719     5974.720
144  mtREV+F       2717.526     56  5547.051     5556.385     5805.099
145  mtREV+F+I     2702.418     57  5518.836     5528.517     5781.492
146  mtREV+F+G4    2702.971     57  5519.941     5529.622     5782.597
147  mtREV+F+I+G4  2701.567     58  5519.134     5529.169     5786.398
148  mtREV+F+R2    2698.391     58  5512.782     5522.817     5780.046
149  mtREV+F+R3    2697.753     60  5515.507     5526.271     5791.987
157  rtREV         2748.372     37  5570.744     5574.744     5741.240
158  rtREV+I       2733.257     38  5542.513     5546.735     5717.617
159  rtREV+G4      2733.970     38  5543.940     5548.162     5719.044
160  rtREV+I+G4    2732.653     39  5543.307     5547.757     5723.019
161  rtREV+R2      2730.889     39  5539.778     5544.229     5719.490
162  rtREV+R3      2730.822     41  5543.644     5548.571     5732.572
170  rtREV+F       2706.796     56  5525.592     5534.925     5783.640
171  rtREV+F+I     2692.334     57  5498.667     5508.348     5761.323
172  rtREV+F+G4    2692.866     57  5499.733     5509.414     5762.389
173  rtREV+F+I+G4  2691.663     58  5499.326     5509.361     5766.590
174  rtREV+F+R2    2689.673     58  5495.346     5505.381     5762.610
175  rtREV+F+R3    2689.554     60  5499.108     5509.873     5775.588
183  mtART         2900.433     37  5874.866     5878.866     6045.362
184  mtART+I       2882.070     38  5840.141     5844.363     6015.245
185  mtART+G4      2882.882     38  5841.764     5845.986     6016.868
186  mtART+I+G4    2880.580     39  5839.159     5843.610     6018.871
187  mtART+R2      2873.940     39  5825.880     5830.331     6005.593
188  mtART+R3      2872.392     41  5826.783     5831.710     6015.711
196  mtART+F       2740.607     56  5593.214     5602.547     5851.262
197  mtART+F+I     2722.916     57  5559.832     5569.512     5822.488
198  mtART+F+G4    2723.690     57  5561.379     5571.060     5824.035
199  mtART+F+I+G4  2721.398     58  5558.796     5568.831     5826.060
200  mtART+F+R2    2713.164     58  5542.328     5552.363     5809.592
201  mtART+F+R3    2712.361     60  5544.722     5555.487     5821.202
209  mtZOA         2855.196     37  5784.391     5788.391     5954.887
210  mtZOA+I       2839.821     38  5755.642     5759.865     5930.747
211  mtZOA+G4      2840.172     38  5756.343     5760.566     5931.447
212  mtZOA+I+G4    2838.640     39  5755.280     5759.731     5934.992
213  mtZOA+R2      2833.501     39  5745.003     5749.453     5924.715
214  mtZOA+R3      2832.789     41  5747.577     5752.504     5936.505
222  mtZOA+F       2720.777     56  5553.554     5562.887     5811.602
223  mtZOA+F+I     2705.445     57  5524.890     5534.571     5787.546
224  mtZOA+F+G4    2705.902     57  5525.804     5535.484     5788.460
225  mtZOA+F+I+G4  2704.375     58  5524.751     5534.786     5792.015
226  mtZOA+F+R2    2699.282     58  5514.564     5524.599     5781.828
227  mtZOA+F+R3    2698.666     60  5517.332     5528.097     5793.812
235  VT            2721.409     37  5516.818     5520.818     5687.314
236  VT+I          2706.587     38  5489.173     5493.396     5664.277
237  VT+G4         2707.292     38  5490.583     5494.806     5665.687
238  VT+I+G4       2706.033     39  5490.065     5494.516     5669.777
239  VT+R2         2704.634     39  5487.268     5491.719     5666.980
240  VT+R3         2704.553     41  5491.106     5496.033     5680.034
248  VT+F          2705.041     56  5522.082     5531.415     5780.130
249  VT+F+I        2690.779     57  5495.558     5505.239     5758.214
250  VT+F+G4       2691.324     57  5496.648     5506.328     5759.304
251  VT+F+I+G4     2690.180     58  5496.360     5506.395     5763.624
252  VT+F+R2       2688.645     58  5493.290     5503.325     5760.554
253  VT+F+R3       2688.559     60  5497.118     5507.882     5773.598
261  LG            2721.090     37  5516.180     5520.180     5686.676
262  LG+I          2706.354     38  5488.707     5492.929     5663.811
263  LG+G4         2706.992     38  5489.984     5494.206     5665.088
264  LG+I+G4       2705.722     39  5489.445     5493.896     5669.157
265  LG+R2         2703.867     39  5485.734     5490.185     5665.446
266  LG+R3         2703.782     41  5489.565     5494.492     5678.493
274  LG+F          2703.201     56  5518.402     5527.735     5776.450
275  LG+F+I        2689.030     57  5492.061     5501.742     5754.717
276  LG+F+G4       2689.506     57  5493.013     5502.693     5755.669
277  LG+F+I+G4     2688.336     58  5492.672     5502.708     5759.936
278  LG+F+R2       2686.297     58  5488.594     5498.629     5755.858
279  LG+F+R3       2686.205     60  5492.410     5503.175     5768.890
287  DCMut         2751.785     37  5577.569     5581.569     5748.065
288  DCMut+I       2732.363     38  5540.727     5544.949     5715.831
289  DCMut+G4      2734.259     38  5544.519     5548.741     5719.623
290  DCMut+I+G4    2731.809     39  5541.618     5546.069     5721.330
291  DCMut+R2      2729.469     39  5536.938     5541.389     5716.650
292  DCMut+R3      2729.464     41  5540.928     5545.855     5729.856
300  DCMut+F       2713.709     56  5539.418     5548.751     5797.466
301  DCMut+F+I     2695.797     57  5505.594     5515.275     5768.250
302  DCMut+F+G4    2697.139     57  5508.279     5517.959     5770.935
303  DCMut+F+I+G4  2695.151     58  5506.302     5516.337     5773.566
304  DCMut+F+R2    2692.578     58  5501.156     5511.191     5768.420
305  DCMut+F+R3    2692.534     60  5505.068     5515.833     5781.548
313  PMB           2727.698     37  5529.395     5533.395     5699.891
314  PMB+I         2713.363     38  5502.726     5506.949     5677.830
315  PMB+G4        2713.928     38  5503.857     5508.079     5678.961
316  PMB+I+G4      2712.768     39  5503.536     5507.987     5683.248
317  PMB+R2        2711.258     39  5500.516     5504.967     5680.228
318  PMB+R3        2711.211     41  5504.421     5509.348     5693.349
326  PMB+F         2709.786     56  5531.572     5540.905     5789.620
327  PMB+F+I       2695.679     57  5505.357     5515.038     5768.013
328  PMB+F+G4      2696.182     57  5506.364     5516.045     5769.020
329  PMB+F+I+G4    2695.060     58  5506.120     5516.155     5773.384
330  PMB+F+R2      2693.477     58  5502.954     5512.989     5770.218
331  PMB+F+R3      2693.428     60  5506.856     5517.621     5783.336
339  HIVb          2728.984     37  5531.969     5535.969     5702.465
340  HIVb+I        2710.407     38  5496.813     5501.036     5671.917
341  HIVb+G4       2711.590     38  5499.180     5503.403     5674.284
342  HIVb+I+G4     2709.905     39  5497.809     5502.260     5677.521
343  HIVb+R2       2708.934     39  5495.869     5500.320     5675.581
344  HIVb+R3       2708.920     41  5499.840     5504.767     5688.768
352  HIVb+F        2700.395     56  5512.791     5522.124     5770.839
353  HIVb+F+I      2682.356     57  5478.713     5488.394     5741.369
354  HIVb+F+G4     2683.339     57  5480.677     5490.358     5743.333
355  HIVb+F+I+G4   2681.803     58  5479.605     5489.641     5746.870
356  HIVb+F+R2     2680.720     58  5477.441     5487.476     5744.705
357  HIVb+F+R3     2680.692     60  5481.384     5492.149     5757.865
365  HIVw          2781.575     37  5637.150     5641.150     5807.646
366  HIVw+I        2764.675     38  5605.351     5609.573     5780.455
367  HIVw+G4       2765.788     38  5607.576     5611.798     5782.680
368  HIVw+I+G4     2764.061     39  5606.122     5610.572     5785.834
369  HIVw+R2       2762.200     39  5602.400     5606.851     5782.112
370  HIVw+R3       2762.150     41  5606.300     5611.227     5795.228
378  HIVw+F        2708.824     56  5529.647     5538.981     5787.695
379  HIVw+F+I      2693.643     57  5501.286     5510.966     5763.942
380  HIVw+F+G4     2694.286     57  5502.572     5512.253     5765.228
381  HIVw+F+I+G4   2693.004     58  5502.008     5512.043     5769.272
382  HIVw+F+R2     2691.386     58  5498.773     5508.808     5766.037
383  HIVw+F+R3     2691.342     60  5502.684     5513.449     5779.164
391  JTTDCMut      2710.472     37  5494.944     5498.944     5665.440
392  JTTDCMut+I    2695.382     38  5466.763     5470.986     5641.868
393  JTTDCMut+G4   2696.138     38  5468.275     5472.497     5643.379
394  JTTDCMut+I+G4 2694.808     39  5467.615     5472.066     5647.327
395  JTTDCMut+R2   2693.367     39  5464.733     5469.184     5644.445
396  JTTDCMut+R3   2693.338     41  5468.676     5473.603     5657.604
404  JTTDCMut+F    2696.053     56  5504.106     5513.440     5762.154
405  JTTDCMut+F+I  2681.776     57  5477.552     5487.233     5740.208
406  JTTDCMut+F+G4 2682.298     57  5478.596     5488.277     5741.252
407  JTTDCMut+F+I+G4 2681.144     58  5478.288     5488.323     5745.552
408  JTTDCMut+F+R2 2679.633     58  5475.265     5485.301     5742.529
409  JTTDCMut+F+R3 2679.592     60  5479.185     5489.950     5755.665
417  FLU           2734.903     37  5543.806     5547.806     5714.302
418  FLU+I         2720.694     38  5517.387     5521.609     5692.491
419  FLU+G4        2721.059     38  5518.117     5522.340     5693.221
420  FLU+I+G4      2719.899     39  5517.797     5522.248     5697.509
421  FLU+R2        2717.678     39  5513.356     5517.807     5693.068
422  FLU+R3        2717.592     41  5517.184     5522.111     5706.112
430  FLU+F         2697.223     56  5506.447     5515.780     5764.495
431  FLU+F+I       2684.263     57  5482.526     5492.207     5745.182
432  FLU+F+G4      2684.395     57  5482.790     5492.471     5745.446
433  FLU+F+I+G4    2683.399     58  5482.798     5492.833     5750.062
434  FLU+F+R2      2681.260     58  5478.520     5488.555     5745.784
435  FLU+F+R3      2681.169     60  5482.337     5493.102     5758.817
443  Blosum62      2726.032     37  5526.063     5530.063     5696.559
444  Blosum62+I    2711.476     38  5498.953     5503.175     5674.057
445  Blosum62+G4   2712.088     38  5500.177     5504.399     5675.281
446  Blosum62+I+G4 2710.866     39  5499.732     5504.183     5679.444
447  Blosum62+R2   2709.290     39  5496.579     5501.030     5676.291
448  Blosum62+R3   2709.241     41  5500.483     5505.410     5689.411
456  Blosum62+F    2712.050     56  5536.099     5545.433     5794.147
457  Blosum62+F+I  2697.696     57  5509.392     5519.073     5772.048
458  Blosum62+F+G4 2698.251     57  5510.502     5520.183     5773.158
459  Blosum62+F+I+G4 2697.062     58  5510.124     5520.159     5777.388
460  Blosum62+F+R2 2695.405     58  5506.810     5516.845     5774.074
461  Blosum62+F+R3 2695.354     60  5510.707     5521.472     5787.187
469  mtMet         2891.328     37  5856.657     5860.657     6027.153
470  mtMet+I       2876.892     38  5829.784     5834.006     6004.888
471  mtMet+G4      2877.225     38  5830.451     5834.673     6005.555
472  mtMet+I+G4    2875.883     39  5829.766     5834.217     6009.478
473  mtMet+R2      2872.889     39  5823.779     5828.230     6003.491
474  mtMet+R3      2872.048     41  5826.096     5831.023     6015.024
482  mtMet+F       2712.946     56  5537.892     5547.225     5795.940
483  mtMet+F+I     2698.324     57  5510.648     5520.329     5773.304
484  mtMet+F+G4    2698.766     57  5511.531     5521.212     5774.187
485  mtMet+F+I+G4  2697.406     58  5510.811     5520.846     5778.075
486  mtMet+F+R2    2694.468     58  5504.936     5514.971     5772.200
487  mtMet+F+R3    2693.983     60  5507.965     5518.730     5784.445
495  mtVer         2888.129     37  5850.259     5854.259     6020.755
496  mtVer+I       2873.057     38  5822.114     5826.336     5997.218
497  mtVer+G4      2873.425     38  5822.849     5827.071     5997.953
498  mtVer+I+G4    2871.710     39  5821.419     5825.870     6001.131
499  mtVer+R2      2866.235     39  5810.471     5814.922     5990.183
500  mtVer+R3      2865.880     41  5813.760     5818.687     6002.688
508  mtVer+F       2719.042     56  5550.083     5559.417     5808.131
509  mtVer+F+I     2704.376     57  5522.752     5532.433     5785.408
510  mtVer+F+G4    2704.829     57  5523.657     5533.338     5786.314
511  mtVer+F+I+G4  2703.239     58  5522.477     5532.513     5789.741
512  mtVer+F+R2    2698.189     58  5512.378     5522.414     5779.642
513  mtVer+F+R3    2697.872     60  5515.744     5526.509     5792.224
521  mtInv         2932.016     37  5938.032     5942.032     6108.528
522  mtInv+I       2917.420     38  5910.840     5915.062     6085.944
523  mtInv+G4      2917.841     38  5911.682     5915.904     6086.786
524  mtInv+I+G4    2916.544     39  5911.087     5915.538     6090.799
525  mtInv+R2      2913.850     39  5905.700     5910.151     6085.412
526  mtInv+R3      2913.500     41  5909.000     5913.927     6097.928
534  mtInv+F       2710.617     56  5533.234     5542.568     5791.282
535  mtInv+F+I     2695.692     57  5505.385     5515.065     5768.041
536  mtInv+F+G4    2696.257     57  5506.515     5516.195     5769.171
537  mtInv+F+I+G4  2694.857     58  5505.714     5515.749     5772.978
538  mtInv+F+R2    2692.228     58  5500.457     5510.492     5767.721
539  mtInv+F+R3    2691.985     60  5503.971     5514.735     5780.451
Akaike Information Criterion:           JTT+R2
Corrected Akaike Information Criterion: JTT+R2
Bayesian Information Criterion:         JTT+I
Best-fit model: JTT+I chosen according to BIC

> All model information printed to sequences-aligned-muscle.fasta.model.gz
CPU time for ModelFinder: 4.719 seconds (0h:0m:4s)
Wall-clock time for ModelFinder: 6.332 seconds (0h:0m:6s)

> NOTE: 0 MB RAM (0 GB) is required!
Estimate model parameters (epsilon = 0.100)
1. Initial log-likelihood: -2702.456
2. Current log-likelihood: -2695.058
Optimal log-likelihood: -2695.037
Proportion of invariable sites: 0.813
Parameters optimization took 2 rounds (0.017 sec)
Computing ML distances based on estimated model parameters... 0.031 sec
Computing BIONJ tree...
0.012 seconds
Log-likelihood of BIONJ tree: -2694.838
--------------------------------------------------------------------
|             INITIALIZING CANDIDATE TREE SET
           |
--------------------------------------------------------------------
Generating 98 parsimony trees... 0.107 second
Computing log-likelihood of 98 initial trees ... 0.162 seconds
Current best score: -2693.300

> Do NNI search on 20 best initial trees
Estimate model parameters (epsilon = 0.100)
BETTER TREE FOUND at iteration 1: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 10 / LogL: -2693.297 / Time: 0h:0m:0s
UPDATE BEST LOG-LIKELIHOOD: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 20 / LogL: -2693.297 / Time: 0h:0m:0s
Finish initializing candidate tree set (3)
Current best tree score: -2693.297 / CPU time: 0.482
Number of iterations: 20
--------------------------------------------------------------------
|               OPTIMIZING CANDIDATE TREE SET
           |
--------------------------------------------------------------------
UPDATE BEST LOG-LIKELIHOOD: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 30 / LogL: -2693.297 / Time: 0h:0m:0s (0h:0m:1s left)
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 40 / LogL: -2693.298 / Time: 0h:0m:0s (0h:0m:1s left)
BETTER TREE FOUND at iteration 41: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 50 / LogL: -2693.297 / Time: 0h:0m:1s (0h:0m:2s left)
UPDATE BEST LOG-LIKELIHOOD: -2693.297
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 60 / LogL: -2693.297 / Time: 0h:0m:1s (0h:0m:1s left)
Iteration 70 / LogL: -2693.297 / Time: 0h:0m:1s (0h:0m:1s left)
Iteration 80 / LogL: -2693.297 / Time: 0h:0m:1s (0h:0m:1s left)
Iteration 90 / LogL: -2693.297 / Time: 0h:0m:1s (0h:0m:1s left)
UPDATE BEST LOG-LIKELIHOOD: -2693.297
Iteration 100 / LogL: -2693.298 / Time: 0h:0m:1s (0h:0m:0s left)
Iteration 110 / LogL: -2693.297 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 120 / LogL: -2693.298 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 130 / LogL: -2693.301 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 140 / LogL: -2693.297 / Time: 0h:0m:2s (0h:0m:0s left)
TREE SEARCH COMPLETED AFTER 142 ITERATIONS / Time: 0h:0m:2s

> --------------------------------------------------------------------
|                    FINALIZING TREE SEARCH
           |
> --------------------------------------------------------------------
> Performs final model parameters optimization
Estimate model parameters (epsilon = 0.010)
1. Initial log-likelihood: -2693.297
Optimal log-likelihood: -2693.297
Proportion of invariable sites: 0.813
Parameters optimization took 1 rounds (0.011 sec)
BEST SCORE FOUND : -2693.297
Total tree length: 0.099

> Total number of iterations: 142
CPU time used for tree search: 2.359 sec (0h:0m:2s)
Wall-clock time used for tree search: 2.555 sec (0h:0m:2s)
Total CPU time used: 2.438 sec (0h:0m:2s)
Total wall-clock time used: 2.704 sec (0h:0m:2s)

> Analysis results written to:
  IQ-TREE report:                sequences-aligned-muscle.fasta.iqtree
  Maximum-likelihood tree:       sequences-aligned-muscle.fasta.treefile
  Likelihood distances:          sequences-aligned-muscle.fasta.mldist
  Screen log file:               sequences-aligned-muscle.fasta.log

> Date and Time: Mon May 09 17:28:42 2022

'''
bin/iqtree -s sequences-aligned-clustalw2.fasta
'''

> IQ-TREE multicore version 1.6.12 for Windows 64-bit built Aug 15 2019
Developed by Bui Quang Minh, Nguyen Lam Tung, Olga Chernomor,
Heiko Schmidt, Dominik Schrempf, Michael Woodhams.

> Host:    DESKTOP-6RSS9IC (AVX2, FMA3, 15 GB RAM)
Command: C:\Users\19202\desktop\Botany563\myproject\software\IQTree\bin\iqtree.exe -s sequences-aligned-clustalw2.fasta
Seed:    231123 (Using SPRNG - Scalable Parallel Random
Number Generator)
Time:    Mon May 09 17:31:12 2022
Kernel:  AVX+FMA - 1 threads (8 CPU cores detected)

> HINT: Use -nt option to specify number of threads because your CPU has 8 cores!
HINT: -nt AUTO will automatically determine the best number of threads to use.

> Reading alignment file sequences-aligned-clustalw2.fasta ... Fasta format detected
Alignment most likely contains protein sequences
Alignment has 20 sequences with 741 columns, 83 distinct patterns
31 parsimony-informative, 26 singleton sites, 684 constant sites
                Gap/Ambiguity  Composition  p-value
   1  XP_002749725.2    1.89%    passed    100.00%
   2  XP_032134401.1    1.89%    passed    100.00%
   3  XP_039325526.1    1.89%    passed    100.00%
   4  PNI67080.1        0.00%    passed    100.00%
   5  XP_008972488.1    1.89%    passed    100.00%
   6  NP_001266520.1    2.02%    passed    100.00%
   7  PNJ73451.1        0.00%    passed    100.00%
   8  P0CB68.1          1.89%    passed    100.00%
   9  XP_032610702.1    1.89%    passed    100.00%
  10  XP_030659807.1    1.89%    passed    100.00%
  11  Q4R6K9.1          1.89%    passed    100.00%
  12  XP_025261308.1    1.89%    passed    100.00%
  13  XP_003907894.1    1.89%    passed    100.00%
  14  XP_010350948.1    1.89%    passed    100.00%
  15  XP_033086464.1    1.89%    passed    100.00%
  16  XP_011805264.1    1.08%    passed    100.00%
  17  XP_023075176.1    1.89%    passed    100.00%
  18  XP_015990567.2    1.08%    passed    100.00%
  19  XP_006921444.1    1.89%    passed    100.00%
  20  XP_011224853.1    1.89%    passed    100.00%
****  TOTAL             1.63%  0 sequences failed composition chi2 test (p-value<5%; df=19)


> Create initial parsimony tree by phylogenetic likelihood library (PLL)... 0.007 seconds
NOTE: ModelFinder requires 3 MB RAM!
ModelFinder will test 546 protein models (sample size: 741) ...
 No. Model         -LnL         df  AIC          AICc
      BIC
  1  Dayhoff       2770.416     37  5614.831     5618.831     5785.327
  2  Dayhoff+I     2749.190     38  5574.380     5578.602     5749.484
  3  Dayhoff+G4    2751.425     38  5578.849     5583.071     5753.953
  4  Dayhoff+I+G4  2748.599     39  5575.197     5579.648     5754.909
  5  Dayhoff+R2    2745.193     39  5568.386     5572.837     5748.098
  6  Dayhoff+R3    2745.055     41  5572.109     5577.036     5761.037
 14  Dayhoff+F     2731.189     56  5574.378     5583.711     5832.426
 15  Dayhoff+F+I   2711.595     57  5537.190     5546.871     5799.846
 16  Dayhoff+F+G4  2713.210     57  5540.421     5550.102     5803.077
 17  Dayhoff+F+I+G4 2710.882     58  5537.765     5547.800     5805.029
 18  Dayhoff+F+R2  2707.173     58  5530.346     5540.382     5797.611
 19  Dayhoff+F+R3  2706.988     60  5533.976     5544.741     5810.456
 27  mtMAM         2910.970     37  5895.940     5899.940     6066.436
 28  mtMAM+I       2886.466     38  5848.932     5853.154     6024.036
 29  mtMAM+G4      2887.658     38  5851.316     5855.539     6026.420
 30  mtMAM+I+G4    2884.107     39  5846.215     5850.665     6025.927
 31  mtMAM+R2      2873.351     39  5824.703     5829.154     6004.415
 32  mtMAM+R3      2872.366     41  5826.732     5831.659     6015.660
 40  mtMAM+F       2750.745     56  5613.491     5622.824     5871.539
 41  mtMAM+F+I     2727.710     57  5569.421     5579.101     5832.077
 42  mtMAM+F+G4    2728.833     57  5571.666     5581.347     5834.322
 43  mtMAM+F+I+G4  2725.672     58  5567.344     5577.380     5834.608
 44  mtMAM+F+R2    2715.793     58  5547.586     5557.621     5814.850
 45  mtMAM+F+R3    2714.826     60  5549.653     5560.418     5826.133
 53  JTT           2726.433     37  5526.866     5530.866     5697.362
 54  JTT+I         2709.804     38  5495.609     5499.831     5670.713
 55  JTT+G4        2710.770     38  5497.540     5501.762     5672.644
 56  JTT+I+G4      2709.244     39  5496.488     5500.939     5676.200
 57  JTT+R2        2707.510     39  5493.020     5497.471     5672.732
 58  JTT+R3        2707.427     41  5496.855     5501.782     5685.783
 66  JTT+F         2712.248     56  5536.496     5545.829     5794.544
 67  JTT+F+I       2696.457     57  5506.914     5516.595     5769.570
 68  JTT+F+G4      2697.160     57  5508.320     5518.001     5770.976
 69  JTT+F+I+G4    2695.835     58  5507.671     5517.706     5774.935
 70  JTT+F+R2      2693.980     58  5503.961     5513.996     5771.225
 71  JTT+F+R3      2693.883     60  5507.766     5518.531     5784.246
 79  WAG           2738.323     37  5550.646     5554.646     5721.142
 80  WAG+I         2721.411     38  5518.821     5523.043     5693.925
 81  WAG+G4        2722.459     38  5520.917     5525.140     5696.022
 82  WAG+I+G4      2720.826     39  5519.652     5524.103     5699.364
 83  WAG+R2        2718.629     39  5515.258     5519.709     5694.970
 84  WAG+R3        2718.579     41  5519.158     5524.085     5708.086
 92  WAG+F         2719.022     56  5550.044     5559.377     5808.092
 93  WAG+F+I       2703.092     57  5520.185     5529.866     5782.841
 94  WAG+F+G4      2703.838     57  5521.675     5531.356     5784.331
 95  WAG+F+I+G4    2702.448     58  5520.896     5530.931     5788.160
 96  WAG+F+R2      2700.187     58  5516.375     5526.410     5783.639
 97  WAG+F+R3      2700.116     60  5520.233     5530.998     5796.713
105  cpREV         2742.453     37  5558.905     5562.905     5729.401
106  cpREV+I       2727.418     38  5530.835     5535.057     5705.939
107  cpREV+G4      2727.878     38  5531.756     5535.979     5706.860
108  cpREV+I+G4    2726.572     39  5531.145     5535.595     5710.857
109  cpREV+R2      2723.404     39  5524.809     5529.260     5704.521
110  cpREV+R3      2723.271     41  5528.542     5533.469     5717.470
118  cpREV+F       2714.546     56  5541.091     5550.425     5799.139
119  cpREV+F+I     2699.302     57  5512.604     5522.284     5775.260
120  cpREV+F+G4    2699.791     57  5513.581     5523.262     5776.237
121  cpREV+F+I+G4  2698.442     58  5512.884     5522.919     5780.148
122  cpREV+F+R2    2695.266     58  5506.533     5516.568     5773.797
123  cpREV+F+R3    2695.154     60  5510.307     5521.072     5786.787
131  mtREV         2884.313     37  5842.626     5846.626     6013.122
132  mtREV+I       2867.760     38  5811.519     5815.741     5986.623
133  mtREV+G4      2868.361     38  5812.723     5816.945     5987.827
134  mtREV+I+G4    2866.854     39  5811.707     5816.158     5991.419
135  mtREV+R2      2863.232     39  5804.463     5808.914     5984.175
136  mtREV+R3      2862.795     41  5807.590     5812.517     5996.518
144  mtREV+F       2729.886     56  5571.773     5581.106     5829.821
145  mtREV+F+I     2713.379     57  5540.758     5550.439     5803.414
146  mtREV+F+G4    2714.058     57  5542.115     5551.796     5804.771
147  mtREV+F+I+G4  2712.444     58  5540.888     5550.923     5808.152
148  mtREV+F+R2    2708.475     58  5532.949     5542.984     5800.213
149  mtREV+F+R3    2708.152     60  5536.304     5547.069     5812.784
157  rtREV         2766.187     37  5606.374     5610.374     5776.870
158  rtREV+I       2749.572     38  5575.143     5579.365     5750.247
159  rtREV+G4      2750.473     38  5576.947     5581.169     5752.051
160  rtREV+I+G4    2748.945     39  5575.890     5580.341     5755.602
161  rtREV+R2      2746.888     39  5571.775     5576.226     5751.487
162  rtREV+R3      2746.754     41  5575.508     5580.435     5764.436
170  rtREV+F       2723.688     56  5559.376     5568.710     5817.424
171  rtREV+F+I     2707.777     57  5529.554     5539.235     5792.210
172  rtREV+F+G4    2708.470     57  5530.941     5540.621     5793.597
173  rtREV+F+I+G4  2707.085     58  5530.169     5540.204     5797.433
174  rtREV+F+R2    2704.785     58  5525.570     5535.605     5792.834
175  rtREV+F+R3    2704.662     60  5529.324     5540.089     5805.804
183  mtART         2916.139     37  5906.278     5910.278     6076.774
184  mtART+I       2896.179     38  5868.358     5872.580     6043.462
185  mtART+G4      2897.148     38  5870.295     5874.518     6045.399
186  mtART+I+G4    2894.529     39  5867.057     5871.508     6046.769
187  mtART+R2      2886.328     39  5850.656     5855.106     6030.368
188  mtART+R3      2885.543     41  5853.086     5858.013     6042.014
196  mtART+F       2755.687     56  5623.374     5632.708     5881.422
197  mtART+F+I     2736.414     57  5586.828     5596.509     5849.484
198  mtART+F+G4    2737.350     57  5588.700     5598.381     5851.356
199  mtART+F+I+G4  2734.808     58  5585.616     5595.651     5852.880
200  mtART+F+R2    2726.243     58  5568.485     5578.520     5835.749
201  mtART+F+R3    2725.560     60  5571.120     5581.884     5847.600
209  mtZOA         2871.607     37  5817.214     5821.214     5987.710
210  mtZOA+I       2854.737     38  5785.473     5789.695     5960.577
211  mtZOA+G4      2855.205     38  5786.410     5790.633     5961.514
212  mtZOA+I+G4    2853.409     39  5784.818     5789.268     5964.530
213  mtZOA+R2      2847.127     39  5772.254     5776.705     5951.966
214  mtZOA+R3      2846.495     41  5774.989     5779.916     5963.917
222  mtZOA+F       2736.614     56  5585.229     5594.562     5843.277
223  mtZOA+F+I     2719.667     57  5553.334     5563.015     5815.990
224  mtZOA+F+G4    2720.293     57  5554.586     5564.267     5817.242
225  mtZOA+F+I+G4  2718.465     58  5552.929     5562.964     5820.193
226  mtZOA+F+R2    2712.290     58  5540.581     5550.616     5807.845
227  mtZOA+F+R3    2711.759     60  5543.518     5554.282     5819.998
235  VT            2737.922     37  5549.843     5553.843     5720.339
236  VT+I          2721.590     38  5519.181     5523.403     5694.285
237  VT+G4         2722.494     38  5520.987     5525.210     5696.092
238  VT+I+G4       2721.016     39  5520.032     5524.483     5699.744
239  VT+R2         2719.363     39  5516.725     5521.176     5696.437
240  VT+R3         2719.262     41  5520.525     5525.452     5709.453
248  VT+F          2721.044     56  5554.088     5563.422     5812.136
249  VT+F+I        2705.307     57  5524.614     5534.295     5787.270
250  VT+F+G4       2706.027     57  5526.053     5535.734     5788.709
251  VT+F+I+G4     2704.686     58  5525.373     5535.408     5792.637
252  VT+F+R2       2702.896     58  5521.792     5531.827     5789.056
253  VT+F+R3       2702.815     60  5525.631     5536.395     5802.111
261  LG            2737.599     37  5549.199     5553.199     5719.695
262  LG+I          2721.352     38  5518.703     5522.926     5693.808
263  LG+G4         2722.177     38  5520.354     5524.576     5695.458
264  LG+I+G4       2720.665     39  5519.330     5523.781     5699.042
265  LG+R2         2718.244     39  5514.488     5518.939     5694.200
266  LG+R3         2718.177     41  5518.354     5523.281     5707.282
274  LG+F          2719.362     56  5550.724     5560.058     5808.772
275  LG+F+I        2703.711     57  5521.422     5531.102     5784.078
276  LG+F+G4       2704.350     57  5522.699     5532.380     5785.355
277  LG+F+I+G4     2702.960     58  5521.919     5531.955     5789.183
278  LG+F+R2       2700.362     58  5516.723     5526.758     5783.987
279  LG+F+R3       2700.287     60  5520.574     5531.339     5797.054
287  DCMut         2770.295     37  5614.590     5618.590     5785.086
288  DCMut+I       2749.114     38  5574.227     5578.450     5749.331
289  DCMut+G4      2751.333     38  5578.667     5582.889     5753.771
290  DCMut+I+G4    2748.407     39  5574.815     5579.266     5754.527
291  DCMut+R2      2744.996     39  5567.992     5572.443     5747.704
292  DCMut+R3      2744.965     41  5571.930     5576.857     5760.858
300  DCMut+F       2731.055     56  5574.109     5583.443     5832.158
301  DCMut+F+I     2711.496     57  5536.992     5546.673     5799.648
302  DCMut+F+G4    2713.101     57  5540.202     5549.882     5802.858
303  DCMut+F+I+G4  2710.680     58  5537.359     5547.394     5804.623
304  DCMut+F+R2    2706.990     58  5529.980     5540.016     5797.244
305  DCMut+F+R3    2706.946     60  5533.892     5544.657     5810.372
313  PMB           2744.107     37  5562.214     5566.214     5732.710
314  PMB+I         2728.341     38  5532.682     5536.904     5707.786
315  PMB+G4        2729.070     38  5534.141     5538.363     5709.245
316  PMB+I+G4      2727.726     39  5533.452     5537.903     5713.164
317  PMB+R2        2726.059     39  5530.118     5534.569     5709.830
318  PMB+R3        2726.015     41  5534.031     5538.958     5722.959
326  PMB+F         2725.779     56  5563.558     5572.891     5821.606
327  PMB+F+I       2710.239     57  5534.478     5544.159     5797.135
328  PMB+F+G4      2710.902     57  5535.804     5545.485     5798.460
329  PMB+F+I+G4    2709.600     58  5535.199     5545.234     5802.463
330  PMB+F+R2      2707.838     58  5531.676     5541.711     5798.940
331  PMB+F+R3      2707.799     60  5535.597     5546.362     5812.077
339  HIVb          2745.496     37  5564.991     5568.991     5735.487
340  HIVb+I        2725.756     38  5527.513     5531.735     5702.617
341  HIVb+G4       2727.106     38  5530.211     5534.433     5705.315
342  HIVb+I+G4     2725.110     39  5528.220     5532.671     5707.932
343  HIVb+R2       2723.474     39  5524.948     5529.399     5704.660
344  HIVb+R3       2723.421     41  5528.842     5533.769     5717.770
352  HIVb+F        2716.597     56  5545.194     5554.527     5803.242
353  HIVb+F+I      2697.444     57  5508.888     5518.569     5771.544
354  HIVb+F+G4     2698.573     57  5511.145     5520.826     5773.801
355  HIVb+F+I+G4   2696.740     58  5509.481     5519.516     5776.745
356  HIVb+F+R2     2694.987     58  5505.975     5516.010     5773.239
357  HIVb+F+R3     2694.937     60  5509.874     5520.639     5786.354
365  HIVw          2801.056     37  5676.111     5680.111     5846.607
366  HIVw+I        2782.320     38  5640.640     5644.862     5815.744
367  HIVw+G4       2783.739     38  5643.477     5647.699     5818.581
368  HIVw+I+G4     2781.520     39  5641.040     5645.491     5820.752
369  HIVw+R2       2778.341     39  5634.683     5639.133     5814.395
370  HIVw+R3       2778.268     41  5638.536     5643.463     5827.464
378  HIVw+F        2727.620     56  5567.239     5576.572     5825.287
379  HIVw+F+I      2710.733     57  5535.466     5545.146     5798.122
380  HIVw+F+G4     2711.604     57  5537.208     5546.889     5799.864
381  HIVw+F+I+G4   2709.906     58  5535.812     5545.847     5803.076
382  HIVw+F+R2     2707.092     58  5530.184     5540.219     5797.448
383  HIVw+F+R3     2707.019     60  5534.039     5544.803     5810.519
391  JTTDCMut      2726.941     37  5527.882     5531.882     5698.378
392  JTTDCMut+I    2710.273     38  5496.546     5500.768     5671.650
393  JTTDCMut+G4   2711.248     38  5498.496     5502.718     5673.600
394  JTTDCMut+I+G4 2709.649     39  5497.299     5501.750     5677.011
395  JTTDCMut+R2   2707.826     39  5493.651     5498.102     5673.363
396  JTTDCMut+R3   2707.807     41  5497.613     5502.540     5686.541
404  JTTDCMut+F    2712.124     56  5536.249     5545.582     5794.297
405  JTTDCMut+F+I  2696.337     57  5506.673     5516.354     5769.329
406  JTTDCMut+F+G4 2697.037     57  5508.074     5517.755     5770.730
407  JTTDCMut+F+I+G4 2695.653     58  5507.306     5517.341     5774.570
408  JTTDCMut+F+R2 2693.753     58  5503.507     5513.542     5770.771
409  JTTDCMut+F+R3 2693.716     60  5507.432     5518.197     5783.912
417  FLU           2752.484     37  5578.969     5582.969     5749.465
418  FLU+I         2737.032     38  5550.064     5554.286     5725.168
419  FLU+G4        2737.518     38  5551.037     5555.259     5726.141
420  FLU+I+G4      2736.033     39  5550.066     5554.516     5729.778
421  FLU+R2        2732.489     39  5542.978     5547.429     5722.690
422  FLU+R3        2732.399     41  5546.797     5551.724     5735.725
430  FLU+F         2714.116     56  5540.232     5549.565     5798.280
431  FLU+F+I       2699.999     57  5513.998     5523.679     5776.654
432  FLU+F+G4      2700.201     57  5514.402     5524.083     5777.058
433  FLU+F+I+G4    2698.923     58  5513.846     5523.881     5781.110
434  FLU+F+R2      2695.499     58  5506.999     5517.034     5774.263
435  FLU+F+R3      2695.362     60  5510.723     5521.488     5787.203
443  Blosum62      2742.385     37  5558.770     5562.770     5729.266
444  Blosum62+I    2726.386     38  5528.772     5532.994     5703.876
445  Blosum62+G4   2727.168     38  5530.336     5534.558     5705.440
446  Blosum62+I+G4 2725.749     39  5529.497     5533.948     5709.209
447  Blosum62+R2   2724.001     39  5526.002     5530.452     5705.714
448  Blosum62+R3   2723.942     41  5529.884     5534.811     5718.812
456  Blosum62+F    2728.076     56  5568.151     5577.485     5826.200
457  Blosum62+F+I  2712.276     57  5538.551     5548.232     5801.207
458  Blosum62+F+G4 2712.997     57  5539.993     5549.674     5802.649
459  Blosum62+F+I+G4 2711.614     58  5539.227     5549.262     5806.491
460  Blosum62+F+R2 2709.744     58  5535.489     5545.524     5802.753
461  Blosum62+F+R3 2709.690     60  5539.381     5550.146     5815.861
469  mtMet         2908.123     37  5890.247     5894.247     6060.743
470  mtMet+I       2892.193     38  5860.387     5864.609     6035.491
471  mtMet+G4      2892.655     38  5861.311     5865.533     6036.415
472  mtMet+I+G4    2891.057     39  5860.114     5864.565     6039.826
473  mtMet+R2      2886.396     39  5850.792     5855.243     6030.504
474  mtMet+R3      2886.087     41  5854.175     5859.102     6043.103
482  mtMet+F       2728.965     56  5569.929     5579.262     5827.977
483  mtMet+F+I     2712.765     57  5539.530     5549.211     5802.186
484  mtMet+F+G4    2713.376     57  5540.752     5550.432     5803.408
485  mtMet+F+I+G4  2711.734     58  5539.469     5549.504     5806.733
486  mtMet+F+R2    2707.488     58  5530.976     5541.011     5798.240
487  mtMet+F+R3    2707.228     60  5534.455     5545.220     5810.935
495  mtVer         2904.226     37  5882.452     5886.452     6052.948
496  mtVer+I       2887.710     38  5851.421     5855.643     6026.525
497  mtVer+G4      2888.191     38  5852.382     5856.605     6027.486
498  mtVer+I+G4    2886.223     39  5850.447     5854.897     6030.159
499  mtVer+R2      2879.747     39  5837.494     5841.944     6017.206
500  mtVer+R3      2879.036     41  5840.072     5844.999     6029.000
508  mtVer+F       2734.227     56  5580.454     5589.788     5838.503
509  mtVer+F+I     2718.028     57  5550.056     5559.737     5812.712
510  mtVer+F+G4    2718.643     57  5551.286     5560.967     5813.942
511  mtVer+F+I+G4  2716.792     58  5549.585     5559.620     5816.849
512  mtVer+F+R2    2710.882     58  5537.765     5547.800     5805.029
513  mtVer+F+R3    2710.265     60  5540.530     5551.295     5817.010
521  mtInv         2949.492     37  5972.985     5976.985     6143.481
522  mtInv+I       2933.381     38  5942.762     5946.985     6117.866
523  mtInv+G4      2933.954     38  5943.907     5948.129     6119.011
524  mtInv+I+G4    2932.394     39  5942.788     5947.239     6122.500
525  mtInv+R2      2928.596     39  5935.193     5939.644     6114.905
526  mtInv+R3      2928.195     41  5938.391     5943.318     6127.319
534  mtInv+F       2727.276     56  5566.551     5575.884     5824.599
535  mtInv+F+I     2710.735     57  5535.471     5545.151     5798.127
536  mtInv+F+G4    2711.500     57  5536.999     5546.680     5799.655
537  mtInv+F+I+G4  2709.799     58  5535.598     5545.633     5802.862
538  mtInv+F+R2    2706.110     58  5528.221     5538.256     5795.485
539  mtInv+F+R3    2705.937     60  5531.875     5542.639     5808.355
Akaike Information Criterion:           JTT+R2
Corrected Akaike Information Criterion: JTT+R2
Bayesian Information Criterion:         JTT+I
Best-fit model: JTT+I chosen according to BIC

> All model information printed to sequences-aligned-clustalw2.fasta.model.gz
CPU time for ModelFinder: 4.734 seconds (0h:0m:4s)
Wall-clock time for ModelFinder: 6.565 seconds (0h:0m:6s)

> NOTE: 0 MB RAM (0 GB) is required!
Estimate model parameters (epsilon = 0.100)
1. Initial log-likelihood: -2718.177
2. Current log-likelihood: -2709.831
Optimal log-likelihood: -2709.804
Proportion of invariable sites: 0.818
Parameters optimization took 2 rounds (0.019 sec)
Computing ML distances based on estimated model parameters... 0.031 sec
Computing BIONJ tree...
0.012 seconds
Log-likelihood of BIONJ tree: -2711.082
--------------------------------------------------------------------
|             INITIALIZING CANDIDATE TREE SET
           |
--------------------------------------------------------------------
Generating 98 parsimony trees... 0.106 second
Computing log-likelihood of 98 initial trees ... 0.168 seconds
Current best score: -2709.525

> Do NNI search on 20 best initial trees
Estimate model parameters (epsilon = 0.100)
BETTER TREE FOUND at iteration 1: -2709.518
BETTER TREE FOUND at iteration 2: -2709.518
UPDATE BEST LOG-LIKELIHOOD: -2709.518
Iteration 10 / LogL: -2709.518 / Time: 0h:0m:0s
UPDATE BEST LOG-LIKELIHOOD: -2709.518
Iteration 20 / LogL: -2709.518 / Time: 0h:0m:0s
Finish initializing candidate tree set (2)
Current best tree score: -2709.518 / CPU time: 0.524
Number of iterations: 20
--------------------------------------------------------------------
|               OPTIMIZING CANDIDATE TREE SET
           |
--------------------------------------------------------------------
Iteration 30 / LogL: -2709.518 / Time: 0h:0m:0s (0h:0m:2s left)
BETTER TREE FOUND at iteration 31: -2709.518
UPDATE BEST LOG-LIKELIHOOD: -2709.518
UPDATE BEST LOG-LIKELIHOOD: -2709.518
UPDATE BEST LOG-LIKELIHOOD: -2709.518
Iteration 40 / LogL: -2709.518 / Time: 0h:0m:1s (0h:0m:2s left)
UPDATE BEST LOG-LIKELIHOOD: -2709.518
Iteration 50 / LogL: -2709.518 / Time: 0h:0m:1s (0h:0m:2s left)
Iteration 60 / LogL: -2709.518 / Time: 0h:0m:1s (0h:0m:1s left)
UPDATE BEST LOG-LIKELIHOOD: -2709.518
Iteration 70 / LogL: -2709.519 / Time: 0h:0m:1s (0h:0m:1s left)
UPDATE BEST LOG-LIKELIHOOD: -2709.517
Iteration 80 / LogL: -2709.518 / Time: 0h:0m:1s (0h:0m:1s left)
Iteration 90 / LogL: -2709.518 / Time: 0h:0m:2s (0h:0m:0s left)
UPDATE BEST LOG-LIKELIHOOD: -2709.517
UPDATE BEST LOG-LIKELIHOOD: -2709.517
UPDATE BEST LOG-LIKELIHOOD: -2709.517
Iteration 100 / LogL: -2709.518 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 110 / LogL: -2713.720 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 120 / LogL: -2709.517 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 130 / LogL: -2709.517 / Time: 0h:0m:2s (0h:0m:0s left)
TREE SEARCH COMPLETED AFTER 132 ITERATIONS / Time: 0h:0m:2s

> --------------------------------------------------------------------
|                    FINALIZING TREE SEARCH
           |
> --------------------------------------------------------------------
> Performs final model parameters optimization
Estimate model parameters (epsilon = 0.010)
1. Initial log-likelihood: -2709.517
Optimal log-likelihood: -2709.517
Proportion of invariable sites: 0.818
Parameters optimization took 1 rounds (0.011 sec)
BEST SCORE FOUND : -2709.517
Total tree length: 0.102

> Total number of iterations: 132
CPU time used for tree search: 2.422 sec (0h:0m:2s)
Wall-clock time used for tree search: 2.604 sec (0h:0m:2s)
Total CPU time used: 2.469 sec (0h:0m:2s)
Total wall-clock time used: 2.767 sec (0h:0m:2s)

> Analysis results written to:
  IQ-TREE report:                sequences-aligned-clustalw2.fasta.iqtree
  Maximum-likelihood tree:       sequences-aligned-clustalw2.fasta.treefile
  Likelihood distances:          sequences-aligned-clustalw2.fasta.mldist
  Screen log file:               sequences-aligned-clustalw2.fasta.log

> Date and Time: Mon May 09 17:31:21 2022

##### Trees were visualized using iTOL, the free website. They were downloaded into the figures directory under the name "ML-tree-ALIGNMENT METHOD (MUSCLE or clustalw2)-aligned.pdf"

# Bayesian Implementation


I will be using MrBayes for bayesian implementation. 

##### Create MrBayes block in a separate text file called mbblock.txt
'''
begin mrbayes;
 set autoclose=yes;
 prset brlenspr=unconstrained:exp(10.0);
 prset shapepr=exp(1.0);
 prset statefreqpr=dirichlet(1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0,1.0);
 lset nst=2 rates=gamma ngammacat=4;
 mcmcp ngen=10000 samplefreq=10 printfreq=100 nruns=1 nchains=3 savebrlens=yes;
 mcmc;
 sumt;
end;
'''

##### Copy and paste MUSCLE and Clustalw2 aligned sequences into MrBayes directory. Use MEGA-X software to export both fasta files into nexus files, which are inputs for MrBayes. Open one file -> analyze -> Data -> Export sequences -> NEXUS. (Make sure to send file to MrBayes directory under original name with .nexus) Repeat for second file. Change to MrBayes directory and append the MrBayes block to the aligned sequence files. In order to do this with the MUSCLE aligned sequences, I needed to shorten the names of the taxa including everything from "NADH" to the actual species name in each of the 20 sequences. Also needed to remove phrases from sequence names such as "PREDICTED:" and "RecName:"

'''
cd ../MrBayes/MrBayes
cat sequences-aligned-clustalw2.nexus mbblock.txt > sequences-aligned-clustalw2-mb.nexus
cat sequences-aligned-MUSCLE.nexus mbblock.txt > sequences-aligned-MUSCLE-mb.nexus
'''

##### Run MrBayes with both new files
mb sequences-aligned-clustalw2-mb.nexus

Executing file "sequences-aligned-clustalw2-mb.nexus"
   DOS line termination
   Longest line length = 761
   Parsing file
   Expecting NEXUS formatted file
   Reading taxa block
      Allocated taxon set
      Defining new set of 20 taxa
   Exiting taxa block
   Reading characters block
      Allocated matrix
      Defining new character matrix with 741 characters
      Missing data coded as ?
      Gaps coded as -
      Matching characters coded as .
      Data is Protein
      Taxon  1 -> XP_002749725.2
      Taxon  2 -> XP_032134401.1
      Taxon  3 -> XP_039325526.1
      Taxon  4 -> PNI67080.1
      Taxon  5 -> XP_008972488.1
      Taxon  6 -> NP_001266520.1
      Taxon  7 -> PNJ73451.1
      Taxon  8 -> P0CB68.1
      Taxon  9 -> XP_032610702.1
      Taxon 10 -> XP_030659807.1
      Taxon 11 -> Q4R6K9.1
      Taxon 12 -> XP_025261308.1
      Taxon 13 -> XP_003907894.1
      Taxon 14 -> XP_010350948.1
      Taxon 15 -> XP_033086464.1
      Taxon 16 -> XP_011805264.1
      Taxon 17 -> XP_023075176.1
      Taxon 18 -> XP_015990567.2
      Taxon 19 -> XP_006921444.1
      Taxon 20 -> XP_011224853.1
      Successfully read matrix
      Setting default partition (does not divide up characters)
      Setting model defaults
      Seed (for generating default start values) = 1652144653
      Setting output file names to "sequences-aligned-clustalw2-mb.nexus.run<i>.<p|t>"
   Exiting characters block
   Reading mrbayes block
      Setting autoclose to yes
      Setting Brlenspr to Unconstrained:Exponential(10.00)
      Successfully set prior model parameters
      Setting Shapepr to Exponential(1.00)
      Successfully set prior model parameters
      Setting Statefreqpr to Dirichlet(1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00)
      Successfully set prior model parameters
      Nst =1 unchanged because dataType is not DNA or RNA
      Setting Rates to Gamma
      Setting Ngammacat to 4
      Successfully set likelihood model parameters
      Setting number of generations to 10000
      Setting sample frequency to 10
      Setting print frequency to 100
      WARNING: Reallocation of zero size attempted. This is probably a bug. Problems may follow.
      WARNING: Reallocation of zero size attempted. This is probably a bug. Problems may follow.
      Setting number of runs to 1
      WARNING: Allocation of zero size attempted. This is probably a bug; problems may follow.
      Setting number of chains to 3
      Setting chain output file names to "sequences-aligned-clustalw2-mb.nexus.<p/t>"
      Successfully set chain parameters
      Running Markov chain
      MCMC stamp = 2380591072
      Seed = 444786498
      Swapseed = 1652144653
      Model settings:

         Data not partitioned --
            Datatype  = Protein
            Aamodel   = Poisson
                        Substitution rates are fixed to be equal
            Covarion  = No
            # States  = 20
                        State frequencies are fixed to be equal
            Rates     = Gamma
                        The distribution is approximated using 4 categories.
                        Shape parameter is exponentially
                        distributed with parameter (1.00).

      Active parameters:

         Parameters
         ---------------------
         Statefreq           1
         Shape               2
         Ratemultiplier      3
         Topology            4
         Brlens              5
         ---------------------

         1 --  Parameter  = Pi
               Type       = Stationary state frequencies
               Prior      = Fixed (equal frequencies)

         2 --  Parameter  = Alpha
               Type       = Shape of scaled gamma distribution of site rates
               Prior      = Exponential(1.00)

         3 --  Parameter  = Ratemultiplier
               Type       = Partition-specific rate multiplier
               Prior      = Fixed(1.0)

         4 --  Parameter  = Tau
               Type       = Topology
               Prior      = All topologies equally probable a priori
               Subparam.  = V

         5 --  Parameter  = V
               Type       = Branch lengths
               Prior      = Unconstrained:Exponential(10.0)



      The MCMC sampler will use the following moves:
         With prob.  Chain will use move
            1.96 %   Multiplier(Alpha)
            9.80 %   ExtSPR(Tau,V)
            9.80 %   ExtTBR(Tau,V)
            9.80 %   NNI(Tau,V)
            9.80 %   ParsSPR(Tau,V)
           39.22 %   Multiplier(V)
           13.73 %   Nodeslider(V)
            5.88 %   TLMultiplier(V)

      Division 1 has 83 unique site patterns
      Initializing conditional likelihoods
      Using standard non-SSE likelihood calculator for division 1 (single-precision)

      Initial log likelihoods and log prior probs:
         Chain 1 -- -3447.391078 -- 29.948048
         Chain 2 -- -3431.369724 -- 29.948048
         Chain 3 -- -3443.422600 -- 29.948048


      Chain results (10000 generations requested):

          0 -- [-3447.391] (-3431.370) (-3443.423)
        100 -- (-3203.378) (-3145.626) [-3071.734] -- 0:00:00
        200 -- (-3138.762) (-3049.656) [-2998.909] -- 0:00:00
        300 -- (-3087.826) (-3022.145) [-2934.907] -- 0:00:32
        400 -- (-3070.174) (-2972.479) [-2926.922] -- 0:00:24
        500 -- (-3051.897) (-2954.022) [-2918.006] -- 0:00:19
        600 -- (-2982.448) (-2943.887) [-2915.282] -- 0:00:15
        700 -- (-2977.358) (-2942.281) [-2911.227] -- 0:00:26
        800 -- (-2970.503) (-2920.651) [-2897.664] -- 0:00:23
        900 -- (-2960.689) (-2925.585) [-2904.571] -- 0:00:20
       1000 -- (-2956.478) (-2901.239) [-2898.607] -- 0:00:18
       1100 -- (-2943.061) (-2899.490) [-2895.676] -- 0:00:16
       1200 -- (-2925.308) (-2900.705) [-2897.234] -- 0:00:22
       1300 -- (-2919.181) (-2905.951) [-2892.286] -- 0:00:20
       1400 -- (-2912.759) (-2900.041) [-2891.701] -- 0:00:18
       1500 -- (-2901.447) (-2905.908) [-2897.899] -- 0:00:22
       1600 -- [-2897.313] (-2909.459) (-2910.712) -- 0:00:21
       1700 -- (-2902.809) (-2903.784) [-2897.153] -- 0:00:19
       1800 -- [-2901.215] (-2900.149) (-2895.941) -- 0:00:22
       1900 -- (-2901.399) [-2898.880] (-2900.476) -- 0:00:21
       2000 -- [-2899.565] (-2903.246) (-2905.301) -- 0:00:20
       2100 -- (-2904.187) [-2902.233] (-2908.990) -- 0:00:18
       2200 -- (-2901.564) [-2906.997] (-2903.849) -- 0:00:21
       2300 -- [-2900.091] (-2907.612) (-2909.340) -- 0:00:20
       2400 -- [-2904.171] (-2913.834) (-2897.550) -- 0:00:19
       2500 -- [-2887.359] (-2914.405) (-2898.646) -- 0:00:18
       2600 -- (-2902.978) (-2908.095) [-2895.599] -- 0:00:19
       2700 -- (-2912.420) [-2901.331] (-2898.169) -- 0:00:18
       2800 -- [-2901.860] (-2903.213) (-2893.262) -- 0:00:18
       2900 -- (-2893.927) [-2901.625] (-2921.416) -- 0:00:17
       3000 -- (-2909.322) [-2903.930] (-2913.381) -- 0:00:18
       3100 -- (-2911.274) (-2901.080) [-2906.888] -- 0:00:17
       3200 -- [-2917.037] (-2897.076) (-2914.303) -- 0:00:17
       3300 -- (-2902.127) [-2896.673] (-2903.737) -- 0:00:18
       3400 -- [-2902.271] (-2905.703) (-2916.919) -- 0:00:17
       3500 -- [-2891.609] (-2896.783) (-2914.372) -- 0:00:16
       3600 -- [-2901.497] (-2907.363) (-2921.615) -- 0:00:17
       3700 -- (-2896.501) [-2898.093] (-2904.163) -- 0:00:17
       3800 -- (-2900.326) [-2890.092] (-2911.180) -- 0:00:17
       3900 -- (-2900.787) [-2890.108] (-2903.201) -- 0:00:17
       4000 -- (-2899.527) [-2896.887] (-2913.365) -- 0:00:16
       4100 -- (-2901.410) (-2894.666) [-2895.370] -- 0:00:17
       4200 -- (-2895.538) [-2891.738] (-2903.689) -- 0:00:16
       4300 -- [-2896.945] (-2908.828) (-2903.852) -- 0:00:15
       4400 -- [-2894.652] (-2906.625) (-2903.182) -- 0:00:16
       4500 -- (-2898.890) (-2897.872) [-2897.863] -- 0:00:17
       4600 -- [-2902.565] (-2894.465) (-2894.423) -- 0:00:16
       4700 -- (-2929.581) [-2896.141] (-2891.066) -- 0:00:16
       4800 -- [-2904.808] (-2894.871) (-2897.012) -- 0:00:16
       4900 -- (-2915.900) [-2891.043] (-2901.435) -- 0:00:15
       5000 -- (-2918.304) (-2896.252) [-2901.370] -- 0:00:16
       5100 -- [-2899.138] (-2902.799) (-2893.520) -- 0:00:15
       5200 -- (-2904.277) [-2895.283] (-2894.701) -- 0:00:14
       5300 -- (-2906.372) [-2896.275] (-2906.761) -- 0:00:15
       5400 -- (-2902.793) (-2893.753) [-2894.200] -- 0:00:14
       5500 -- (-2911.737) [-2898.834] (-2899.710) -- 0:00:14
       5600 -- (-2909.835) (-2900.876) [-2896.282] -- 0:00:14
       5700 -- (-2905.703) (-2898.637) [-2897.890] -- 0:00:14
       5800 -- (-2900.002) (-2905.043) [-2888.399] -- 0:00:13
       5900 -- (-2905.343) (-2904.851) [-2889.113] -- 0:00:13
       6000 -- (-2905.021) (-2904.331) [-2899.267] -- 0:00:13
       6100 -- (-2920.486) [-2899.467] (-2900.647) -- 0:00:13
       6200 -- [-2890.093] (-2916.948) (-2900.153) -- 0:00:12
       6300 -- (-2916.330) (-2930.068) [-2897.102] -- 0:00:12
       6400 -- [-2900.142] (-2902.543) (-2894.546) -- 0:00:12
       6500 -- [-2889.366] (-2902.223) (-2909.083) -- 0:00:11
       6600 -- (-2892.552) [-2901.636] (-2901.535) -- 0:00:11
       6700 -- [-2899.834] (-2898.559) (-2913.702) -- 0:00:11
       6800 -- [-2901.817] (-2907.569) (-2906.562) -- 0:00:10
       6900 -- [-2899.297] (-2904.268) (-2898.044) -- 0:00:10
       7000 -- (-2916.206) (-2891.895) [-2903.363] -- 0:00:10
       7100 -- (-2909.625) [-2901.909] (-2902.906) -- 0:00:10
       7200 -- (-2906.780) (-2919.118) [-2906.894] -- 0:00:09
       7300 -- (-2910.976) [-2899.759] (-2902.340) -- 0:00:09
       7400 -- (-2901.622) (-2901.039) [-2895.023] -- 0:00:08
       7500 -- [-2900.184] (-2903.671) (-2900.410) -- 0:00:08
       7600 -- [-2902.921] (-2895.128) (-2895.640) -- 0:00:08
       7700 -- (-2905.771) (-2899.342) [-2891.427] -- 0:00:08
       7800 -- (-2902.684) (-2899.594) [-2888.272] -- 0:00:07
       7900 -- (-2893.907) [-2900.439] (-2912.304) -- 0:00:07
       8000 -- (-2890.377) [-2904.191] (-2914.526) -- 0:00:06
       8100 -- [-2895.925] (-2898.714) (-2899.928) -- 0:00:06
       8200 -- (-2900.598) (-2896.014) [-2902.317] -- 0:00:06
       8300 -- (-2894.125) (-2904.740) [-2897.937] -- 0:00:05
       8400 -- [-2895.418] (-2897.624) (-2898.691) -- 0:00:05
       8500 -- (-2894.493) (-2890.173) [-2895.029] -- 0:00:05
       8600 -- (-2897.036) (-2902.854) [-2890.297] -- 0:00:04
       8700 -- (-2892.208) (-2908.880) [-2896.010] -- 0:00:04
       8800 -- (-2891.184) (-2912.111) [-2891.879] -- 0:00:04
       8900 -- (-2899.961) [-2901.905] (-2892.602) -- 0:00:03
       9000 -- [-2895.140] (-2910.247) (-2902.787) -- 0:00:03
       9100 -- (-2895.209) [-2906.508] (-2899.977) -- 0:00:03
       9200 -- (-2900.764) (-2903.250) [-2895.906] -- 0:00:02
       9300 -- (-2901.886) [-2897.475] (-2899.333) -- 0:00:02
       9400 -- (-2903.971) (-2896.277) [-2894.536] -- 0:00:02
       9500 -- (-2902.498) [-2896.619] (-2911.116) -- 0:00:01
       9600 -- (-2896.303) (-2907.721) [-2900.613] -- 0:00:01
       9700 -- [-2891.318] (-2912.745) (-2896.420) -- 0:00:01
       9800 -- (-2908.679) (-2895.056) [-2891.776] -- 0:00:00
       9900 -- (-2897.314) [-2901.919] (-2897.424) -- 0:00:00
      10000 -- (-2897.215) [-2892.232] (-2898.638) -- 0:00:00

      Analysis completed in 36 seconds
      Analysis used 35.70 seconds of CPU time
      Log likelihood of best state for "cold" chain was -2883.18

      Acceptance rates for the moves in the "cold" chain:
         With prob.   (last 100)   chain accepted proposals by move
            86.1 %     ( 93 %)     Multiplier(Alpha)
            16.3 %     ( 23 %)     ExtSPR(Tau,V)
            13.6 %     ( 11 %)     ExtTBR(Tau,V)
            24.9 %     ( 24 %)     NNI(Tau,V)
            16.2 %     ( 16 %)     ParsSPR(Tau,V)
            76.0 %     ( 65 %)     Multiplier(V)
            58.8 %     ( 57 %)     Nodeslider(V)
            29.0 %     ( 33 %)     TLMultiplier(V)

      Chain swap information:

                 1     2     3
           --------------------
         1 |        0.64  0.37
         2 |  3354        0.60
         3 |  3343  3303

      Upper diagonal: Proportion of successful state exchanges between chains
      Lower diagonal: Number of attempted state exchanges between chains

      Chain information:

        ID -- Heat
       -----------
         1 -- 1.00  (cold chain)
         2 -- 0.91
         3 -- 0.83

      Heat = 1 / (1 + T * (ID - 1))
         (where T = 0.10 is the temperature and ID is the chain number)

      Summarizing trees in file "sequences-aligned-clustalw2-mb.nexus.t"
      Using relative burnin ('relburnin=yes'), discarding the first 25 % of sampled trees
      Writing statistics to files sequences-aligned-clustalw2-mb.nexus.<parts|tstat|vstat|trprobs|con>
      Examining file ...
      Found one tree block in file "sequences-aligned-clustalw2-mb.nexus.t" with 1001 trees in last block

      Tree reading status:

      0      10      20      30      40      50      60      70      80      90     100
      v-------v-------v-------v-------v-------v-------v-------v-------v-------v-------v
      *********************************************************************************

      Read 1001 trees from last tree block (sampling 751 of them)

      General explanation:

      In an unrooted tree, a taxon bipartition (split) is specified by removing a
      branch, thereby dividing the species into those to the left and those to the
      right of the branch. Here, taxa to one side of the removed branch are denoted
      '.' and those to the other side are denoted '*'. Specifically, the '.' symbol
      is used for the taxa on the same side as the outgroup.

      In a rooted or clock tree, the tree is rooted using the model and not by
      reference to an outgroup. Each bipartition therefore corresponds to a clade,
      that is, a group that includes all the descendants of a particular branch in
      the tree.  Taxa that are included in each clade are denoted using '*', and
      taxa that are not included are denoted using the '.' symbol.

      The output first includes a key to all the bipartitions with frequency larger
      or equual to (Minpartfreq) in at least one run. Minpartfreq is a parameter to
      sumt command and currently it is set to 0.10.  This is followed by a table
      with statistics for the informative bipartitions (those including at least
      two taxa), sorted from highest to lowest probability. For each bipartition,
      the table gives the number of times the partition or split was observed in all
      runs (#obs) and the posterior probability of the bipartition (Probab.), which
      is the same as the split frequency. If several runs are summarized, this is
      followed by the minimum split frequency (Min(s)), the maximum frequency
      (Max(s)), and the standard deviation of frequencies (Stddev(s)) across runs.
      The latter value should approach 0 for all bipartitions as MCMC runs converge.

      This is followed by a table summarizing branch lengths, node heights (if a
      clock model was used) and relaxed clock parameters (if a relaxed clock model
      was used). The mean, variance, and 95 % credible interval are given for each
      of these parameters. If several runs are summarized, the potential scale
      reduction factor (PSRF) is also given; it should approach 1 as runs converge.
      Node heights will take calibration points into account, if such points were
      used in the analysis.

      Note that Stddev may be unreliable if the partition is not present in all
      runs (the last column indicates the number of runs that sampled the partition
      if more than one run is summarized). The PSRF is not calculated at all if
      the partition is not present in all runs.The PSRF is also sensitive to small
      sample sizes and it should only be considered a rough guide to convergence
      since some of the assumptions allowing one to interpret it as a true potential
      scale reduction factor are violated in MrBayes.

      List of taxa in bipartitions:

         1 -- XP_002749725.2
         2 -- XP_032134401.1
         3 -- XP_039325526.1
         4 -- PNI67080.1
         5 -- XP_008972488.1
         6 -- NP_001266520.1
         7 -- PNJ73451.1
         8 -- P0CB68.1
         9 -- XP_032610702.1
        10 -- XP_030659807.1
        11 -- Q4R6K9.1
        12 -- XP_025261308.1
        13 -- XP_003907894.1
        14 -- XP_010350948.1
        15 -- XP_033086464.1
        16 -- XP_011805264.1
        17 -- XP_023075176.1
        18 -- XP_015990567.2
        19 -- XP_006921444.1
        20 -- XP_011224853.1

      Key to taxon bipartitions (saved to file "sequences-aligned-clustalw2-mb.nexus.parts"):

      ID -- Partition
      --------------------------
       1 -- .*******************
       2 -- .*..................
       3 -- ..*.................
       4 -- ...*................
       5 -- ....*...............
       6 -- .....*..............
       7 -- ......*.............
       8 -- .......*............
       9 -- ........*...........
      10 -- .........*..........
      11 -- ..........*.........
      12 -- ...........*........
      13 -- ............*.......
      14 -- .............*......
      15 -- ..............*.....
      16 -- ...............*....
      17 -- ................*...
      18 -- .................*..
      19 -- ..................*.
      20 -- ...................*
      21 -- ........**..........
      22 -- ......**............
      23 -- .................**.
      24 -- .................***
      25 -- .............****...
      26 -- ...**...............
      27 -- ...*****************
      28 -- .............***....
      29 -- .............**.....
      30 -- ..........*******...
      31 -- ...*****............
      32 -- ...*******..........
      33 -- ..........**********
      34 -- ..******************
      35 -- ...***..............
      36 -- .*.*****************
      37 -- ...**.**............
      38 -- ..........*.*****...
      39 -- ...**************...
      40 -- ..........**........
      41 -- ..........*..****...
      42 -- ............*****...
      43 -- ...........******...
      44 -- ..........**.****...
      45 -- ..........*.*.......
      46 -- ..........***.......
      47 -- ...........*.****...
      48 -- ........************
      49 -- .....***............
      50 -- ...........**.......
      51 -- ...*******.......***
      --------------------------

      Summary statistics for informative taxon bipartitions
         (saved to file "sequences-aligned-clustalw2-mb.nexus.tstat"):

      ID   #obs    Probab.
      --------------------
      21   751    1.000000
      22   751    1.000000
      23   751    1.000000
      24   751    1.000000
      25   751    1.000000
      26   751    1.000000
      27   751    1.000000
      28   749    0.997337
      29   748    0.996005
      30   731    0.973369
      31   618    0.822903
      32   521    0.693742
      33   469    0.624501
      34   443    0.589880
      35   370    0.492676
      36   307    0.408788
      37   246    0.327563
      38   179    0.238349
      39   168    0.223702
      40   159    0.211718
      41   153    0.203728
      42   153    0.203728
      43   148    0.197071
      44   148    0.197071
      45   142    0.189081
      46   142    0.189081
      47   141    0.187750
      48   140    0.186418
      49   135    0.179760
      50   128    0.170439
      51   106    0.141145
      --------------------

      Summary statistics for branch and node parameters
         (saved to file "sequences-aligned-clustalw2-mb.nexus.vstat"):

                                              95% HPD Interval
                                            --------------------
      Parameter      Mean       Variance     Lower       Upper       Median
      ---------------------------------------------------------------------
      length[1]     0.006932    0.000016    0.000698    0.015378    0.006109
      length[2]     0.009726    0.000017    0.004208    0.018085    0.008857
      length[3]     0.006811    0.000012    0.000830    0.014114    0.006464
      length[4]     0.003257    0.000005    0.000497    0.007688    0.002819
      length[5]     0.001410    0.000002    0.000044    0.003892    0.000913
      length[6]     0.001719    0.000003    0.000039    0.005598    0.001126
      length[7]     0.001984    0.000005    0.000056    0.006938    0.001247
      length[8]     0.001853    0.000002    0.000075    0.004818    0.001372
      length[9]     0.005494    0.000010    0.000789    0.012150    0.004617
      length[10]    0.003389    0.000005    0.000287    0.007197    0.002812
      length[11]    0.002939    0.000004    0.000200    0.006532    0.002470
      length[12]    0.002954    0.000005    0.000037    0.006863    0.002376
      length[13]    0.001381    0.000002    0.000010    0.004443    0.000977
      length[14]    0.004017    0.000008    0.000801    0.011022    0.003140
      length[15]    0.005081    0.000008    0.001051    0.010941    0.004793
      length[16]    0.003571    0.000007    0.000170    0.008795    0.003055
      length[17]    0.003258    0.000004    0.000035    0.006954    0.002838
      length[18]    0.003302    0.000005    0.000417    0.007980    0.002684
      length[19]    0.009060    0.000014    0.002780    0.016558    0.008501
      length[20]    0.017553    0.000041    0.007991    0.032086    0.017065
      length[21]    0.006211    0.000012    0.000934    0.012881    0.005489
      length[22]    0.007496    0.000012    0.001514    0.013452    0.007046
      length[23]    0.016866    0.000037    0.006901    0.028468    0.016408
      length[24]    0.011094    0.000025    0.003604    0.021612    0.009921
      length[25]    0.003732    0.000006    0.000044    0.007953    0.003245
      length[26]    0.006259    0.000011    0.001099    0.012543    0.005766
      length[27]    0.010181    0.000015    0.002903    0.017930    0.009594
      length[28]    0.003541    0.000006    0.000119    0.009003    0.002773
      length[29]    0.003126    0.000005    0.000287    0.009430    0.002486
      length[30]    0.004397    0.000010    0.000027    0.010995    0.004005
      length[31]    0.004891    0.000013    0.000360    0.012191    0.004159
      length[32]    0.005055    0.000014    0.000062    0.012073    0.004648
      length[33]    0.004890    0.000013    0.000040    0.012661    0.003954
      length[34]    0.003522    0.000007    0.000238    0.009115    0.002770
      length[35]    0.002913    0.000006    0.000174    0.008505    0.002249
      length[36]    0.003579    0.000005    0.000669    0.008399    0.003119
      length[37]    0.002183    0.000002    0.000305    0.005454    0.002118
      length[38]    0.002374    0.000005    0.000018    0.006497    0.001854
      length[39]    0.002755    0.000005    0.000025    0.006452    0.002150
      length[40]    0.001459    0.000002    0.000062    0.003855    0.001082
      length[41]    0.002398    0.000006    0.000072    0.007781    0.001606
      length[42]    0.001444    0.000002    0.000060    0.004631    0.000859
      length[43]    0.001627    0.000003    0.000018    0.005111    0.001192
      length[44]    0.001658    0.000002    0.000057    0.004006    0.001208
      length[45]    0.001666    0.000003    0.000019    0.004865    0.000788
      length[46]    0.001516    0.000003    0.000018    0.004767    0.000976
      length[47]    0.001757    0.000003    0.000089    0.005471    0.001499
      length[48]    0.002908    0.000005    0.000049    0.006438    0.002757
      length[49]    0.001888    0.000002    0.000115    0.004227    0.001846
      length[50]    0.001186    0.000001    0.000055    0.002747    0.000861
      length[51]    0.002786    0.000005    0.000025    0.007800    0.002519
      ---------------------------------------------------------------------




      Clade credibility values:

      /----------------------------------------------------------- XP_002749725.2 (1)
      |
      |----------------------------------------------------------- XP_032134401.1 (2)
      |
      |      /---------------------------------------------------- XP_039325526.1 (3)
      |      |
      |      |                                            /------- PNI67080.1 (4)
      +      |                                    /--100--+
      |      |                                    |       \------- XP_008972488.1 (5)
      |      |                                    |
      |      |                             /--82--+--------------- NP_001266520.1 (6)
      |      |                             |      |
      |      |                             |      |       /------- PNJ73451.1 (7)
      |      |                             |      \--100--+
      \--59--+       /----------69---------+              \------- P0CB68.1 (8)
             |       |                     |
             |       |                     |              /------- XP_032610702.1 (9)
             |       |                     \------100-----+
             |       |                                    \------- XP_030659807.1 (10)
             |       |
             |       |              /----------------------------- Q4R6K9.1 (11)
             |       |              |
             |       |              |----------------------------- XP_025261308.1 (12)
             \--100--+              |
                     |              |----------------------------- XP_003907894.1 (13)
                     |              |
                     |      /---97--+                     /------- XP_010350948.1 (14)
                     |      |       |             /--100--+
                     |      |       |             |       \------- XP_033086464.1 (15)
                     |      |       |      /--100-+
                     |      |       |      |      \--------------- XP_011805264.1 (16)
                     |      |       \--100-+
                     \--62--+              \---------------------- XP_023075176.1 (17)
                            |
                            |                             /------- XP_015990567.2 (18)
                            |                     /--100--+
                            |                     |       \------- XP_006921444.1 (19)
                            \---------100---------+
                                                  \--------------- XP_011224853.1 (20)


      Phylogram (based on average branch lengths):

      /------- XP_002749725.2 (1)
      |
      |---------- XP_032134401.1 (2)
      |
      |  /-------- XP_039325526.1 (3)
      |  |
      |  |                           /--- PNI67080.1 (4)
      +  |                    /------+
      |  |                    |      \- XP_008972488.1 (5)
      |  |                    |
      |  |                /---+-- NP_001266520.1 (6)
      |  |                |   |
      |  |                |   |        /- PNJ73451.1 (7)
      |  |                |   \--------+
      \--+          /-----+            \- P0CB68.1 (8)
         |          |     |
         |          |     |     /----- XP_032610702.1 (9)
         |          |     \-----+
         |          |           \--- XP_030659807.1 (10)
         |          |
         |          |        /--- Q4R6K9.1 (11)
         |          |        |
         |          |        |--- XP_025261308.1 (12)
         \----------+        |
                    |        |-- XP_003907894.1 (13)
                    |        |
                    |    /---+         /---- XP_010350948.1 (14)
                    |    |   |      /--+
                    |    |   |      |  \------ XP_033086464.1 (15)
                    |    |   |   /--+
                    |    |   |   |  \---- XP_011805264.1 (16)
                    |    |   \---+
                    \----+       \--- XP_023075176.1 (17)
                         |
                         |                             /--- XP_015990567.2 (18)
                         |          /------------------+
                         |          |                  \---------- XP_006921444.1 (19)
                         \----------+
                                    \-------------------- XP_011224853.1 (20)

      |----------| 0.010 expected changes per site

      Calculating tree probabilities...

      Credible sets of trees (350 trees sampled):
         50 % credible set contains 83 trees
         90 % credible set contains 275 trees
         95 % credible set contains 313 trees
         99 % credible set contains 343 trees

   Exiting mrbayes block
   Reached end of file

mb sequences-aligned-MUSCLE-mb.nexus

Executing file "sequences-aligned-MUSCLE-mb.nexus"
   DOS line termination
   Longest line length = 801
   Parsing file
   Expecting NEXUS formatted file
   Reading taxa block
      Allocated taxon set
      Defining new set of 20 taxa
      Expecting '<name> or <number>'
      Instead found ':' in command 'Taxlabels'
      The error occurred when reading char. 30-30 on line 15
         in the file 'sequences-aligned-MUSCLE-mb.nexus'

   Returning execution to command line ...

   Error in command "Execute"

MrBayes > execute sequences-aligned-MUSCLE-mb.nexus

   Executing file "sequences-aligned-MUSCLE-mb.nexus"
   DOS line termination
   Longest line length = 793
   Parsing file
   Expecting NEXUS formatted file
   Deleting previously defined taxa
   Reading taxa block
      Allocated taxon set
      Defining new set of 20 taxa
   Exiting taxa block
   Reading characters block
      Allocated matrix
      Defining new character matrix with 741 characters
      Missing data coded as ?
      Gaps coded as -
      Matching characters coded as .
      Data is Protein
      Taxon  1 -> XP_025261308.1_Theropithecus_gelada
      Taxon  2 -> XP_032134401.1_Sapajus_apella
      Taxon  3 -> XP_015990567.2_Rousettus_aegyptiacus
      Taxon  4 -> PNI67080.1_Pan_troglodytes
      Taxon  5 -> XP_011224853.1_Ailuropoda_melanoleuca
      Taxon  6 -> XP_033086464.1_Trachypithecus_francoisi
      Taxon  7 -> PNJ73451.1_Pongo_abelii
      Taxon  8 -> XP_011805264.1_Colobus_angolensis_palliatus
      Taxon  9 -> XP_023075176.1_Piliocolobus_tephrosceles
      Taxon 10 -> P0CB68.1_Pongo_pygmaeus
      Taxon 11 -> XP_030659807.1_Nomascus_leucogenys
      Taxon 12 -> NP_001266520.1_Gorilla_gorilla
      Taxon 13 -> XP_032610702.1_Hylobates_moloch
      Taxon 14 -> XP_002749725.2_Callithrix_jacchus
      Taxon 15 -> XP_008972488.1_Pan_paniscus
      Taxon 16 -> XP_003907894.1_Papio_anubis
      Taxon 17 -> XP_006921444.1_Pteropus_alecto
      Taxon 18 -> XP_039325526.1_Saimiri_boliviensis_boliviensis
      Taxon 19 -> XP_010350948.1_Rhinopithecus_roxellana
      Taxon 20 -> Q4R6K9.1_Macaca_fascicularis
      Successfully read matrix
      Setting default partition (does not divide up characters)
      Setting model defaults
      Seed (for generating default start values) = 1652145503
      Setting output file names to "sequences-aligned-MUSCLE-mb.nexus.run<i>.<p|t>"
   Exiting characters block
   Reading mrbayes block
      Setting autoclose to yes
      Setting Brlenspr to Unconstrained:Exponential(10.00)
      Successfully set prior model parameters
      Setting Shapepr to Exponential(1.00)
      Successfully set prior model parameters
      Setting Statefreqpr to Dirichlet(1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00,1.00)
      Successfully set prior model parameters
      Nst =1 unchanged because dataType is not DNA or RNA
      Setting Rates to Gamma
      Setting Ngammacat to 4
      Successfully set likelihood model parameters
      Setting number of generations to 10000
      Setting sample frequency to 10
      Setting print frequency to 100
      WARNING: Reallocation of zero size attempted. This is probably a bug. Problems may follow.
      WARNING: Reallocation of zero size attempted. This is probably a bug. Problems may follow.
      Setting number of runs to 1
      WARNING: Allocation of zero size attempted. This is probably a bug; problems may follow.
      Setting number of chains to 3
      Setting chain output file names to "sequences-aligned-MUSCLE-mb.nexus.<p/t>"
      Successfully set chain parameters
      Running Markov chain
      MCMC stamp = 3119401117
      Seed = 2003151243
      Swapseed = 1652145503
      Model settings:

         Data not partitioned --
            Datatype  = Protein
            Aamodel   = Poisson
                        Substitution rates are fixed to be equal
            Covarion  = No
            # States  = 20
                        State frequencies are fixed to be equal
            Rates     = Gamma
                        The distribution is approximated using 4 categories.
                        Shape parameter is exponentially
                        distributed with parameter (1.00).

      Active parameters:

         Parameters
         ---------------------
         Statefreq           1
         Shape               2
         Ratemultiplier      3
         Topology            4
         Brlens              5
         ---------------------

         1 --  Parameter  = Pi
               Type       = Stationary state frequencies
               Prior      = Fixed (equal frequencies)

         2 --  Parameter  = Alpha
               Type       = Shape of scaled gamma distribution of site rates
               Prior      = Exponential(1.00)

         3 --  Parameter  = Ratemultiplier
               Type       = Partition-specific rate multiplier
               Prior      = Fixed(1.0)

         4 --  Parameter  = Tau
               Type       = Topology
               Prior      = All topologies equally probable a priori
               Subparam.  = V

         5 --  Parameter  = V
               Type       = Branch lengths
               Prior      = Unconstrained:Exponential(10.0)



      The MCMC sampler will use the following moves:
         With prob.  Chain will use move
            1.96 %   Multiplier(Alpha)
            9.80 %   ExtSPR(Tau,V)
            9.80 %   ExtTBR(Tau,V)
            9.80 %   NNI(Tau,V)
            9.80 %   ParsSPR(Tau,V)
           39.22 %   Multiplier(V)
           13.73 %   Nodeslider(V)
            5.88 %   TLMultiplier(V)

      Division 1 has 84 unique site patterns
      Initializing conditional likelihoods
      Using standard non-SSE likelihood calculator for division 1 (single-precision)

      Initial log likelihoods and log prior probs:
         Chain 1 -- -3432.143405 -- 29.948048
         Chain 2 -- -3464.030252 -- 29.948048
         Chain 3 -- -3431.735416 -- 29.948048


      Chain results (10000 generations requested):

          0 -- [-3432.143] (-3464.030) (-3431.735)
        100 -- (-3193.345) (-3258.342) [-3121.840] -- 0:00:00
        200 -- (-3003.037) [-3004.716] (-3039.415) -- 0:00:00
        300 -- (-2992.362) [-2958.022] (-3001.248) -- 0:00:00
        400 -- (-2969.065) [-2936.972] (-2992.428) -- 0:00:24
        500 -- [-2932.930] (-2938.098) (-2935.835) -- 0:00:19
        600 -- (-2923.523) (-2942.777) [-2921.416] -- 0:00:15
        700 -- (-2914.294) (-2936.620) [-2900.912] -- 0:00:13
        800 -- (-2911.886) (-2918.463) [-2885.915] -- 0:00:11
        900 -- (-2907.886) (-2921.460) [-2878.418] -- 0:00:20
       1000 -- (-2909.551) (-2914.779) [-2881.344] -- 0:00:18
       1100 -- (-2912.057) (-2926.157) [-2889.929] -- 0:00:16
       1200 -- (-2909.493) (-2917.633) [-2878.693] -- 0:00:14
       1300 -- (-2915.499) (-2904.636) [-2884.133] -- 0:00:20
       1400 -- (-2911.178) (-2905.072) [-2884.603] -- 0:00:18
       1500 -- (-2916.308) (-2914.867) [-2884.100] -- 0:00:17
       1600 -- (-2913.819) (-2900.082) [-2874.119] -- 0:00:21
       1700 -- (-2913.307) (-2895.697) [-2874.850] -- 0:00:19
       1800 -- (-2901.077) [-2888.193] (-2877.086) -- 0:00:18
       1900 -- (-2899.945) (-2901.383) [-2884.155] -- 0:00:21
       2000 -- (-2897.171) [-2889.408] (-2887.931) -- 0:00:20
       2100 -- (-2892.890) [-2884.997] (-2884.818) -- 0:00:18
       2200 -- (-2905.422) (-2889.033) [-2878.183] -- 0:00:21
       2300 -- (-2910.103) (-2893.128) [-2874.843] -- 0:00:20
       2400 -- (-2897.358) (-2887.226) [-2875.983] -- 0:00:22
       2500 -- (-2895.601) [-2881.051] (-2885.880) -- 0:00:21
       2600 -- (-2902.954) [-2882.194] (-2882.380) -- 0:00:19
       2700 -- (-2880.496) (-2891.924) [-2878.149] -- 0:00:21
       2800 -- [-2884.532] (-2895.072) (-2889.099) -- 0:00:20
       2900 -- (-2888.468) [-2892.703] (-2894.697) -- 0:00:19
       3000 -- (-2898.068) [-2888.765] (-2892.219) -- 0:00:21
       3100 -- (-2902.110) (-2886.138) [-2892.126] -- 0:00:20
       3200 -- (-2893.029) [-2885.646] (-2896.767) -- 0:00:19
       3300 -- [-2892.700] (-2883.930) (-2875.576) -- 0:00:20
       3400 -- (-2898.409) (-2881.660) [-2876.863] -- 0:00:19
       3500 -- [-2889.832] (-2885.762) (-2888.726) -- 0:00:18
       3600 -- [-2893.856] (-2879.822) (-2908.392) -- 0:00:17
       3700 -- (-2885.340) (-2882.515) [-2890.120] -- 0:00:18
       3800 -- (-2879.563) [-2884.130] (-2898.235) -- 0:00:17
       3900 -- (-2875.233) (-2887.805) [-2890.179] -- 0:00:17
       4000 -- [-2878.675] (-2877.424) (-2880.445) -- 0:00:16
       4100 -- (-2877.581) (-2884.105) [-2877.978] -- 0:00:17
       4200 -- [-2876.824] (-2886.133) (-2899.011) -- 0:00:16
       4300 -- (-2882.421) (-2880.133) [-2884.285] -- 0:00:15
       4400 -- [-2885.440] (-2887.278) (-2899.570) -- 0:00:16
       4500 -- (-2895.229) (-2894.008) [-2889.290] -- 0:00:15
       4600 -- (-2886.777) [-2886.249] (-2879.659) -- 0:00:15
       4700 -- (-2889.084) (-2881.424) [-2883.523] -- 0:00:15
       4800 -- (-2891.862) [-2887.741] (-2892.950) -- 0:00:15
       4900 -- [-2892.134] (-2895.538) (-2890.222) -- 0:00:14
       5000 -- (-2901.568) (-2885.453) [-2894.448] -- 0:00:15
       5100 -- (-2907.681) [-2879.999] (-2881.881) -- 0:00:14
       5200 -- [-2901.842] (-2883.148) (-2887.013) -- 0:00:13
       5300 -- (-2890.461) [-2882.175] (-2891.156) -- 0:00:14
       5400 -- (-2895.424) (-2882.365) [-2880.272] -- 0:00:13
       5500 -- [-2882.909] (-2884.699) (-2884.447) -- 0:00:13
       5600 -- [-2885.047] (-2892.779) (-2883.220) -- 0:00:13
       5700 -- (-2886.822) (-2893.890) [-2885.505] -- 0:00:13
       5800 -- (-2886.742) (-2886.434) [-2885.083] -- 0:00:13
       5900 -- (-2902.436) (-2875.022) [-2880.853] -- 0:00:13
       6000 -- (-2886.387) (-2889.658) [-2884.135] -- 0:00:12
       6100 -- (-2883.457) (-2898.769) [-2875.707] -- 0:00:12
       6200 -- (-2882.099) (-2882.437) [-2876.176] -- 0:00:11
       6300 -- (-2883.635) [-2876.285] (-2875.392) -- 0:00:11
       6400 -- [-2884.788] (-2895.516) (-2884.020) -- 0:00:11
       6500 -- [-2881.170] (-2901.060) (-2890.883) -- 0:00:10
       6600 -- [-2876.976] (-2890.993) (-2883.975) -- 0:00:10
       6700 -- [-2881.064] (-2886.616) (-2886.840) -- 0:00:10
       6800 -- (-2883.720) (-2901.944) [-2872.753] -- 0:00:09
       6900 -- [-2884.399] (-2899.683) (-2892.097) -- 0:00:09
       7000 -- (-2887.606) (-2896.619) [-2886.683] -- 0:00:09
       7100 -- (-2897.638) (-2885.780) [-2890.101] -- 0:00:08
       7200 -- (-2890.881) [-2880.184] (-2907.962) -- 0:00:08
       7300 -- (-2889.410) [-2882.573] (-2894.803) -- 0:00:08
       7400 -- (-2884.470) [-2897.780] (-2899.357) -- 0:00:08
       7500 -- (-2891.094) (-2893.398) [-2877.057] -- 0:00:07
       7600 -- (-2888.455) [-2877.560] (-2884.618) -- 0:00:07
       7700 -- (-2882.999) [-2879.020] (-2892.912) -- 0:00:07
       7800 -- (-2897.085) (-2884.153) [-2885.069] -- 0:00:07
       7900 -- (-2873.771) [-2880.821] (-2893.680) -- 0:00:06
       8000 -- (-2873.076) [-2882.483] (-2891.433) -- 0:00:06
       8100 -- [-2883.308] (-2885.228) (-2886.165) -- 0:00:06
       8200 -- (-2887.893) [-2882.551] (-2889.288) -- 0:00:05
       8300 -- (-2890.073) [-2882.106] (-2898.918) -- 0:00:05
       8400 -- (-2883.916) [-2880.618] (-2886.179) -- 0:00:05
       8500 -- (-2895.453) [-2883.034] (-2892.880) -- 0:00:04
       8600 -- [-2884.080] (-2878.867) (-2897.989) -- 0:00:04
       8700 -- (-2900.985) (-2877.941) [-2889.356] -- 0:00:04
       8800 -- (-2897.797) [-2884.474] (-2885.924) -- 0:00:03
       8900 -- (-2885.074) (-2878.382) [-2879.535] -- 0:00:03
       9000 -- (-2881.448) (-2880.018) [-2882.276] -- 0:00:03
       9100 -- (-2884.996) [-2885.806] (-2888.279) -- 0:00:02
       9200 -- (-2893.923) [-2890.353] (-2885.691) -- 0:00:02
       9300 -- (-2886.020) [-2883.672] (-2893.984) -- 0:00:02
       9400 -- (-2890.000) (-2905.413) [-2877.139] -- 0:00:01
       9500 -- [-2890.736] (-2900.929) (-2891.920) -- 0:00:01
       9600 -- (-2889.298) (-2894.649) [-2884.731] -- 0:00:01
       9700 -- (-2894.943) [-2885.505] (-2874.587) -- 0:00:00
       9800 -- (-2883.527) (-2883.763) [-2879.391] -- 0:00:00
       9900 -- (-2890.487) (-2890.472) [-2883.704] -- 0:00:00
      10000 -- (-2888.698) [-2887.366] (-2891.747) -- 0:00:00

      Analysis completed in 32 seconds
      Analysis used 32.09 seconds of CPU time
      Log likelihood of best state for "cold" chain was -2871.49

      Acceptance rates for the moves in the "cold" chain:
         With prob.   (last 100)   chain accepted proposals by move
            85.1 %     ( 81 %)     Multiplier(Alpha)
            16.4 %     ( 15 %)     ExtSPR(Tau,V)
            15.4 %     ( 13 %)     ExtTBR(Tau,V)
            26.5 %     ( 30 %)     NNI(Tau,V)
            18.0 %     ( 16 %)     ParsSPR(Tau,V)
            77.1 %     ( 79 %)     Multiplier(V)
            61.7 %     ( 57 %)     Nodeslider(V)
            26.8 %     ( 26 %)     TLMultiplier(V)

      Chain swap information:

                 1     2     3
           --------------------
         1 |        0.61  0.37
         2 |  3393        0.68
         3 |  3320  3287

      Upper diagonal: Proportion of successful state exchanges between chains
      Lower diagonal: Number of attempted state exchanges between chains

      Chain information:

        ID -- Heat
       -----------
         1 -- 1.00  (cold chain)
         2 -- 0.91
         3 -- 0.83

      Heat = 1 / (1 + T * (ID - 1))
         (where T = 0.10 is the temperature and ID is the chain number)

      Summarizing trees in file "sequences-aligned-MUSCLE-mb.nexus.t"
      Using relative burnin ('relburnin=yes'), discarding the first 25 % of sampled trees
      Writing statistics to files sequences-aligned-MUSCLE-mb.nexus.<parts|tstat|vstat|trprobs|con>
      Examining file ...
      Found one tree block in file "sequences-aligned-MUSCLE-mb.nexus.t" with 1001 trees in last block

      Tree reading status:

      0      10      20      30      40      50      60      70      80      90     100
      v-------v-------v-------v-------v-------v-------v-------v-------v-------v-------v
      *********************************************************************************

      Read 1001 trees from last tree block (sampling 751 of them)

      General explanation:

      In an unrooted tree, a taxon bipartition (split) is specified by removing a
      branch, thereby dividing the species into those to the left and those to the
      right of the branch. Here, taxa to one side of the removed branch are denoted
      '.' and those to the other side are denoted '*'. Specifically, the '.' symbol
      is used for the taxa on the same side as the outgroup.

      In a rooted or clock tree, the tree is rooted using the model and not by
      reference to an outgroup. Each bipartition therefore corresponds to a clade,
      that is, a group that includes all the descendants of a particular branch in
      the tree.  Taxa that are included in each clade are denoted using '*', and
      taxa that are not included are denoted using the '.' symbol.

      The output first includes a key to all the bipartitions with frequency larger
      or equual to (Minpartfreq) in at least one run. Minpartfreq is a parameter to
      sumt command and currently it is set to 0.10.  This is followed by a table
      with statistics for the informative bipartitions (those including at least
      two taxa), sorted from highest to lowest probability. For each bipartition,
      the table gives the number of times the partition or split was observed in all
      runs (#obs) and the posterior probability of the bipartition (Probab.), which
      is the same as the split frequency. If several runs are summarized, this is
      followed by the minimum split frequency (Min(s)), the maximum frequency
      (Max(s)), and the standard deviation of frequencies (Stddev(s)) across runs.
      The latter value should approach 0 for all bipartitions as MCMC runs converge.

      This is followed by a table summarizing branch lengths, node heights (if a
      clock model was used) and relaxed clock parameters (if a relaxed clock model
      was used). The mean, variance, and 95 % credible interval are given for each
      of these parameters. If several runs are summarized, the potential scale
      reduction factor (PSRF) is also given; it should approach 1 as runs converge.
      Node heights will take calibration points into account, if such points were
      used in the analysis.

      Note that Stddev may be unreliable if the partition is not present in all
      runs (the last column indicates the number of runs that sampled the partition
      if more than one run is summarized). The PSRF is not calculated at all if
      the partition is not present in all runs.The PSRF is also sensitive to small
      sample sizes and it should only be considered a rough guide to convergence
      since some of the assumptions allowing one to interpret it as a true potential
      scale reduction factor are violated in MrBayes.

      List of taxa in bipartitions:

         1 -- XP_025261308.1_Theropithecus_gelada
         2 -- XP_032134401.1_Sapajus_apella
         3 -- XP_015990567.2_Rousettus_aegyptiacus
         4 -- PNI67080.1_Pan_troglodytes
         5 -- XP_011224853.1_Ailuropoda_melanoleuca
         6 -- XP_033086464.1_Trachypithecus_francoisi
         7 -- PNJ73451.1_Pongo_abelii
         8 -- XP_011805264.1_Colobus_angolensis_palliatus
         9 -- XP_023075176.1_Piliocolobus_tephrosceles
        10 -- P0CB68.1_Pongo_pygmaeus
        11 -- XP_030659807.1_Nomascus_leucogenys
        12 -- NP_001266520.1_Gorilla_gorilla
        13 -- XP_032610702.1_Hylobates_moloch
        14 -- XP_002749725.2_Callithrix_jacchus
        15 -- XP_008972488.1_Pan_paniscus
        16 -- XP_003907894.1_Papio_anubis
        17 -- XP_006921444.1_Pteropus_alecto
        18 -- XP_039325526.1_Saimiri_boliviensis_boliviensis
        19 -- XP_010350948.1_Rhinopithecus_roxellana
        20 -- Q4R6K9.1_Macaca_fascicularis

      Key to taxon bipartitions (saved to file "sequences-aligned-MUSCLE-mb.nexus.parts"):

      ID -- Partition
      --------------------------
       1 -- .*******************
       2 -- .*..................
       3 -- ..*.................
       4 -- ...*................
       5 -- ....*...............
       6 -- .....*..............
       7 -- ......*.............
       8 -- .......*............
       9 -- ........*...........
      10 -- .........*..........
      11 -- ..........*.........
      12 -- ...........*........
      13 -- ............*.......
      14 -- .............*......
      15 -- ..............*.....
      16 -- ...............*....
      17 -- ................*...
      18 -- .................*..
      19 -- ..................*.
      20 -- ...................*
      21 -- ......*..*..........
      22 -- .....*.**.........*.
      23 -- ..........*.*.......
      24 -- .....*.*..........*.
      25 -- ...*..........*.....
      26 -- ..*.............*...
      27 -- .*...........*...*..
      28 -- ..*.*...........*...
      29 -- .....*............*.
      30 -- .****.*..******.**..
      31 -- ...*.......*..*.....
      32 -- .*.*..*..******..*..
      33 -- ...*..*..*.*..*.....
      34 -- ...*..*..****.*.....
      35 -- .*...........*......
      36 -- .............*...*..
      37 -- .****.*..******.**.*
      38 -- .****.*..*********..
      39 -- .....*.**......*..**
      40 -- .****.*..*********.*
      41 -- .....*.**.........**
      42 -- ...*..*..*....*.....
      43 -- .....*.**......*..*.
      44 -- ...............*...*
      45 -- .**.*........*..**..
      46 -- .*.*..*..*.*.**..*..
      47 -- .**************.****
      48 -- .******************.
      49 -- ...*......***.*.....
      50 -- .**************.***.
      51 -- .*........*.**...*..
      52 -- ..***.*..****.*.*...
      53 -- ......*..*.*........
      --------------------------

      Summary statistics for informative taxon bipartitions
         (saved to file "sequences-aligned-MUSCLE-mb.nexus.tstat"):

      ID   #obs    Probab.
      --------------------
      21   751    1.000000
      22   751    1.000000
      23   751    1.000000
      24   751    1.000000
      25   751    1.000000
      26   751    1.000000
      27   751    1.000000
      28   751    1.000000
      29   738    0.982690
      30   730    0.972037
      31   520    0.692410
      32   502    0.668442
      33   480    0.639148
      34   433    0.576565
      35   378    0.503329
      36   370    0.492676
      37   183    0.243675
      38   174    0.231691
      39   167    0.222370
      40   162    0.215712
      41   154    0.205060
      42   148    0.197071
      43   148    0.197071
      44   148    0.197071
      45   147    0.195739
      46   130    0.173103
      47   121    0.161119
      48   119    0.158455
      49   111    0.147803
      50    98    0.130493
      51    91    0.121172
      52    89    0.118509
      53    77    0.102530
      --------------------

      Summary s  0.010089    0.003116
      length[4]     0.003449    0.000004    0.000384    0.007043    0.003070
      length[5]     0.017019    0.000042    0.007554    0.031530    0.015809
      length[6]     0.004676    0.000006    0.001051    0.009650    0.004387
      length[7]     0.001573    0.000002    0.000002    0.004162    0.001216
      length[8]     0.003981    0.000007    0.000142    0.009309    0.003389
      length[9]     0.003150    0.000005    0.000330    0.007947    0.002605
      length[10]    0.001764    0.000003    0.000003    0.004800    0.001401
      length[11]    0.002750    0.000004    0.000421    0.006513    0.002174
      length[12]    0.001918    0.000003    0.000065    0.005682    0.001419
      length[13]    0.004445    0.000009    0.000282    0.009556    0.003957
      length[14]    0.006091    0.000013    0.001037    0.012498    0.005211
      length[15]    0.002262    0.000004    0.000008    0.007065    0.001779
      length[16]    0.002147    0.000002    0.000050    0.004905    0.001859
      length[17]    0.009356    0.000015    0.003333    0.016365    0.008921
      length[18]    0.005304    0.000012    0.000644    0.012032    0.004722
      length[19]    0.002863    0.000004    0.000489    0.006687    0.002417
      length[20]    0.003136    0.000004    0.000166    0.006617    0.002839
      length[21]    0.006446    0.000011    0.001119    0.013196    0.005971
      length[22]    0.003587    0.000006    0.000517    0.008515    0.002997
      length[23]    0.004475    0.000005    0.000821    0.008823    0.004314
      length[24]    0.003679    0.000006    0.000228    0.008248    0.003048
      length[25]    0.005244    0.000010    0.000599    0.010422    0.004645
      length[26]    0.016042    0.000030    0.006119    0.026545    0.015647
      length[27]    0.010937    0.000023    0.004074    0.020566    0.010250
      length[28]    0.012318    0.000025    0.004411    0.022970    0.011404
      length[29]    0.002819    0.000004    0.000113    0.007175    0.002436
      length[30]    0.004252    0.000008    0.000597    0.009744    0.003590
      length[31]    0.002698    0.000004    0.000073    0.006260    0.002420
      length[32]    0.004153    0.000011    0.000167    0.010872    0.003694
      length[33]    0.003520    0.000007    0.000241    0.009737    0.002810
      length[34]    0.003185    0.000007    0.000030    0.007494    0.002503
      length[35]    0.003613    0.000006    0.000076    0.007292    0.003091
      length[36]    0.003426    0.000005    0.000060    0.008059    0.003044
      length[37]    0.001957    0.000003    0.000009    0.005219    0.001531
      length[38]    0.001954    0.000003    0.000051    0.004611    0.001436
      length[39]    0.002208    0.000006    0.000012    0.007370    0.001262
      length[40]    0.002244    0.000007    0.000016    0.009140    0.001290
      length[41]    0.001605    0.000003    0.000055    0.004710    0.001065
      length[42]    0.002902    0.000006    0.000074    0.006775    0.002261
      length[43]    0.001917    0.000003    0.000074    0.005307    0.001412
      length[44]    0.001670    0.000003    0.000091    0.005096    0.001173
      length[45]    0.002586    0.000006    0.000325    0.009570    0.001401
      length[46]    0.001295    0.000001    0.000007    0.003373    0.000859
      length[47]    0.001685    0.000002    0.000059    0.004162    0.001276
      length[48]    0.001789    0.000003    0.000102    0.004055    0.001371
      length[49]    0.001484    0.000002    0.000025    0.003295    0.001223
      length[50]    0.002062    0.000003    0.000018    0.005217    0.001601
      length[51]    0.000932    0.000001    0.000007    0.002560    0.000785
      length[52]    0.002968    0.000006    0.000104    0.008395    0.002431
      length[53]    0.002133    0.000002    0.000056    0.005268    0.001741
      ---------------------------------------------------------------------




       Clade credibility values:

      /---------------------------------------------------------- XP_025261308.1_~ (1)
      |
      |---------------------------------------------------------- XP_003907894.1~ (16)
      |
      |---------------------------------------------------------- Q4R6K9.1_Macac~ (20)
      |
      |                                                 /-------- XP_033086464.1_~ (6)
      |                                        /---98---+
      |                                        |        \-------- XP_010350948.1~ (19)
      |                                /--100--+
      |                                |       \----------------- XP_011805264.1_~ (8)
      |---------------100--------------+
      |                                \------------------------- XP_023075176.1_~ (9)
      |
      |                                                 /-------- XP_032134401.1_~ (2)
      +                                        /---50---+
      |                                        |        \-------- XP_002749725.2~ (14)
      |                /----------100----------+
      |                |                       \----------------- XP_039325526.1~ (18)
      |                |
      |                |                                /-------- PNI67080.1_Pan_~ (4)
      |                |                       /---100--+
      |                |                       |        \-------- XP_008972488.1~ (15)
      |       /---67---+               /---69--+
      |       |        |               |       \----------------- NP_001266520.1~ (12)
      |       |        |       /---64--+
      |       |        |       |       |                /-------- PNJ73451.1_Pong~ (7)
      |       |        |       |       \-------100------+
      |       |        \---58--+                        \-------- P0CB68.1_Pongo~ (10)
      |       |                |
      \---97--+                |                        /-------- XP_030659807.1~ (11)
              |                \-----------100----------+
              |                                         \-------- XP_032610702.1~ (13)
              |
              |                                         /-------- XP_015990567.2_~ (3)
              |                                /---100--+
              |                                |        \-------- XP_006921444.1~ (17)
              \---------------100--------------+
                                               \----------------- XP_011224853.1_~ (5)


      Phylogram (based on average branch lengths):

      /----- XP_025261308.1_~ (1)
      |
      |--- XP_003907894.1~ (16)
      |
      |---- Q4R6K9.1_Macac~ (20)
      |
      |           /------- XP_033086464.1_~ (6)
      |        /--+
      |        |  \---- XP_010350948.1~ (19)
      |   /----+
      |   |    \----- XP_011805264.1_~ (8)
      |---+
      |   \---- XP_023075176.1_~ (9)
      |
      |                             /------------- XP_032134401.1_~ (2)
      +                         /---+
      |                         |   \-------- XP_002749725.2~ (14)
      |          /--------------+
      |          |              \------- XP_039325526.1~ (18)
      |          |
      |          |                 /---- PNI67080.1_Pan_~ (4)
      |          |          /------+
      |          |          |      \-- XP_008972488.1~ (15)
      |    /-----+      /---+
      |    |     |      |   \-- NP_001266520.1~ (12)
      |    |     |  /---+
      |    |     |  |   |        /-- PNJ73451.1_Pong~ (7)
      |    |     |  |   \--------+
      |    |     \--+            \-- P0CB68.1_Pongo~ (10)
      |    |        |
      \----+        |      /--- XP_030659807.1~ (11)
           |        \------+
           |               \----- XP_032610702.1~ (13)
           |
           |                                       /---- XP_015990567.2_~ (3)
           |                /----------------------+
           |                |                      \------------- XP_006921444.1~ (17)
           \----------------+
                            \----------------------- XP_011224853.1_~ (5)

        |-------------| 0.010 expected changes per site

       Calculating tree probabilities...

       Credible sets of trees (385 trees sampled):
          50 % credible set contains 92 trees
          90 % credible set contains 310 trees
          95 % credible set contains 348 trees
          99 % credible set contains 378 trees

    Exiting mrbayes block
    Reached end of file

 All output files were saved in the same directory. (MrBayes)tatistics for branch and node parameters
          (saved to file "sequences-aligned-MUSCLE-mb.nexus.vstat"):

                                               95% HPD Interval
                                             --------------------
       Parameter      Mean       Variance     Lower       Upper       Median
       ---------------------------------------------------------------------
       length[1]     0.004294    0.000008    0.000296    0.010287    0.003530
       length[2]     0.009473    0.000015    0.003447    0.017463    0.009035
       length[3]     0.004083    0.000011    0.000058

