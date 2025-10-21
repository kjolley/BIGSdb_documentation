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
  *in silico* Antigen Typing with Kaptive 3 Microb Genom. 2025 11(6):001428.
  https://doi.org/10.1099/mgen.0.001428
 
If you use the *Klebsiella* K or O locus databases, you should also cite:

* Wyres, K.L., Wick, R.R., Gorrie, C., Jenney, A., Follador, R., Thomson, N.R., 
  Holt, K.E., 2016. Identification of *Klebsiella* capsule synthesis loci from 
  whole genome data. Microbial Genomics 2, e000102. 
  https://doi.org/10.1099/mgen.0.000102

* Lam, M.M.C., Wick, R.R., Judd, L.M., Holt, K.E., Wyres, K.L., 2022. 
  Kaptive 2.0: updated capsule and lipopolysaccharide locus typing for the 
  *Klebsiella pneumoniae* species complex. Microbial Genomics 8. 
  https://doi.org/10.1099/mgen.0.000800

If you use the *A. baumannii* K or OC locus databases, please also cite:

* Wyres, K.L., Cahill, S.M., Holt, K.E., Hall, R.M., Kenyon, J.J., 2020. 
  Identification of Acinetobacter baumannii loci for capsular polysaccharide 
  (KL) and lipooligosaccharide outer core (OCL) synthesis in genome assemblies
  using curated reference databases compatible with Kaptive. Microbial 
  Genomics 6. https://doi.org/10.1099/mgen.0.000339

* Cahill, S.M., Hall, R.M., Kenyon, J.J., 2022. An update to the database for
  Acinetobacter baumannii capsular polysaccharide locus typing extends the 
  extensive and diverse repertoire of genes found at and outside the K locus.
  Microbial Genomics 8. https://doi.org/10.1099/mgen.0.000878
      
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

   
 