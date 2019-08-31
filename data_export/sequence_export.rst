***************
Sequence export
***************
You can export the sequences for any set of loci designated in isolate records,
or belonging to scheme profiles in the sequence definition database.

The sequence export function can be accessed by clicking the 'Sequences' link 
in the Export section of the contents page of isolate databases, or the 
'Profile sequences' link of sequence definition databases.

.. image:: /images/data_export/sequence_export.png

Alternatively, you can access this function by clicking the ‘Sequences’ button
in the Export list at the bottom of the results table. Please note that the
list of functions here may vary depending on the setup of the database.

.. image:: /images/data_export/sequence_export2.png

Select the isolate or profile records to analyse - these will be pre-selected
if you accessed the plugin following a query. Select the loci to include either
directly within the loci list and/or using the schemes tree.

.. image:: /images/data_export/sequence_export3.png

Click submit.

.. image:: /images/data_export/sequence_export4.png

The job will be submitted to the job queue.  Click the link to follow the
progress and download the resulting files.

Sequences will be export in XMFA and FASTA file formats.

.. image:: /images/data_export/sequence_export5.png

Aligning sequences
==================
By default, sequences will be exported unaligned - this is very quick since no 
processing is required.  You can choose to align the sequences by checking 
the 'Align sequences' checkbox.

.. image:: /images/data_export/sequence_export6.png

You can also choose to use MUSCLE or MAFFT as the aligner.  MAFFT is the 
default choice and is usually much quicker than MUSCLE.  Both produce 
comparable results.
