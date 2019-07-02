*************
Contig export
*************
The contig export plugin can be accessed by clicking the ‘Contigs’ link in the 
Export section of the contents page of isolate databases.

.. image:: /images/data_export/contig_export.png

Alternatively, it can be accessed following a query by clicking the ‘Contigs’ 
button in the Export section at the bottom of the results table.

.. image:: /images/data_export/contig_export2.png

Select the isolates for which you wish to export contig data for. If the 
export function was accessed following a query, isolates returned in the query 
will be pre-selected.

.. image:: /images/data_export/contig_export3.png

At its simplest, press submit.

A table will be produced with download links.  Clicking these will produce the 
contigs in FASTA format.

.. image:: /images/data_export/contig_export4.png

You can also download all the data in a tar file by clicking the 'Batch 
download' link.

.. image:: /images/data_export/contig_export5.png

Filtering by tagged status of contigs
=====================================
You can also export contigs based on the percentage of the sequence that has 
been tagged.  This is useful to find sequences to target for gene discovery.

In order to export contigs where at least half the sequence has been tagged 
(and also the remaining contigs in a separate file), select '50' in the 
dropdown box for %untagged.

.. image:: /images/data_export/contig_export6.png

The resulting table has two download links for each isolate, one for contigs 
matching the condition, and one for contigs that don't match.

.. image:: /images/data_export/contig_export7.png
