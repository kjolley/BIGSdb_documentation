.. index::
   single: PlasmidFinder

.. _plasmidfinder:

*************
PlasmidFinder
*************
PlasmidFinder is a tool for detecting plasmid sequences in whole genome data,
primarily from *Enterobacteriaceae*. It is described in:

 * Carattoli et al. 2014 *In silico* detection and typing of plasmids using 
   PlasmidFinder and plasmid multilocus sequence typing. 
   Antimicrob Agents Chemother 58:3895-903. 
   https://pubmed.ncbi.nlm.nih.gov/24777092/
 * Carattoli et al. 2020 PlasmidFinder and *in silico* pMLST: Identification 
   and Typing of Plasmid Replicons in Whole-Genome Sequencing (WGS) 
   Methods Mol Biol 2075:285-294.
   https://pubmed.ncbi.nlm.nih.gov/31584170/
   
The function can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/plasmidfinder1.png

Jump to the ‘Third party’ category, follow the link to PlasmidFinder, then click 
‘Launch PlasmidFinder’.

.. image:: /images/data_analysis/plasmidfinder2.png

Alternatively, it can be accessed following a query by clicking the ‘PlasmidFinder’ 
button in the 'Third party' list at the bottom of the results table. Please 
note that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/plasmidfinder3.png

Select the isolate records to analyse - these will be pre-selected if you 
accessed the plugin following a query. 

Click submit.

.. image:: /images/data_analysis/plasmidfinder4.png

The analysis will be submitted to the job queue.

If plasmids are found, these are displayed in a table as output. There will 
also be an output file containing the results. This will either be a single
JSON file, or a zip file containing multiple JSON files if more than one 
isolate was selected.

.. image:: /images/data_analysis/plasmidfinder5.png

If plasmids are found, these results are stored within the database and will 
be displayed with an isolate record for anybody accessing it in the future.

.. image:: /images/data_analysis/plasmidfinder6.png

 