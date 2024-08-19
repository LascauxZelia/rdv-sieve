Installation
============

Installation instructions for sieve. 

Nextflow
--------

To run sieve, you will need to install `Nextflow <https://www.nextflow.io/docs/latest/index.html>`_ , a pipeline execution framework. Nextflow is distributed as a self-installing package, which means that it does not require any special installation procedure.

It only needs two easy steps:

    1. Download the executable package by copying and pasting either one of the following commands in your terminal window: ``wget -qO- https://get.nextflow.io | bash``

    Or, if you prefer curl: ``curl -s https://get.nextflow.io | bash``

    This will create the nextflow main executable file in the current directory.

    2. Make the binary executable on your system by running ``chmod +x nextflow``.

    3. Optionally, move the nextflow file to a directory accessible by your``$PATH`` variable (this is only required to avoid remembering and typing the full path to nextflow each time you need to run it).


Singularity
-----------

We provide a singularity container with all necessary tools installed and configured. To use it, you first need to install `Singularity <https://docs.sylabs.io/guides/3.0/user-guide/index.html>`_  itself: 

.. code-block:: console

   $ export VERSION=3.0.3 && # adjust this as necessary \
       mkdir -p $GOPATH/src/github.com/sylabs && \
       cd $GOPATH/src/github.com/sylabs && \
       wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
       tar -xzf singularity-${VERSION}.tar.gz && \
       cd ./singularity && \
       ./mconfig

Singularity uses a custom build system called makeit. mconfig is called to generate a Makefile and then make is used to compile and install.

.. code-block:: console

   $ ./mconfig && \
    make -C ./builddir && \
    sudo make -C ./builddir install

By default Singularity will be installed in the /usr/local directory hierarchy. You can specify a custom directory with the --prefix option, to mconfig like so:

.. code-block:: console

   $ ./mconfig --prefix=/opt/singularity

You can also install singularity using Go.


.. WARNING::

   Install these dependencies with apt-get or yum/rpm as shown below or similar with other package managers. See  `Singularity <https://docs.sylabs.io/guides/3.0/user-guide/index.html>`_ documentation. 


Singularity container
---------------------

Then, download the container from singularity cloud (highly recommended):

.. code-block:: console

   singularity pull --arch amd64 library://lascauxzelia/sieve/sieve:01

Or build it locally with the singularity recipe ``sieve.def`` available in sieve Github repository (you need the root access):

.. code-block:: console

   sudo singularity build sieve_01.sif sieve.def


.. NOTE::

   We highly recommend using the provided singularity container to install all needed software. Installing everything directly on the machine can be achieved using conda. 

If you want to see the version of the tools installed in the container, simply use conda to list all installed packages:

.. code-block:: console

   singularity exec sieve_<version>.sif conda list -n sieve

Sieve
-----

Now you can either get sieve from Github (recommended) or let Nextflow handle it. 

.. code-block:: console

   git clone https://github.com/LascauxZelia/sieve.git

   cd sieve

   nextflow run . -help

or 

.. code-block:: console

    nextflow run LascauxZelia/sieve -r main -preview

CAT database
------------

In addition to these intallations, you will have to get the `CAT <https://github.com/dutilh/CAT#downloading-preconstructed-database-files>`_ database files on your system. You can either download preconstructed database files, or generate them yourself.

Downloading preconstructed database files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To download the database files, find the most recent version on `tbb.bio.uu.nl/tina/CAT_prepare/ <tbb.bio.uu.nl/tina/CAT_prepare/>`_ , download and extract, and you are ready to run the pipeline!

For NCBI nr:

.. code-block:: console

    wget tbb.bio.uu.nl/tina/CAT_prepare/<latest_version>_CAT_nr.tar.gz

    tar -xvzf <latest_version>_CAT_nr.tar.gz

You can also creating a custom database, see the `instructions <https://github.com/dutilh/CAT#downloading-preconstructed-database-files>`_ . 

In the 'CAT_prepare_<latest_version>' folder, the ‘path_to/<latest_version>_CAT_database/’ and ‘path_to/<latest_version>_taxonomy’ subfolders must be used as -cat_db and -cat_tax arguments. 

.. NOTE::

   To test the sieve pipeline without downloading the CAT_prepare database, we have included a small database that allows the user to test the installation with the ERS1073737 biosample. The database is available in the sieve folder.     

.. WARNING::

   If you don't download the preconstructed database files, or generate them yourself you won't be able to run sieve. 
   GTDB preconstructed database files are not compatible with sieve.  
