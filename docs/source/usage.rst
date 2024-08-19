Usage
=====

MGnify API input
----------------

To use data from MGnify API you can first specify a sample accession, study accesion, experiment type, pipeline version, instrument platform, instrument model and biome name. Valid examples could look like the following:

.. code-block:: console

   --sample_accession ERR2136697
   --study_accession MGYS00001946
   --experiment_type metagenomic
   --pipeline_version 2.0
   --instrument_platform Illumina
   --instrument_model Illumina MiSeq
   --biome_name aquatic

For more details please refer to the :doc:`parameters <parameters>` documentation. 

Please note the following requirements:
   * You have to precise a least one of these parameters in the command line 
   * If the command line parameter --noapi is specified all the parameters related to the API input are ignored

You can apply taxonomy filters on these data before the downloading step. You can specify taxonomy filters at each taxonomic level directly in the command line. 
Valid examples could look like the following:

.. code-block:: console

   --taxonomy_phylum proteobacteria
   --taxonomy_class alphaproteobacteria
   --taxonomy_order ['legionellales','triotrichales']
   --taxonomy_family legionellaceae
   --taxonomy_genus legionella
   --taxonomy_species 'legionella pneumophila'

For more details please refer to the :doc:`usage <parameters>` documentation. 

Local data input
----------------

To use you own local data you can specify a CSV samplesheet input file that contains the paths to your FASTQ files and additional metadata. 

.. NOTE::

   By default the input data comes from the MGnify API, if you want to use you own data as input you have to specify --local in the command line. 

At a minimum CSV file should contain the following columns:
sample,read_1,read_2,experiment,biome

The path to read_2 is optional. Valid examples could look like the following:

.. code-block:: console

   sample,read_1,read_2,biome
   sample1,data/sample1_R1.fastq.gz,data/sample1_R2.fastq.gz,root:Environmental:Terrestrial:Soil:Mine
   sample2,data/sample2_R1.fastq.gz,data/sample2_R2.fastq.gz,root:Environmental:Terrestrial:Soil
   sample3,data/sample3_R1.fastq.gz,data/sample3_R2.fastq.gz,root:Environmental:Terrestrial:Soil:Cave

or

.. code-block:: console

   sample,read_1,read_2,biome
   sample1,data/sample1.fastq.gz,,root:Environmental:Terrestrial:Soil:Mine
   sample2,data/sample2.fastq.gz,,root:Environmental:Terrestrial
   sample3,data/sample3.fastq.gz,,root:Environmental:Terrestrial:Soil:Cave


Please note the following requirements:
    * a minimum 4 of comma-seperated columns
    * Valid file extension: .csv
    * Must contain the header sample,read_1,read_2,biome
    * FastQ files must be compressed (.fastq.gz, .fq.gz)
    * Within one samplesheet either only single-end, assembled reads, or only paired-end reads can be specified
    * If single-end reads are specified, the command line parameter --single_end must be specified as well
    * If assembled reads are specified, the command line parameter --assembly_input must be specified as well

.. WARNING::

   Please provide the biome lineage correctly as same nomenlature a MGnify. If you don't know the biome lineage you can find it on the `MGnify website (browse biomes data) <https://www.ebi.ac.uk/metagenomics/browse/biomes/>`_

.. NOTE::

   A sample sheet template is available on the GitHub repository.

Running the pipeline
--------------------

The typical command for running the pipeline is as follows:

.. code-block:: console

   nextflow run main.nf --with-singularity sieve_01.sif --resultsDir <OUTDIR> --cat_db <PATH/TO/CAT_database> --cat_taxonomy <PATH/TO/CAT_taxonomy>

Note that the pipeline will create the following files in your working directory:

.. code-block:: console

   work                # Directory containing the nextflow working files
   <OUTDIR>            # Finished results in specified location (defined with --resultsDir)
   .nextflow_log       # Log file from Nextflow


How to skip steps
-----------------

Some of the pipeline steps are optional such as the identification of genes of interest, the identification of macromolecular systems and the usage of all binning tools.
If you want to skip one or all these steps you can specify it directly in the command line. 

Valid examples could look like the following:

.. code-block:: console

   --noapi                #Skip the API processes
   --nodiamond            #Skip the indentification of genes
   --nomacsyfinder        #Skip the identification of macromolecular system
   --nomaxbin2            #Skip binning with maxbin2
   --noconcoct            #Skip binning with concoct


Need help to writing the running command line ?
-----------------------------------------------

We have developed the shiny app with a `'command_generator' <https://lascauxzelia.shinyapps.io/sieve_app/>`_ tab that can easily generate the command line with a graphical interface.




