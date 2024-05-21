Overview
========

.. figure:: ../figures/Logo.png
   :alt: Logo
   :align: center
   :width: 50%

``Hammerhead`` is a tool designed to *de novo* identify bacterial DNA
methylation, including 4mC, 5mC, and 6mA, based on the strand-specific
mismatch patterns observed in R10.4.1 nanopore sequencing reads. It does
not require negative controls (methylation-free datasets); only native
DNA reads and references are needed as input for Hammerhead.

Author’s notes
==============

We are continuously improving ``Hammerhead`` to enhance its usability
and expand its capabilities. Your feedback is greatly appreciated. You
can contact us via email at xudongliu98@gmail.com or
runsheng.li@cityu.edu.hk, or directly through the `GitHub issues
page <https://github.com/lrslab/Hammerhead/issues>`__.

Installation
============

To use this tool, you’ll need to install additional tools or packages
for read processing, including samtools and minimap2. The following
command can help you install dependencies.

You can directly use `Conda <https://docs.conda.io/en/latest/>`__ to
download and install the dependencies based on the current environment.

.. code:: shell

   conda install -c bioconda -c conda-forge minimap2 samtools bedtools -y

Also, you can create a new environment to install these dependencies.

.. code:: shell

   conda create -n hammerhead -c bioconda -c conda-forge python samtools minimap2 bedtools -y 
   conda activate hammerhead

If you encounter any version conflicts, you can select a specific
version of the software to resolve the issue.

.. code:: shell

   conda install -c bioconda -c conda-forge minimap2==2.17 samtools==1.17 bedtools==2.30.0 -y

Once you solve the problem of dependencies, the following command can
help to install the ``Hammerhead``.

.. code:: shell

   pip install Hammerhead-View

Quick usage
===========

``Hammerhead`` can be run in two different strategies to locate
methylation positions:

The first strategy is to select the sites with a difference index over
the cutoff, the default is 0.35.

.. code:: shell

   hammerhead --ref genome.fa --read input.fastq --cpu 4

The second strategy is to select the top N sites, based on the
difference index sorted from the largest to the smallest, the default
number is 2000.

.. code:: shell

   hammerhead --ref genome.fa --read input.fastq --cpu 4 --method top

Example
=======

Here, we provide demo datasets (R10.4.1 simplex reads of *E. coli*) for
testing the ``Hammerhead``. The following commands can help to download
them.

.. code:: shell

   wget https://figshare.com/ndownloader/files/46437190 -O ecoli.fa
   wget https://figshare.com/ndownloader/files/46437193 -O test.fastq.gz

Please run the following command to start data analysis!

.. code:: shell

   hammerhead --ref ecoli.fa --read test.fastq.gz --min_depth 5 --min_depth_strand 3

**Note:** The arguments used in this command were for demonstration
purposes only (the read coverage of data was too shallow) and may not
reflect the optimal settings for your dataset. It is generally
recommended to use the default arguments when you have sufficient read
coverage, typically considered to be more than 50-fold coverage.
