Few other things on bioinformatic tools. There are derived databases, for example proteins or custom (or invented) sequences. The most important is NCBI RefSeq, both for DNA and Protein data. It's filtered from GeneBank, redundancies are eliminated, cleaned by NCBI, manually curated, and more trustworthy.

[UniProt](www.uniprot.org) is the most accurate protein DB. They can be automatically or manually annotated. TrEMBL is a database that just translates automatically EMBL sequences. SwissProt is manually curated.

[Mastermind](mastermind.genomenon.com) is another interesting website that mines publications.

### the workflow

We want to look, into a database, which sequences are similar to ours, to inherit annotation. Or, from a high-throughput experiment (Illumina) we want to align our sequences (**assembly**) , to understand **sites of conservation** at sequence level to understand functionality. Another thing is **philogeny**, to understand evolution. 

### comparing sequences

one to one (pairwise sequence comparison) , one to many (in sequence databases, via BLAST or FASTA), many to many (multiple sequences together. Multiple sequence alignment, de novo assembly).

Methods can be categorized into **optimal/exhaustive**, **heuristic**, or **graphical**. 

**Local alignment**: find the best aligning subsequences (BLAST) (gene vs genome). It subsets both sequences to return the common part.
**Global alignment**: align over the entire length (ClustalW) (gene vs gene, seq vs gene)

### BLAST

One of the most used tools. It takes one sequence against a database (that can be all GeneBank, a single genome, etc).  We provide a query (my sequence to compare to the DB is called query). Our database is a FASTA file that needs to be indexed. Binary files are produced during indexing. Word size should be large with similar DBs (human vs human) and more tolerant (short words, less efficient) between different species. Seeds are created when there is a match.

Tables like BLOSUM62 are used to see if two aminoacids are similar and interchangable. After seeds matching, seeds are extended to see how the match holds in their neighborhood. Many **results** are returned. a **hit** or **subject** is a single relation between the query and a matching sequence (subject or hit) in the database, the WHOLE matched sequence. An **hsp  (high scoring pair)** is a single alignment between the query and the subject.

Returned results are, in order, different hits. **Expect value (E value)** = number of unrelated databank sequences expected to yield the same or higher score by pure chance. Lower=better. **Bit score** = score corrected for scale of scoring scheme. Higher=better.

There are many version:

* blastn (DNA vs DNA)
* blastp (protein vs protein)
* blastx (translated DNA vs protein)
* tblastn ...
* tblastx ...

on NCBI, blast can be optimized: **megablast** is highly specific (same species only) but very fast. You can choose expect threshold (E-value cutoff. ) and word size for seeds. You can **mask** repeats.