.. index::
   single: Kaptive

.. _kaptive:

*******
Kaptive
*******
Kaptive is a tool for surface polysaccharide typing from bacterial genome
sequences, specifically for *Klebsiella* and *Acinetobacter baumannii* although
it can be extended for other organisms. This plugin is a wrapper that runs
Kaptive for selected isolates, outputs the results and also stores them within 
the database so that they can be shown within the isolate information page.

Kaptive will usually only be available on databases hosting suitable data
i.e. *Klebsiella* or *Acinetobacter baumannii* isolates. 

Documentation for Kaptive can be found at 
https://kaptive.readthedocs.io/en/latest/.

If you use the results of Kaptive, you should cite the following:

* Stanton TD, Hetland MAK, Löhr IH, Holt KE, Wyres KL. Fast and Accurate 
  *in silico* Antigen Typing with Kaptive 3 [Internet]. bioRxiv; 2025 
  [cited 2025 Feb 27]. p. 2025.02.05.636613. 
  https://www.biorxiv.org/content/10.1101/2025.02.05.636613v1
      
The function can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/kaptive.png

Jump to the ‘Third party’ category, follow the link to Kaptive, then click 
‘Launch Kaptive’.

.. image:: /images/data_analysis/kaptive2.png

Alternatively, it can be accessed following a query by clicking the ‘Kleborate’ 
button in the 'Third party' list at the bottom of the results table. Please 
note that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/kaptive3.png

Select the isolate records to analyse - these will be pre-selected if you 
accessed the plugin following a query. 

Click submit.

.. image:: /images/data_analysis/kaptive4.png

The analysis will be submitted to the job queue.

When the job has completed you will see a files available for download in 
tab-delimited text and Excel formats, as well as SVG file(s) containing a
visualisation of each locus.

.. image:: /images/data_analysis/kaptive5.png

   
 