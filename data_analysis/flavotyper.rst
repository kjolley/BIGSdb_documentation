.. index::
   single: FlavoTyper; 
   
.. _flavotyper:

**********
FlavoTyper
**********
FlavoTyper is a bioinformatics tool that performs *in silico* serotyping of 
*Flavobacterium psychrophilum* genome assemblies. Phenotypic characterization 
of this pathogen (including serotyping based on the structural variations in 
the O-polysaccharide moiety of cell surface lipopolysaccharide) provides 
critical information for epidemiological surveillance, outbreak investigation, 
and the design of effective vaccines. FlavoTyper enables this characterization
directly from genome assemblies, making serotyping scalable, reproducible, and
independent of wet-lab assays.

The tool will only be enabled on the database for *Flavobacterium psychrophilum*.

The function can be accessed by expanding the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/flavotyper.png

Alternatively, it can be accessed following a query by clicking the 'Gene 
Presence' button at the bottom of the results table. Isolates returned from 
the query will be automatically selected within the plugin interface.

.. image:: /images/data_analysis/flavotyper2.png

Finally, the analysis is also possible directly from an isolate record, if
the isolate has a genome assembly associated with it.

.. image:: /images/data_analysis/flavotyper3.png

The tool interface consists of a list of isolate ids to check. This will be
pre-populated if accessed following a query or directly from an isolate record. 

Click 'submit'.

.. image:: /images/data_analysis/flavotyper4.png

The output will be an HTML table (if fewer than 100 records are selected), a 
tab-delimited text file and an Excel file generated from this.

.. image:: /images/data_analysis/flavotyper5.png

If a single record is chosen, the output may also include a .png file of a two-
track locus map.

.. image:: /images/data_analysis/flavotyper6.png

The results from running FlavoTyper will be stored in the database and once run
are available for display within an isolate record.

.. image:: /images/data_analysis/flavotyper7.png

