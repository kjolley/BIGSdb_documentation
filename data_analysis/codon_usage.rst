.. index::
   single: codon usage

.. _codon_usage_plugin:

***********
Codon usage
***********
The codon usage plugin for isolate databases calculates the absolute and 
relative synonymous codon usage by isolate and by locus.

The function can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/analysis.png

Jump to the 'Analysis' category, follow the link to 'Codon Usage', then click 
'Launch Codon Usage'.

The function can be selected by clicking the 'Codon usage' link in the Analysis
section of the main contents page.

.. image:: /images/data_analysis/codon_usage.png

Alternatively, it can be accessed following a query by clicking the 'Codons' 
button in the Analysis list at the bottom of the results table.  Please note 
that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/codon_usage2.png

Enter the ids of the isolate records to analyse - these will be already entered
if you accessed the plugin following a query.  Select the loci you would like 
to analyse, either from the dropdown loci list, and/or by selecting one or more
schemes.

.. image:: /images/data_analysis/codon_usage3.png

Click submit.  The job will be submitted to the queue and will start running 
shortly.
  
Output files will be created in both tab-delimited text and Excel formats for
the following:

* Absolute frequency of codon usage by isolate
* Absolute frequency of codon usage by locus
* Relative synonymous codon usage by isolate
* Relative synonymous codon usage by locus

.. image:: /images/data_analysis/codon_usage4.png
