.. index::
   single: SNP sites

.. _snp_sites_plugin:

********
SNPsites
********
The SNPsites plugin for isolate databases will create alignments for each 
selected locus for the set of isolates chosen. These alignments are then
passed to the `snp-sites tool <https://github.com/sanger-pathogens/snp-sites>`_.
which will generate VCF files for each locus. A summary table will be created
showing the number of alleles and polymorphisms found for each locus.

The snp-sites algorithm and program are described in 
`Page et al. 2016. Microb Gen 2:e000056 <https://pubmed.ncbi.nlm.nih.gov/28348851/>`_.

The function can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/analysis.png

Jump to the 'Analysis' category, follow the link to 'SNPSites', then click 
'Launch SNPsites'.

Alternatively, it can be accessed following a query by clicking the 'SNPSites' 
button in the Analysis list at the bottom of the results table.  Please note 
that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/snp_sites.png

Enter the ids of the isolate records to analyse - these will be already entered
if you accessed the plugin following a query.  Select the loci you would like 
to analyse, either from the dropdown loci list, and/or by selecting one or more
schemes.

.. image:: /images/data_analysis/snp_sites2.png

Click submit.  The job will be submitted to the queue and will start running 
shortly.

Output consists of a summary file showing the number of sequences found in the
dataset, the number of unique alleles, and the number of SNPs for each locus.
An interactive chart is also displayed showing these values. Finally, Zip files
are produced that contain FASTA alignments and VCF files for each locus.

.. image:: /images/data_analysis/snp_sites3.png
