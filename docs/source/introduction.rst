Introduction
============

`SIEVE <https://github.com/LascauxZelia/sieve>`_ is a bioinformatics filters-analysis pipeline for assembly, binning and annotation of metagenomes from EBI public database (database mining) or local user data. 

Pipeline summary
----------------

To analyse metagenomic datasets, users can input their own data (the pipeline will be in charge of the trimming) or filter and collect data from the European public database EBI using the MGnify API. 

The pipeline then:

* Identification of genes of interest using `diamond <https://github.com/bbuchfink/diamond>`_ 
* Performs assembly using `MEGAHIT <https://github.com/voutcn/megahit>`_ and predicts proteins-coding genes for the assemblies using `Prodigal <https://github.com/hyattpd/Prodigalt>`_ .
* Identification of contigs that contains macromolecular systems, genetic pathways of our interest with `MacSyFinder <https://github.com/gem-pasteur/macsyfinder>`_ .
* Extract contigs of interest using `seqtk <https://github.com/lh3/seqtk>`_ and assigns taxonomy using `CAT <https://github.com/dutilh/CAT>`_ .
* Performs metagenome binning using `MaxBin2 <https://sourceforge.net/projects/maxbin2/>`_ and `CONCOCT <https://github.com/BinPro/CONCOCT>`_ and checks the quality of the genome bins using `miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ 
* Refines bins with `DAS Tool <https://github.com/cmks/DAS_Tool>`_ 
* Assigns taxonomy to bins using `BAT <https://github.com/dutilh/CAT>`_ 

Futhermore, the pipeline creates various reports in the results directory specified, including a final table summarizing the main findings of the run.
A shiny app `'Sieve app' <https://lascauxzelia.shinyapps.io/sieve_app/>`_ is available to visualise the main results. 

Basic usage
-----------

.. NOTE::

   If you are new to Nextflow, please refer to this `page <https://www.nextflow.io/docs/latest/getstarted.html>`_ on how to set-up Nextflow. 

.. code-block:: console

   nextflow run . with-singularity sieve.sif --resultsDir <OUTDIR> --cat_db <PATH/TO/CAT_database> --cat_taxonomy <PATH/TO/CAT_taxonomy>

.. WARNING::

   Please provide pipeline parameters via the command line or Nextflow config file ``nextflow.config``.

For more details and further functionality, please refer to the :doc:`usage <usage>` documentation and the :doc:`parameter <parameters>` documentation. 

Pipeline output
---------------

To see the results of an example test run with a full size dataset refers to results tab on the Github pipeline page. For more details about the output files and reports, please refer to the :doc:`output <output>` documentation.

Inputs
------

The pipeline supports two types of input. You can use your own metagenomic data (in `.fastq.gz` format), the metagenomic data you are interested in from the MGnify database, or both. 

Local data
~~~~~~~~~~

The user can enter their own metagenomics data by adding the flag ``--local``. All raw reads must be in the same directory and have the same extension ``.fastq.gz``. 

In the command line the user must add ``--local_input`` with the path of the samples sheet (csv format). The samples file specifies the samples, the path of the corresponding raw read files and the biome lineage, separated by commas. A template is available `here <https://github.com/LascauxZelia/sieve>`_ . 

It has the format: ``sample,read_1,read_2,biome``. For more details please refer to the :doc:`usage <usage>` documentation.

.. WARNING::

   The 'local data' input option only works with short reads. 

MGnify API
~~~~~~~~~~

The pipeline can be run with metagenomic data from the European public database EBI. The data are retrieved using `MGnify API <https://www.ebi.ac.uk/metagenomics>`_ . You can retrieve metagenomic or assembly data using the MGnify API. You can search for a specific sample, study, sequencing platform, biome and so on. Sieve will automatically sort (based on taxonomic filters that you can define, for example retain all the metagenomes in this study that contain reads affiliated with ‘Legionella’) and download the metagenomes of interest to you.  

The MGnify ressource: 
   "Microbiome research involves the study of all genomes present within a specific environment. The approach can provide unique insights into the complex processes performed by environmental micro-organisms and their relationship to their surroundings, to each other, and, in some cases, to their host.

   MGnify offers an automated pipeline for the analysis and archiving of microbiome data to help determine the taxonomic diversity and functional & metabolic potential of environmental samples. Users can submit their own data for analysis or freely browse all of the analysed public datasets held within the repository. In addition, users can request analysis of any appropriate dataset within the European Nucleotide Archive (ENA). User-submitted or ENA-derived datasets can also be assembled on request, prior to analysis."

If you use the MGnify API option as input please cite the article: Richardson et al, NAR 2023,DOI: https://doi.org/10.1093/nar/gkac1080

For more details, please refer to the :doc: `input <input>` documentation. 

Credits
-------

SIEVE pipeline was written by Zelia Bontemps, Andrei Gulliaev and Lionel Guy at Uppsala University (Departement of Medical Biochemistry and Microbiology).

We thank the MGnify team for the assistance in the developpement of this pipeline. 


Citation
--------

If you use SIEVE, please cite the article: XXX


