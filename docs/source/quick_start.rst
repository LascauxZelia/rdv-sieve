Running sieve and user cases
============================

I want to reconstruct MAGs from a specific sample
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Only one sample as the input. No filters are applied.

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \  
        --sample_accession ERS1073737 \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --nodiamond --nomacsyfinder  

I want to reconstruct all MAGs belonging to a specific taxon: Legionellales 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Same sample as the input with a taxonomic filter at order level. 

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --nodiamond --nomacsyfinder  

I want to reconstruct all the MAGs belonging to a specific taxon and containing specific genes: Legionellales with T4BSS genes 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Same sample as input. Same taxonomic filters. New filter: Identification of genes of interest to the user.
(All genes must be in fasta format in the same folder. Specify the real path of the folder in the --gene parameter)

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --nomacsyfinder  

I want to reconstruct all the MAGs belonging to a specific taxon, containing specific genes and macromolecular system (pathways): Legionellales with T4BSS 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Same sample as input. Same taxonomic filter. Gene identification filter is also applied. New filter: Identification of macromolecular systems of interest to the user.
(You can use a pre-built model from macsydata or your own).

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model TXSScan --nbmodel bacteria/diderm/T1SS --coverage 0.7 \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output  

Do you want to reconstruct MAGs using specific binning algorithm and quality criteria?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Same input and filters as above. Only one binning algorithm is used here (concoct). We decide to change the binning size (default 1000). 
And we want to annotate and classify only bin with a completeness of 70% and a contamination of maximum 20% (i.e. a redundancy of 1.2).

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --sample_accession ERS1073737 --taxonomyorder legionellales \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model TXSScan --nbmodel bacteria/diderm/T1SS --coverage 0.7 \  
        --nomaxbin2 --chunk_size 1200 --completeness 0.7 --redundancy 1.2 \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output  


Do you want to use local and public metagenomes?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The input will be some local metagenomes (single end) and metagenomes from the aquatic biome. We are looking for gammaproteobacterial genomes that contain specific genes and macromolecular systems. 
We classify all bins here, even those with less than 50% completeness and more than 10% contamination. 
We also specify the maximum number of CPUs, memory and time for the HPC cluster (for the base.config file). 

.. code-block:: console

    nextflow run . \  
        -with-singularity sieve_01.sif \ 
        --local --local_input path/to/samplesheet.csv --single-end \  
        --biome_name water --experiment_type metagenomic --taxonomyclass gammaproteobacteria \  
        --genes path/to/my/genes/ --diamond_min_align_reads 2 \  
        --model yourmodel --modelpath path/to/your/model --coverage 0.7 \  
        --megabinpenalty 0.7 --class_all_bins \  
        --cat_db /your/path/to/cat_db --cat_taxonomy /your/path/to/cat_tax \  
        --resultsDir output \  
        --max_cpus 16 --max_memory 128.GB --max_time 72.h  
