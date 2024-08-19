Running sieve and user cases
============================

I want to reconstruct MAGs from a specific sample
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Only one sample as the input. No filters are applied.

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \  #Use the sieve_01 singularity container. 
        --sample_accession ERS1073737 \  # Enter a specific sample accession number available on MGnify database
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  # Absolute path of the CAT database and CAT taxonomy or custom database
        --resultsDir output \  #The output directory 
        --nodiamond --nomacsyfinder  #Skip diamond (db and aligment) and MacSyFinder processes 

Estimated running time:

I want to reconstruct all MAGs belonging to a specific taxon
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example: Legionellales

Same sample as the input with a taxonomic filter at order level. 

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 \ 
        --taxonomyorder legionellales \  #Taxonomic filter add one or more order names
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --nodiamond --nomacsyfinder  

Estimated running time:

I want to reconstruct all the MAGs belonging to a specific taxon and containing specific genes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example: Legionellales with presence of T4BSS genes

Same sample as input. Same taxonomic filters. New filter: Identification of genes of interest to the user.
(All genes must be in fasta format in the same folder. Specify the real path of the folder in the --gene parameter)

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/  \ #Diamond process: A single path to one or several local fasta files in order to construct diamond database
        --diamond_min_align_reads 2 \  #Diamond: Checks if the number of observed alignment from diamond analysis is not greater than this specified threshold
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --nomacsyfinder  

Estimated running time:

I want to reconstruct all the MAGs belonging to a specific taxon, containing specific genes and macromolecular system (pathways)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example: Legionellales with T4BSS

Same sample as input. Same taxonomic filter. Gene identification filter is also applied. New filter: Identification of macromolecular systems of interest to the user.
(You can use a pre-built model from macsydata or your own).

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model TXSScan  \ #MacSyFinder process: Must be the name of family models
        --nbmodel bacteria/diderm/T1SS  \ #MacSyFinder process: Path to the model of your interest, or it can be all models 'all'
        --coverage 0.7 \  #MacSyFinder process: Minimal profile coverage required in the hit alignment to allow the hit selection for system detection
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output  

Estimated running time:

I want to reconstruct all the MAGs belonging to a specific taxon, containing specific genes and macromolecular system (or pathways) using specific binning algorithm and quality criteria 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example: Legionellales with T4BSS, bin with concoct and select bin with a completeness of 70% and a contamination of maximum 20%

Same input and filters as above. Only one binning algorithm is used here (concoct). We decide to change the binning size (default 1000). 
And we want to annotate and classify only bin with a completeness of 70% and a contamination of maximum 20% (i.e. a redundancy of 1.2).

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model TXSScan --nbmodel bacteria/diderm/T1SS --coverage 0.7 \  
        --nomaxbin2 \ #Skip binning with Maxbin2.
        --chunk_size 1200 \ #Concoct binning: Chunk size of the script cut_ut_fasta.py. Cut up fasta file in non-overlapping or overlapping parts of equal length.
        --completeness 0.7 \ #miComplete: Bin completeness is calculated based on the presence/absence a set of marker genes
        --redundancy 1.2 \  #miComplete: Redundancy is reported as the fraction duplicated markers of all markers. 
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output  

Estimated running time:

I want to reconstruct all the MAGs belonging to a specific biome and taxon from local and public metagenomes, containing specific genes and macromolecular system using specific quality criteria 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The input will be some local metagenomes (single end) and metagenomes from the aquatic biome. We are looking for gammaproteobacterial genomes that contain specific genes and macromolecular systems. 
We classify all bins here, even those with less than 50% completeness and more than 10% contamination. 
We also specify the maximum number of CPUs, memory and time for the HPC cluster (for the base.config file). 

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --local \ #Input includes local data
        --local_input path/to/samplesheet.csv \ #Path of CSV samplesheet file containing information about local samples.
        --single-end \  #If input is single-end reads.
        --biome_name water \ #Enter a specific biome available on MGnify database
        --experiment_type metagenomic \ # Enter a experiment type (metagenomic and assembly are supported by sieve)
        --taxonomyclass gammaproteobacteria \  ##Taxonomic filter add one or more class names
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model yourmodel --modelpath path/to/your/model --coverage 0.7 \  
        --megabinpenalty 0.7 \ #DASTool: Penalty for megabins (weight c)
        --class_all_bins \   #To run the classfication process on all the bins and not only on the good quality bins.
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --max_cpus 16 \ #Set maximum number of cpus
        --max_memory 128.GB \ #Set maximum memory
        --max_time 72.h  \ #Set maximum time

Estimated running time:
