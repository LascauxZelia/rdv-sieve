Parameters
==========

To get a quick overview of all available command line options, run::

   nextflow run . -help

Input/output options
--------------------

``--noapi`` (default: false)

Specifies that the input includes data from the MGnify API.

``--local`` (default: false)

Specifies that the input includes local data.

``--single_end`` (default: false)

Specifies that the input is single-end reads.

``--assembly_input`` (default: false)

Specifies that the input reads are already assembled.

``--local_input`` (default: null)

Input CSV samplesheet file containing information about the samples in the experiment. For more details please refer to the :doc:`usage <usage>` documentation. 

``--resultsDir`` (required)

The output directory where the results will be saved. You have to use absolute paths. 

MGnify filters options
----------------------

``--biome_name`` (default: null)

Enter a specific biome name  (e.g. ``Engineered``, ``Wet fermentation``, ``Hydrocarbon``, ...). By default ``null`` means no filter for the biome name, all the biomes will be included in the analysis. If you need to select more than one biome, please separate them with commas. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/biomes>`_ .

``--lineage`` (default: null)

Enter a specific lineage (e.g. ``root:Engineered``, ``root:Engineered:Biogas plant:Wet fermentation``, ``root:Engineered:Bioremediation:Hydrocarbon``, ...). By default ``null`` means no filter for lineage, all the lineages will be included in the analysis. If you need to select more than one lineage, please separate them with commas. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/biomes>`_ .

``--experiment_type`` (default: null)

Enter a specific experiment_type (i.e. ``metagenomic``, ``assembly``). By default ``null`` means no filter for experiment type, all the experiment type will be included in the analysis. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/experiment-types>`_ .

.. WARNING::

   Only ``metagenomic`` and ``assembly`` experiment type are supported. 

``--study_accession`` (default: null)

Enter a specific study accession number (e.g. ``MGYS00000278``, ``MGYS00003194``, ...). By default ``null`` means no filter for studies, all the studies will be included in the analysis. If you need to select more than one study, please separate them with commas. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/studies>`_ .

``--sample_accession`` (default: null)

Enter a specific sample accession number (e.g. ``ERS15535864``, ``SRS086441``, ...). By default ``null`` means no filter for the samples, all the samples will be included in the analysis. If you need to select more than one sample, please separate them with commas. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/samples>`_ .

``--instrument_platform`` (default: null)

Enter a specific instrument plateform (e.g. ``Illumina``, ``PacBio``, ...). By default ``null`` means no filter for the instrument platform, all the instrument platform will be included in the analysis. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/samples>`_ .

``--instrument_model`` (default: null)

Enter a specific instrument model (e.g. ``Illumina MiSeq``, ``Illumina NovaSeq``, ...). By default ``null`` means no filter for the instrument model, all the instrument  model will be included in the analysis. For more details please see the `MGnify API <https://www.ebi.ac.uk/metagenomics/api/v1/samples>`_ .


``--pipeline version`` (default: null)

Enter a specific version of the MGnify pipeline (``1.0``, ``2.0``, ``3.0``, ``4.0``, ``4.1``, ``5.0``). By default ``null`` means no filter for the pipeline version, all the version will be included in the analysis. If you need to select more than one version, please separate them with commas. For more details please see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ .




``--taxonomyphylum`` (default: null)

Enter one or more phylum names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the phylum level, all the phylum will be included in the analysis. If you need to select more than one phylum, please separate them with commas. 

``--taxonomyclass`` (default: null)

Enter one or more class names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the class level, all the class will be included in the analysis. If you need to select more than one class, please separate them with commas.

``--taxonomyorder`` (default: null)

Enter one or more order names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the order level, all the order will be included in the analysis. If you need to select more than one order, please separate them with commas.

``--taxonomyfamily`` (default: null)

Enter one or more family names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the family level, all the family will be included in the analysis. If you need to select more than one family, please separate them with commas.

``--taxonomygenus`` (default: null)

Enter one or more genus names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the genus level, all the genus will be included in the analysis. If you need to select more than one genus, please separate them with commas.

``--taxonomyspecies`` (default: null)

Enter one or more species names. The phylum name must appear in the Greengenes and/or SILVa v132 databases depending on the pipeline version (see above, or see the `MGnify pipeline version archive <https://www.ebi.ac.uk/metagenomics/pipelines>`_ ). By default ``null`` means no filter at the species level, all the species will be included in the analysis. If you need to select more than one species, please separate them with commas.

Control for targeted genes 
--------------------------

``--nodiamond`` 

Skip diamond processes (db and aligment). 

``--genes`` (required if --nodiamond is not set)

A single path to one or several local fasta files containing orthologous groups of proteins. 

.. WARNING::

   Only ``.fasta`` extension are allowed for this process. 

``--diamond_min_align_reads`` (default: 0)

This is an part of an if statement that checks if the number of observed alignment from diamond analysis is not greater than the specified threshold (diamond_min_align_reads). If this condition is true, it means that there are not enough alignments, and then the file will be removed and the sample will be deleted for the rest of the pipeline. 

