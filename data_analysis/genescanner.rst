.. index::
   single: GeneScanner; 
   
.. _genescanner:

***********
GeneScanner
***********
GeneScanner is a mutation analysis pipeline for aligned sequences.
It reads nucleotide, protein, or both types of FASTA alignments and produces:

  * Per-position mutation summaries with synonymous vs. non-synonymous 
    classification.
  * Detection of protein mutations types and location.
  * Group-wise comparisons.
  
GeneScanner can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/analysis.png

Jump to the 'Analysis' category, follow the link to 'GeneScanner', then click 
'Launch GeneScanner'.

.. image:: /images/data_analysis/genescanner.png

Alternatively, it can be accessed following a query by clicking the 
‘GeneScanner’ button at the bottom of the results table. Isolates returned 
from the query will be automatically selected within the GeneScanner interface.

.. image:: /images/data_analysis/genescanner2.png

Select the isolate ids to include a sequence to analyse against. This can
either be a pre-defined locus selected from the locus list, or you can paste
in your own sequence. This can be either a DNA or protein sequence.

.. image:: /images/data_analysis/genescanner3.png

Choose whether to perform a nucleotide or protein analysis (or both). You can
also select one of the sequence ids in your list to be the reference sequence,
otherwise the first sequence will be used.

.. image:: /images/data_analysis/genescanner4.png

Click 'Submit' to start the analysis.

The main output is an Excel file. See the GeneScanner documentation at 
https://github.com/jeju2486/GeneScanner/wiki/GeneScanner for details.

.. image:: /images/data_analysis/genescanner5.png
