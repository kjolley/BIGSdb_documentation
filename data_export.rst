###################
Data export plugins
###################

*********************
Isolate record export
*********************
You can export the entire isolate recordset by clicking the 'Export dataset' link in the Export section of the main contents page.

.. image:: /images/data_export/isolate_export.png

Alternatively, you can export the recordsets of isolates returned from a database query by clicking the ‘Dataset’ button in the Export list at the bottom of the results table. Please note that the list of functions here may vary depending on the setup of the database.

.. image:: /images/data_export/isolate_export2.png

Select the isolate fields and schemes to include.

.. image:: /images/data_export/isolate_export3.png

Click Submit.

You can then download the data in tab-delimited text or Excel formats.

.. image:: /images/data_export/isolate_export4.png

Advanced options
================

.. image:: /images/data_export/isolate_export5.png

The options fieldset has the following options.

* Include locus common names - any common name for the locus is displayed in parentheses following the primary name.
* Export allele numbers - the allele designation is included for any locus included.
* Use one row per field - this is an alternative output format where instead of each locus and field having a separate column, each field is export on a separate row.
* Include isolate field in row - the name of the isolate is included as a separate column when exporting in 'one row per field' fomrmat.
* Export full allele designation record - export sender, curator and datestamp information as separate rows when exporting allele designation data.

Molecular weight calculation
============================
The plugin can also calculate the predicted molecular weight of the gene product of any allele designated in the dataset.

.. image:: /images/data_export/isolate_export6.png

Click the 'Export protein molecular weight' checkbox.  Additional columns (or rows depending on the output format) will be created to include the molecular weight data.

***************
Sequence export
***************
You can export the sequences for any set of loci designated in isolate records, or belonging to scheme profiles in the sequence definition database.

The sequence export function can be accessed by clicking the 'Sequences' link inthe Export section of the contents page.

.. image:: /images/data_export/sequence_export.png

Alternatively, you can access this function by clicking the ‘Sequences’ button in the Export list at the bottom of the results table. Please note that the list of functions here may vary depending on the setup of the database.

.. image:: /images/data_export/sequence_export2.png

Select the isolate or profile records to analyse - these will be pre-selected if you accessed the plugin following a query. Select the loci to include either directly within the loci list and/or using the schemes tree.

.. image:: /images/data_export/sequence_export3.png

Click submit.

.. image:: /images/data_export/sequence_export4.png

The job will be submitted to the job queue.  Click the link to follow the progress and download the resulting files.

Sequences will be export in XMFA and FASTA file formats.

.. image:: /images/data_export/sequence_export5.png

Aligning sequences
==================
By default, sequences will be exported unaligned - this is very quick since no processing is required.  You can choose to align the sequences by checking the 'Align sequences' checkbox.

.. image:: /images/data_export/sequence_export6.png

You can also choose to use MUSCLE or MAFFT as the aligner.  MAFFT is the default choice and is usually much quicker than MUSCLE.  Both produce comparable results.

*********************
Sequence table export
*********************

.. todo:: Add description.

*************
Contig export
*************

.. todo:: Add description.