Assembly options
----------------

``--min_contig_len`` (default: 1000)

Minimum length of contigs to output. 

``--k_step`` (default: 10)

MEGAHIT uses multiple k-mer strategy. Step for iteration can be set with k_step option. 

``--k_min`` (default: 21)

MEGAHIT uses multiple k-mer strategy. Minimum k can be set with k_min option. 

Secretion system search options
-------------------------------

``--nomacsyfinder``

Skip MacSyFinder process. 

``--model`` (default: TXSS)

For each --models options the first element must be the name of family models, followed by the name of the models. Models can be already defined and available online (see `MacSyFinder documentation <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/index.html>`_ ) or models can be create by the user with a specific structure (`macsy-model package <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/package.html#structure-of-a-macsy-model-package>`_ ). 

``--nbmodel`` (default: all)

If the name 'all' is in the list all models from the family will be searched, otherwise only cited models will be applied. 

``--modelpath`` (default: /opt/....)

For custom model, indicate the real path of the model.

``--coverage`` (default: 0.8)

Minimal profile coverage required in the hit alignment to allow the hit selection for system detection. 

``--evalue`` (default: -20)

Maximal independent e-value for Hmmer hits to be selected for system detection. 

Binning options
---------------

``--nomaxbin2`` (default: false) (Maxbin2)

Skip binning with Maxbin2.

``--markers`` (default: 107) (Maxbin2)

Set the markerset, choose between 107 marker genes by default or 40 marker genes. See `MaxBin2 documention <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/index.html>`_ .

``--probthreashold`` (default: 0.8) (Maxbin2)

Minimum probability for EM algorithm. 

``--noconcoct`` (default: false) (Concoct)

Skip binning with Concoct.

``--chunk_size`` (default: 10000) (Concoct)

Chunk size of the script ``cut_ut_fasta.py``. Cut up fasta file in non-overlapping or overlapping parts of equal length. 

``--overlap_size`` (default: 0) (Concoct)

Overlap size of the script ``cut_ut_fasta.py``. Cut up fasta file in non-overlapping or overlapping parts of equal length. 

``--class_all_bins`` (default: false)

To run the classfication process on all the bins and not only on the good quality bins. 


Bin quality check and refinement options 
----------------------------------------

``--score_threashold`` (default: 0) (DAS Tool)

Score threshold until selection algorithm will keep selecting bins (0..1)

``--megabin_penalty`` (default: 0.5) (DAS Tool)

Penalty for megabins (weight c). Only change if you know what you are doing (0..3)

``--duplicate_penalty`` (default: 0.6) (DAS Tool)

Penalty for duplicate single copy genes per bin (weight b). Only change if you know what you are doing (0..3) 

``--completeness`` (default: 0.50) (miComplete)

Bin completeness is calculated based on the presence/absence a set of marker genes provided as a set of HMMs from 0 (0% complete) to 1 (100% complete)

``--redundancy`` (default: 1.10) (miComplete)

Redundancy is reported as the fraction duplicated markers of all markers. In similar software such as CheckM this is reported as Contamination by percentage. E.g. 6% contamination in CheckM is equivalent to 1.06 redundancy in miComplete. From 1.00 redundancy (=0% contamination) to 2.00 redundancy (= 100% contamination).

Taxonomic profiling and annotation options
------------------------------------------

``--cat_db`` (required)

Absolute path of the CAT database or custom database. For CAT_prepare database path for ``2021-01-07_CAT_database/``

``--cat_taxonomy`` (required)

Absolute path of the CAT taxonomy database or custom taxonomy database. For CAT_prepare database path for ``2021-01-07_taxonomy/``

``--f`` (default: 0.5)

Minimum fraction classification support, on precision, fraction of classified sequences, sensitivity, and taxonomic rank of classification.

Run options
-----------

``--file_name`` (default: accessions.csv) 

File name to store all the accession numbers and metadata

``--page_size`` (default: 250)

MGnify API pagination size

``--help`` or ``--h``

To get a quick overview of all available command line options

``--cpus`` (default: 1)

Number of CPUs to use. 

``--python3`` (default: ``/opt/conda/envs/sieve/bin/python3``) 

Location of Python3. Location of the python3 executable that has all needed packages available. Should usually be ``/usr/bin/env/python3``, leave as default is using the singularity image. 

Nextflow core options
---------------------

``-with-singulairty`` (default: ``sieve.sif``)

To simply specify the Singularity image file from where the containers are started. Every time your script launches a process execution, Nextflow will run it into a Singulairty container created by using the specified image. 

.. WARNING::

   The sieve.sif created for the pipeline is define in the Nextflow configuration file. 

``-resume``

Specigy when restarting the pipeline. Nextflow will use cached results from any pipeline steps where inputs are the same, continuing from where it got to previously. 

You can also supply a run name to resume a specific run: ``-resume [run-name]``. Use the ``nextflow log`` command to show previous run names. 
