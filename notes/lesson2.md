# Genes

There is no complete agreement on what a gene is. This is a big problem for bioinformatics. In 1800-1900, Mendel discovered few laws: Laws of segregation, independent assortment, and dominance. After 1900, Morgan developed the ideas of chromosomal theory of inheritance, genetic linkage and chromosomal crossing over. They discovered that some pairs of genes du not segregate randomly according to Mendel's law of segregation. Morgan proposed that these genes were located on the same entity (chromosome). Variation of the strength of the linkage determined gene position on chromosome.

A gene today is a segment of DNA specifying a polypeptide chain (protein) It includes regions preceding and following the coding region (leader and trailer) as well as intervening sequences (introns) between individual coding segments (exons)

A gene is transcripted in a pre-mRNA, that is then spliced (introns are removed) to become coding mRNA, in eukaryots. Prokaryots have no introns.

5'UTR $\rightarrow$ portion of DNA at first bases(>+1), who doesn't code (untranslated). there is also 3'UTR at the end.
ORF $\rightarrow$ Open Reading Frame. Start with `ATG` until a stop codon is found.
Promoters:
-90 `CAAT`
-75 `GGGCGG`
-30 `TATAAAA` "TATA box", recognized by TBP (tata binding protein), an aligner for transcription, included in 10-30% of genes

Current picture is more complex. Noncoding genes are involved, regulatory regions were discovered, and the result of the central dogma are both proteins an different (m)RNAs.

FANTOM (functional annotation of mammalian genome) and ENCODE (encyclopedia of DNA elements).

Profile: starting from a cell, it's the characterization of mRNA. 

ESTs: expressed sequence tags. It's a catalog of all the transcripts expressed in a cellular population. Genomic mRNA was extracted, put in plasmids (in fragments) and put into bacteria, and cDNA libraries were created.

EST Profile/Unigene database: can find in how many sites a sequence is expressed among all libraries publicated, divided by sites.

Another technique is the microarray. You know know almost all transcriptional outputs of an organism, that can be characterized by different levels in different samples/individuals. So the built a chip with all of them, able to quantify the levels of all transcripts in a tissue. The issue is that probes are defined *ab initio* and hard to change. Usually you dye 2 different samples with red and green dyes, and use one to normalize the other. Affymetrix has a single color.

RNA extraction -> cDNA amplification -> chip hybridization.

GEO Profile database on NCBI.  Tiling microarrays instead bring probes for all, overlapping parts of the genome.



### CAP analysis of tene expression (CAGE)

A transcript is characterized by a specific feature at the beginning (5'). a CAP is a protein molecule present at the beginning of the transcript. It can be recognized by antibody-marked fluorescent beads. On the other side there's a poly`A`, formerly used to sequence backwards the gene (with a poly`T` primer), but in this way we lacked the information about the 5' end, because the expansion was partial. 

Then they were able to cut after 20b from CAP, to be later included in a plasmid.

### RNAseq - NGS

Total RNA -> oligo dR enrichment -> fragmentation (400-500 bp) -> they are amplified from both extremities, random hexamer primed cDNA synthesis (35 bp) -> HiSeq2000 sequencing -> mapping to reference gene -> functional analysis.

We have fragments, of which we know the extremities, that overlaps, all over the genome.

SRA databases on NCBI of Illumina data.

## FANTOM project

So there are 4 techniques:

* full length EST libraries
* CAGE (CAP analysis for gene expression for Transcriptional Start Site annotation)
* Microarray
* Sequencing

Outcomes: over 60k mouse transcripts identified, 60% of genome transcribes in RNA, over 23K non-coding RNA, identified a novel class of short RNAs associated with transcription starting sites, 70% of the transcriptional units shows sense-antisense transcription.

## ENCODE pilot project

from 1% of human genome, produced 600M data points.  It showed pervasive transcriptions in the genome, additional exons and alternative tissue-specific TSS in 80% of genes , 20% of transcripts produces chimeras (fusion of transcripts from different regions), 20% of pseudogenes are transcribed.

Pseudogenes are mutated copies of genes in other regions.



After FANTOM and ENCODE projects, we have an updated gene definition:

A gene is a genomic sequence (DNA or RNA) directly encoding functional product molecules, either RNA or protein. In the case that there are several functional products sharing overlapping regions, one takes the union of all overlapping genomic sequences coding from them. This union must be coherent (done separately for final protein and RNA products) but does not require that all products necessarily share a common subsequence.

[Encode Project website](http://www.encodeproject.org)

## ChIP-seq

Chromatin Immuno-precipitation: we use specific antibodies to bind the copies of proteins that binds regulatory regions. Then we fragment the DNA and keep only the Ab-tagged parts.

## Geuvadis project

For 500 individuals, after sequencing the RNA were analyzed too, so we have both data on RNA and DNA.

## GTEX project

Sequencing from 100s of individuals both genome and trascriptome of different tissues

## TCGA (the cancer genome atlas)

[cancer genome website](cancergenome.nih.gov)

## international human epigenomics project

## GIAB (Genome in a bottle)

