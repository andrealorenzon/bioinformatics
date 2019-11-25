# Example of gene expression data meta-analysis.

How to get data from people who already made them. Communication with wet lab guys is mandatory. Signalin variations during Zebrafish development. We mine multiple datasets to find differences and significant data. A functional interpretation is knowledge extraction in high-throughput genomics experiments. Enrichment Analysis (EA) tells us if an interesting collection of genes is enriched for a particular set of a priori known functional classes. We start from a list of up/down-regulated genes (differentially expressed genes), among a list of unchanged ones (not responding). The intersection of responding genes with sets of genes with common class (metabolism, regulation, signaling, etc) will show the relevance of that class, after being compared with the percentage of intersection of the not-responding genes[^1] 

`class AND not responding VS class AND selected` 

Then you get only the responding gene that belong to your class, to further restrict the research field. We are looking for classes for which most of the differentially regulated genes are in the selected set.

Apart from Bioconductor, other softwares are [DAVID](david.abcc.ncifcrf.gov) and [GSEA](http://software.broadinstitute.org/gsea/index.jsp).  (read the Nature article of the latter). 

Those tools does not necessarily bring results. No functional enrichment could be visibile from microarray analysis data. For example, we could create new classes (i.e. maternal transcripts vs zygotic transcripts)

There are small RNA that can interfere with specific mRNA classes. miRNA are 25 bp RNA construct whose 6/8 beginning bp are complementary with 3'UTR of mRNA, leading to its degradation. Additional classes can be defined by specific miRNA responsiveness. 

# gene expression analysis experimental design



Workflow: experimental design(1) $\rightarrow$ RNA work(2) $\rightarrow$ Platform work(3) $\rightarrow$ analysis(4)

1) have precise specific biological questions to be answered.
2) sample selection, treatments, extraction, labelling
3) Hybridization, washing, scanning, image manipulation
4) everything.

## analytical pipeline

Quality control (test sample and hybridization quality)
$\downarrow$ 
Normalization (make different hybridization comparable)
$\downarrow$ 
Filtering (keep only interesting data, *without introducing bias*)
$\downarrow$ 
Statistical analysis ( select only **reproducible** interesting data)
$\downarrow$ 
Data mining (annotation, knowledge extraction, to produce meaningful information)

Any analysis is useless if there is no clear biological question to be investigated, or if experiments are not carefully designed to minimize human intervention, differences in reagent lots, equipments, timing, etc. It's better to mix sample groups and not to perform first all sample of a group, then the other.

If biological material is not scarce, **think wide**: make replicas (>3) of the experiment, time course experiments should have many time points (>4). Investigate part of the sample by microarrays and save the rest for further validations. Keep dicussing the experiment with statisticians/bioinformatics involved in data analysis.

Questions: how many arrays will I need? 
Should I pool my samples? (spoiler: no, because it masks inter-individual variance) 
Which array should I choose?

Sample quality is based on RIN : RNA Integrity Number. Electrophoretic run that measure degradation by speed of run. Ribosomal RNA forms 2 specific bands (5-8% of RNA), absent in degraded RNA, and absorbance measure by [QuBit IQ assay](https://www.thermofisher.com/it/en/home/industrial/spectroscopy-elemental-isotope-analysis/molecular-spectroscopy/fluorometers/qubit/qubit-assays/qubit-rna-iq-assay.html). 

Arrays are chosen by what I am looking for. On genome browsers (Ensembl) you can activate the track for your array. There are commercially available arrays and you can make custom ones. (~200-500 € / sample, ~30.000 genes).  RNAseq is ~500€. 

You should consider at least three replicates, but the more the better. Over 4, outsider points become very rare, over 8 just 1 or 2 false positives over hundreds of RNAs, and 1 or 2 over 8 false negatives, can be seen. Replicates can be quantified after the quality of the sample, magnitude of expected effect, experimental design, and method of analysis.

## Sources of variability

(*Geschwind, 2001*)

* Biological heterogenicity
* speciment collection and handling
* intra-sample heterogenicity
* RNA extraction and amplification methodologies
* Fluorescent labelling
* Hybridization
  * size/shape of spot
  * sample distribution across slide
* Scanning (voltage, power, software)
* Randomness

## quality control

We start with it as soon as we get the data. We make a table with expression levels. The first QC is the distribution of data on the table. It checks control probes (positive, negative, spikes(exogenous RNA inserted in specific concentrations, to calibrate the sample)). We check scans for artifacts, and evaluate distributions to find and ev. eliminate sample (not gene) outliers and clusters of data, analyzing boxplots of the overall signal of all gene. Lower signals could indicate degradation.

Dendrograms or PCA can be performed to understand which sample clusters with other in the same control/sample groups, to identify outliers and skip them.

## normalization

When we have selected QC-compliant samples, we normalize the data with an algorithm to preserve quantiles ([quantile normalization](https://en.wikipedia.org/wiki/Quantile_normalization) and ranking).  It is aimed to remove systematic biases. If you normalize A LOT, you can compare different platform data, if both have measure on the same set of genes. 

## filtering

We want to discard anything that makes the statistics too much stringent. We start from tens of thousands of genes. Many are not relevant for our specific problem. It will affect false discovery rate. Lowering the number of potential interesting genes helps subsetting the experiment. You can filter:

* by annotation: i.e. only genes implicated in regulation (GO term, presence of transcriptional regulative elements in promoters, etc.)
* Signal features (non specific filter: % intensities greater of a user defined value, interquartile range greater of a defined value... )
* by genefilter pOverA: keep if $\geq 25\%$ probe sets have intensities $ \geq log_2 (100)$ 

## statistical analysis

Reproducibility is the issue. It's a type of T-test, keeps in to consideration the ratio of average values among repeated samples. We take $log_2$ of the signals, to see better difference in downregulation, otherwise masked by compression.

$| log_2 \frac{\over{Trtd}}{\over{Ctrl}}| = 1 $ is the most used arbitrary threshold, to define a significant differential expression. We also could want to filter out groups whose boxplot whiskers overlaps, by filtering on the p-value calculated on the fold change's T-test. There are both parametric (with assumption on sample normality) and non-parametric tests (without it). R packages used for that are `limma` and `edgeR`. 

Genese are annotated with some ontologies, that relates them to particular 1) molecules 2) structures and 3) functions. Most ontologies are tree-structured. 

Example: we start from 1000 genes, of which 100 are transcription factors. 10 genese will be differentially expressed. Of them 8 will be transcription factors. The relative percentage is 10% vs 80%, so we expect an enrichment on the transcription functionals. Fisher's test, hypergeometric test, binomial test, chi square could be used.

The [gene ontology](http://www.geneontology.org) (GO) maintains 3 ontologies for **molecular function** (MF7220), **biological process** (BP 9529) and **cellular component** (CC 1536). 



