#####################
Data analysis plugins
#####################

.. index::
   single: Locus Explorer

.. _locus_explorer:

**************
Locus explorer
**************
The locus explorer is a sequence definition database plugin.  It can create 
schematics showing the polymorphic sites within a locus, calculate the GC 
content and generate aligned translated sequences.

Click 'Locus Explorer' from the sequence definition database contents page. 

.. image:: /images/data_analysis/locus_explorer.png 

.. index::
   pair: Locus Explorer; polymorphic sites

.. _locus_explorer_snp:

Polymorphic site analysis
=========================
Select the locus you would like to analyse in the Locus dropdown box.  The page
will reload.

.. image:: /images/data_analysis/locus_explorer2.png 

Select the alleles that you would like to include in the analysis.  Variable 
length loci are limited to 2000 sequences or fewer since these need to be 
aligned.  Select 'Polymorphic Sites' in the Analysis selection and click 
'Submit'.

.. image:: /images/data_analysis/locus_explorer3.png 

If an alignment is necessary, the job will be submitted to the job queue and 
the analysis performed.  If no alignment is necessary, then the analysis is 
shown immediately.

The first part of the page shows the schematic.

.. image:: /images/data_analysis/locus_explorer4.png 

Clicking any of the sequence bases will calculate the exact frequencies of the
different nucleotides at that position.

.. image:: /images/data_analysis/locus_explorer5.png 

.. image:: /images/data_analysis/locus_explorer6.png 

The second part of the page shows a table listing nucleotide frequencies at 
each of the variable positions.

.. image:: /images/data_analysis/locus_explorer7.png 

.. seealso::

   * :ref:`Investigating allele differences <allele_differences>`.
   * :ref:`Polymorphism analysis following isolate query <polymorphisms>`.

.. index::
   pair: Locus Explorer; codon usage

Codon usage
===========
Select the alleles that you would like to include in the analysis. Again, 
variable length loci are limited to 200 sequences or fewer since these need to
be aligned. Click ‘Codon’.

.. image:: /images/data_analysis/locus_explorer8.png 

The GC content of the alleles will be determined and a table of the codon 
frequencies displayed.

.. image:: /images/data_analysis/locus_explorer9.png 

.. index::
   pair: Locus Explorer; translated sequences

Aligned translations
====================
If a DNA coding sequence locus is selected, an aligned translation can be 
produced.

Select the alleles that you would like to include in the analysis. Again, 
variable length loci are limited to 200 sequences or fewer since these need 
to be aligned. Click ‘Translate’.

.. image:: /images/data_analysis/locus_explorer10.png

An aligned amino acid sequence will be displayed.

.. image:: /images/data_analysis/locus_explorer11.png

If there appear to be a lot of stop codons in the translation, it is possible 
that the orf value in the :ref:`locus definition <add_new_loci>` is not set 
correctly.

.. index::
   pair: breakdown; provenance field

***************
Field breakdown
***************
The field breakdown plugin for isolate databases displays the frequency of each
value for fields stored in the isolates table. 
:ref:`Allele and scheme field breakdowns <scheme_breakdown>` are handled by a 
different plugin.

The breakdown function can be selected for the whole database by clicking the 
'Single field' link in the Breakdown section of the main contents page.

.. image:: /images/data_analysis/field_breakdown.png

Alternatively, a breakdown can be displayed of the dataset returned from a 
query by clicking the 'Fields' button in the Breakdown list at the bottom of 
the results table. Please note that the list of functions here may vary 
depending on the setup of the database.

.. image:: /images/data_analysis/field_breakdown2.png

A series of charts will be displayed. Pick the field to display from the list 
at the top.

.. image:: /images/data_analysis/field_breakdown3.png

The values used to generate the chart can be displayed or extracted by clicking
the 'Table' link at the bottom of the page. 

.. image:: /images/data_analysis/field_breakdown4.png

This displays a table that can be ordered by clicking the appropriate header.

.. image:: /images/data_analysis/field_breakdown5.png

The data can also be downloaded in tab-delimited text or Excel formats by 
clicking the appropriate links.

.. image:: /images/data_analysis/field_breakdown6.png

.. index::
   pair: breakdown; two-field

*******************
Two field breakdown
*******************
The two field breakdown plugin displays a table breaking down one field against
another, e.g. breakdown of serogroup by year.

The analysis can be selected for the whole database by clicking the 'Two field
breakdown' link on the main contents page.

.. image:: /images/data_analysis/two_field_breakdown.png

Alternatively, a two field breakdown can be displayed of the dataset returned 
from a query by clicking the 'Two field' button in the Breakdown list at the 
bottom of the results table. Please note that the list of functions here may 
vary depending on the setup of the database.

.. image:: /images/data_analysis/two_field_breakdown2.png

Select the two fields you wish to breakdown and how you would like the values 
displayed (percentage/absolute values and totaling options).

.. image:: /images/data_analysis/two_field_breakdown3.png

Click submit. The breakdown will be displayed as a table. Bar charts will also
be displayed provided the number of returned values for both fields are fewer 
than 30.

.. image:: /images/data_analysis/two_field_breakdown4.png

The table values can be exported in a format suitable for copying in to a 
spreadsheet by clicking 'Download as tab-delimited text' underneath the table.

.. index::
   pair: breakdown; scheme
   pair: breakdown; allele

.. _scheme_breakdown:

***************************
Scheme and allele breakdown
***************************
The scheme and allele breakdown plugin displays the frequency of each allele 
and scheme field (e.g. ST or clonal complex).

The function can be selected for the whole database by clicking the 'Scheme 
and allele breakdown' link on the main contents page.

.. image:: /images/data_analysis/scheme_breakdown.png

Alternatively, a breakdown can be displayed of the dataset returned from a 
query by clicking the 'Schemes/alleles' button in the Breakdown list at the 
bottom of the results table. Please note that the list of functions here may 
vary depending on the setup of the database.

.. image:: /images/data_analysis/scheme_breakdown2.png

A scheme tree is shown.  Select any combination of schemes to analyse. Click 
'Select'.

.. image:: /images/data_analysis/scheme_breakdown3.png


A table showing the number of unique values for each locus and scheme field 
will be displayed.

.. image:: /images/data_analysis/scheme_breakdown4.png

A detailed display of allele or field frequencies can be displayed by clicking 
the appropriate 'Breakdown' button. 

.. image:: /images/data_analysis/scheme_breakdown5.png

The sorting of the table can be changed by clicking the appropriate header - 
this toggles between ascending and descending order.

.. image:: /images/data_analysis/scheme_breakdown6.png

The table values can be exported in a format suitable for copying in to a 
spreadsheet by clicking the 'Tab-delimited text' button.

.. image:: /images/data_analysis/scheme_breakdown7.png

You can also download the sequeneces for alleles designated in the dataset for 
the loci belonging to the scheme by clicking the appropriate 'Download' button 
in the first results table.

.. image:: /images/data_analysis/scheme_breakdown8.png

Sequences will be served in FASTA format in order of frequency. ::

  >2
  TTTGATACCGTTGCCGAAGGTTTGGGTGAAATTCGCGATTTATTGCGCCGTTACCACCGC
  GTCGGCCATGAGTTGGAAAACGGTTCGGGTGAGGCTTTGTTGAAAGAACTCAACGAATTA
  CAACTTGAAATCGAAGCGAAGGACGGCTGGAAGCTGGATGCGGCAGTCAAGCAGACTTTG
  GGGGAACTCGGTTTGCCGGAAAACGAAAAAATCGGCAACCTTTCCGGCGGTCAGAAAAAG
  CGTGTCGCCTTGGCGCAGGCTTGGGTGCAGAAGCCCGACGTATTGCTGCTGGACGAACCG
  ACCAACCATTTGGATATCGACGCGATTATTTGGCTGGAAAATCTGCTCAAAGCGTTTGAA
  GGCAGCTTGGTTGTGATTACCCACGACCGCCGTTTTTTGGACAATATCGCCACGCGGATT
  GTCGAACTCGATC
  >1
  TTTGATACTGTTGCCGAAGGTTTGGGCGAAATTCGCGATTTATTGCGCCGTTATCATCAT
  GTCAGCCATGAGTTGGAAAATGGTTCGAGTGAGGCCTTATTGAAAGAGCTCAACGAATTG
  CAACTTGAGATCGAAGCGAAGGACGGCTGGAAGTTGGATGCGGCGGTGAAGCAGACTTTG
  GGCGAACTCGGTTTGCCGGAAAACGAAAAAATCGGCAACCTCTCCGGCGGTCAGAAAAAG
  CGCGTCGCCTTGGCGCAGGCTTGGGTGCAGAAGCCCGACGTATTGCTGCTCGATGAACCG
  ACCAACCATTTGGACATCGACGCGATTATTTGGTTGGAAAACCTGCTCAAAGCGTTTGAA
  GGCAGCCTGGTTGTGATTACCCACGACCGCCGTTTTTTGGACAATATCGCCACGCGGATT
  GTCGAACTCGATC
  >4
  TTTGATACCGTTGCCGAAGGTTTGGGCGAAATTCGTGATTTATTGCGCCGTTATCATCAT
  GTCAGCCATGAGTTGGAAAATGGTTCGAGTGAGGCTTTGTTGAAAGAACTCAACGAATTG
  CAACTTGAAATCGAAGCGAAGGACGGCTGGAAACTGGATGCGGCAGTCAAGCAGACTTTG
  GGGGAACTCGGTTTGCCGGAAAATGAAAAAATCGGCAACCTTTCCGGCGGTCAGAAAAAG
  CGCGTCGCCTTGGCTCAGGCTTGGGTGCAAAAGCCCGACGTATTGCTGCTGGACGAGCCG
  ACCAACCATTTGGATATCGACGCGATTATTTGGCTGGAAAATCTGCTCAAAGCGTTTGAA
  GGCAGCTTGGTTGTGATTACCCACGACCGCCGTTTTTTGGACAATATCGCCACGCGGATT
  GTCGAACTCGATC

.. index::
   pair: breakdown; sequence bin

**********************
Sequence bin breakdown
**********************
The sequence bin breakdown plugin calculates statistics based on the number 
and length of contigs in the sequence bin as well as the number of loci tagged
for an isolate record.

The function can be selected by clicking the ‘Sequence bin’ link on the 
Breakdown section of the main contents page.

.. image:: /images/data_analysis/seqbin_breakdown.png 

Alternatively, it can be accessed following a query by clicking the ‘Sequence 
bin’ button in the Breakdown list at the bottom of the results table. Please 
note that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/seqbin_breakdown2.png 

Select the isolate records to analyse - these will be pre-selected if you 
accessed the plugin following a query.  You can also select loci and/or schemes
which will be used to calculate the totals and percentages of loci designated
and tagged.  This may be useful as a guide to assembly quality if you use a 
scheme of core loci where a good assembly would be expected to include all
member loci.  To determine the total of all loci designated or tagged, click 
'All loci' in the scheme tree.  

There is also an option to determine the mean G+C content of the sequence bin
of each isolate.

Click submit.

.. image:: /images/data_analysis/seqbin_breakdown3.png 

If there are fewer than 100 isolates selected, the table will be generated 
immediately.  Otherwise it will be submitted to the job queue.

A table of sequence bin stats will be generated.

.. image:: /images/data_analysis/seqbin_breakdown4.png 

You can choose to export the data in tab-delimited text or Excel formats by 
clicking the appropriate link at the bottom of the table.

.. image:: /images/data_analysis/seqbin_breakdown5.png

:ref:`Sequence bin records <sequence_bin_records>` can also be accessed by 
clicking the 'Display' button for each row of the table.

.. image:: /images/data_analysis/seqbin_breakdown6.png 

.. index::
   single: Genome Comparator
   
.. _genome_comparator:

*****************
Genome comparator
*****************
Genome Comparator is an optional plugin that can be enabled for specific 
databases. It is used to compare whole genome data of isolates within the 
database using either the database defined loci or the coding sequences of an 
annotated genome as the comparator.

Output is equivalent to a whole genome MLST profile, a distance matrix 
calculated based on allelic differences and a NeighborNet graph generated from 
this distance matrix.

Genome Comparator can be accessed on databases where it is enabled from the 
contents page by clicking the 'Genome Comparator' link.

.. image:: /images/data_analysis/genome_comparator.png 

Alternatively, it can be accessed following a query by clicking the 'Genome 
Comparator' button at the bottom of the results table.  Isolates with sequence 
data returned in the query will be automatically selected within the Genome 
Comparator interface.

.. image:: /images/data_analysis/genome_comparator2.png

Analysis using defined loci
===========================
Select the isolate genomes that you wish to analyse and then either the loci 
from the list or a set of schemes.  Press submit.

.. image:: /images/data_analysis/genome_comparator3.png

The job will be submitted to the job queue and will start running shortly. 
Click the link to follow the job progress and view the output.

.. image:: /images/data_analysis/genome_comparator4.png

There will be a series of tables displaying variable loci, colour-coded to 
indicate allelic differences. Finally, there will be links to a distance 
matrix which can be loaded in to SplitsTree for further analysis and to a 
NeighborNet chart showing relatedness of isolates. Due to processing 
constraints on the web server, this NeighborNet is only calculated if 200 or 
fewer genomes are selected for analysis, but this can be generated in the 
stand-alone version of SplitsTree using the distance matrix if required.

.. image:: /images/data_analysis/genome_comparator5.png

Analysis using annotated reference genome
=========================================
Select the isolate genomes that you wish to analyse and then either enter a
Genbank accession number for the reference genome, or select from the list of
reference genomes (this list will only be present if the administrator has 
:ref:`set it up <isolate_xml>`). Selecting reference genomes will hide the 
locus and scheme selection forms.

.. image:: /images/data_analysis/genome_comparator6.png

Output is similar to when comparing against defined loci, but this time every
coding sequence in the annotated reference will be BLASTed against the selected
genomes. Because allele designations are not defined, the allele found in the
reference genome is designated allele 1, the next different sequence is allele
2 etc.

.. image:: /images/data_analysis/genome_comparator10.png

Include in identifiers fieldset
===============================
This selection box allows you to choose which isolate provenance fields will be
included in the results table.  This does not affect the output of the 
alignments as taxa names are limited in length by the alignment programs.

.. image:: /images/data_analysis/genome_comparator7.png

Multiple values can be selected by clicking while holding down Ctrl.

Reference genome fieldset
=========================
This section allows you to choose a reference genome to use as the source of
comparator sequences.

.. image:: /images/data_analysis/genome_comparator8.png

There are three possibilities here:

#. Enter accession number - Enter a Genbank accession number of an annotated 
   reference and Genome Comparator will automatically retrieve this from 
   Genbank.
#. Select from list - The administrator may have selected some genomes to 
   offer for comparison.  If these are present, simply select from the list.
#. Upload genome - Click 'Browse' and upload your own reference.  This can 
   either be in Genbank, EMBL or FASTA format.  Ensure that the filename ends 
   in the appropriate file extension (.gb, .embl, .fas) so that it is 
   recognized.

Parameters/options fieldset
===========================
This section allows you to modify BLAST parameters.  This affects sensitivity
and speed.

.. image:: /images/data_analysis/genome_comparator9.png

* Min % identity - This sets the threshold identity that a matching sequence
  has to be in order to be considered (default: 70%).  Only the best match is
  used.
* Min % alignment - This sets the percentage of the length of reference allele
  sequence that the alignment has to cover in order to be considered (default: 
  50%).
* BLASTN word size - This is the length of the initial identical match that
  BLAST requires before extending a match (default: 20).  Increasing this value
  improves speed at the expense of sensitivity.  The default value gives good
  results in most cases.  The default setting used to be 15 but the new default
  of 20 is almost as good (there was 1 difference among 2000 loci in a test 
  run) but the analysis runs twice as fast.
* Use TBLASTX - This compares the six-frame translation of your nucleotide
  query sequence against the six-frame translation of the contig sequences. 
  Sequences will be classed as identical if they result in the same translated
  sequence even if the nucleotide sequence is different.  This is significantly
  slower than using BLASTN.

Additionally, two other options are available in this fieldset:

* Use tagged designations - When analysing using defined loci, Genome
  Comparator can use the designations stored within the database (this is the
  default).  This is much quicker since it doesn't need to run BLAST against
  these sequences.  If a designation is missing, BLAST will be run for that
  locus anyway.
* Disable HTML output - If running Genome Comparator against a large number of
  genomes, the resulting table may get so large that your web browser struggles
  to render it properly and may use up too much memory on your computer. 
  Clicking this button prevents this output - this output is not required for
  further analysis since everything present in it is also generated in Excel
  format at the end.  HTML output is automatically disabled when more than 150
  genomes are analysed. 

Distance matrix calculation fieldset
====================================
This section provides options for the treatment of incomplete and paralogous
loci when generating the distance matrix.  

.. image:: /images/data_analysis/genome_comparator11.png

For incomplete loci, i.e. those that continue beyond the end of a contig so
are incomplete you can:

* Completely exclude from analysis - Any locus that is incomplete in at least 
  one isolate will be removed from the analysis completely.  Using this option
  means that if there is one bad genome with a lot of incomplete sequences in
  your analysis, a large proportion of the loci may not be used to calculate
  distances.

* Treat as a distinct allele - This treats all incomplete sequences as a
  specific allele 'I'.  This varies from any other allele, but all incomplete
  sequences will be treated as though they were identical.

* Ignore in pairwise comparison (default) - This is probably the best option.
  In this case, incomplete alleles are only excluded from the analysis when
  comparing the particular isolate that has it.  Other isolates with different
  alleles will be properly included.  The effect of this option will be to
  shorten the distances of isolates with poorly sequenced genomes with the
  others.

Paralogous loci, i.e. those with multiple good matches, can be excluded from
the analysis (default).  This is the safest option since there is no guarantee
that differences seen between isolates at paralogous loci are real if the
alternative matches are equally good.  NB: Loci are also only classed as
paralogous when the alternative matches identify different sequences, otherwise
multiple contigs of the same sequence region would result in false positives.

When paralogous loci are excluded, there are two further options:

* Exclude when paralogous in all isolates (default).  Loci are only classed as
  paralogous when there are multiple hits in every genome (except if a genome
  is missing the locus entirely, in which case that genome is ignored in the
  calculation).  This is generally the option that you will want to use with
  the default BLAST parameters since you can often expect multiple hits even
  when loci are not paralogous if you have used relaxed thresholds.
* Exclude when paralogous in any isolate.  Unless you use stringent BLAST
  thresholds, this is likely to overestimate the number of paralogous loci, but
  may be useful if you are specifically looking for them.

Alignments fieldset
===================
This section enables you to choose to produce alignments of the sequences 
identified.  

.. image:: /images/data_analysis/genome_comparator12.png

Available options are:

* Produce alignments - Selecting this will produce the alignment files, as well
  as XMFA and FASTA outputs of aligned sequences.  This will result in the 
  analysis taking approximately twice as long to run.
* Include ref sequences in alignment - When doing analysis using an annotated 
  reference, selecting this will include the reference sequence in the 
  alignment files.
* Align all loci - By default, only loci that vary among the isolates are 
  aligned.  You may however wish to align all if you would like the resultant 
  XMFA and FASTA files to include all coding sequences.
* Aligner - There are currently two choices of alignment algorithm (provided 
  they have both been installed)

  * MAFFT (default) - This is the preferred option as it is significantly 
    quicker than MUSCLE, uses less memory, and produces comparable results.
  * MUSCLE - This was originally the only choice. It is still included to 
    enable previous analyses to be re-run and compared but it is recommended 
    that MAFFT isused otherwise.

Core genome analysis fieldset
=============================
This section enables you to modify the inclusion threshold used to calculate 
whether or not a locus is part of the core genome (of the dataset).

.. image:: /images/data_analysis/genome_comparator13.png

The default setting of 90% means that a locus is counted as core if it appears
within 90% or more of the genomes in the dataset.

There is also an option to calculate the mean distance among sequences of the 
loci.  Selecting this will also select the option to produce alignments.

Filter fieldset
===============
This section allows you to further filter your collection of isolates and the 
contigs to include.  

.. image:: /images/data_analysis/genome_comparator14.png

Available options are:

* Sequence method - Choose to only analyse contigs that have been generated 
  using a particular method.  This depends on the method being set when the 
  contigs were uploaded.
* Project - Only include isolates belonging to the chosen project.  This 
  enables you to select all isolates and filter to a project.
* Experiment - Contig files can belong to an experiment.  How this is used can
  vary between databases, but this enables you to only include contigs from a 
  particular experiment.

Understanding the output
========================

Distance matrix
---------------
The distance matrix is simply a count of the number of loci that differ between
each pair of isolates.  It is generated in NEXUS format which can be used as 
the input file for `SplitsTree <http://www.splitstree.org>`_.  This can be used
to generate NeighborNet, Split decomposition graphs and trees offline.  If 200 
isolates or fewer are included in the analysis, a Neighbor network is 
automatically generated from this distance matrix.

Unique strains
--------------
The table of unique strains is a list of isolates that are identical at every 
locus.  Every isolate is likely to be classed as unique if a whole genome 
analysis is performed, but with a constrained set of loci, such as those for 
MLST, this will group isolates that are indistinguishable at that level of 
resolution.

.. index::
   single: BLAST

*****
BLAST
*****
The BLAST plugin enables you to BLAST a sequence against any of the genomes in 
the database, displaying a table of matches and extracting matching sequences.

The function can be accessed by selecting the 'BLAST' link on the Analysis 
section of the main contents page.

.. image:: /images/data_analysis/blast.png

Alternatively,it can be accessed following a query by clicking the 'BLAST' 
button in the Analysis list at the bottom of the results table.  Please note 
that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/blast2.png

Select the isolate records to analyse - these will be pre-selected if you 
accessed the plugin following a query.  Paste in a sequence to query - this 
be either a DNA or peptide sequence.

.. image:: /images/data_analysis/blast3.png

Click submit.

A table of BLAST results will be displayed.

.. image:: /images/data_analysis/blast4.png

Clicking any of the 'extract' buttons will display the matched sequence along 
with a translated sequence and flanking sequences. 

.. image:: /images/data_analysis/blast5.png 

.. image:: /images/data_analysis/blast6.png

At the bottom of the results table are links to export the matching sequences 
in FASTA format, (optionall) including flanking sequnces.  You can also export
the table in tab-delimited text or Excel formats.

.. image:: /images/data_analysis/blast11.png

Include in results table fieldset
=================================
This selection box allows you to choose which isolate provenance fields will 
be included in the results table.

.. image:: /images/data_analysis/blast7.png

Multiple values can be selected by clicking while holding down Ctrl.

Parameters fieldset
===================
This section allows you to modify BLAST parameters.  This affects sensitivity 
and speed.

.. image:: /images/data_analysis/blast8.png

* BLASTN word size - This is the length of the initial identical match that 
  BLAST requires before extending a match (default: 11). Increasing this value
  improves speed at the expense of sensitivity.
* BLASTN scoring - This is a dropdown box of combinations of identical base 
  rewards; mismatch penalties; and gap open and extension penalties.  BLASTN 
  has a constrained list of allowed values which reflects the available options
  in the list.
* Hits per isolate - By default, only the best match is shown.  Increase this 
  value to the number of hits you'd like to see per isolate.
* Flanking length - Set the size of the upstream and downstream flanking 
  sequences that you'd like to include.
* Use TBLASTX - This compares the six-frame translation of your nucleotide 
  query sequence against the six-frame translation of the contig sequences. 
  This is significantly slower than using BLASTN.

No matches
==========

.. image:: /images/data_analysis/blast9.png

Click this option to create a row in the table indicating that a match was not
found.  This can be useful when screening a large number of isolates.

Filter fieldset
===============
This section allows you to further filter your collection of isolates and the 
contig sequences to include.

.. image:: /images/data_analysis/blast10.png

Available options are:

* Sequence method - Choose to only analyse contigs that have been generated 
  using a particular method. This depends on the method being set when the 
  contigs were uploaded.
* Project - Only include isolates belonging to the chosen project. This 
  enables you to select all isolates and filter to a project.
* Experiment - Contig files can belong to an experiment. How this is used can
  vary between databases, but this enables you to only include contigs from a 
  particular experiment.

.. index::
   single: BURST

*****
BURST
*****
BURST is an algorithm used to group MLST-type data based on a count of the 
number of profiles that match each other at specified numbers of loci.  The 
analysis is available for both sequence definition database and isolate 
database schemes that have primary key fields set.  The algorithm has to be 
:ref:`specifically enabled <enabling_plugins>` by an administrator.  Analysis 
is limited to 1000 or fewer records.

The plugin can be accessed following a query by clicking the 'BURST' button in 
the Analysis list at the bottom of the results table. Please note that the list
of functions here may vary depending on the setup of the database.

.. image:: /images/data_analysis/burst.png 

If there multiple schemes that can be analysed, these can then be selected 
along with the group definition.

.. image:: /images/data_analysis/burst2.png

Modifying the  group definition affects the size of groups and how they link 
together.  By default, the definition is n-2 (where n is the number of loci), 
so for example on a 7 locus MLST scheme groups contain STs that match at 5 or 
more loci to any other member of the group.

Click Submit.

A series of tables will be displayed indicating the groups of profiles.  Where
one profile can be identified as a central genotype, i.e. the profile that has 
the greatest number of other profiles that are single locus variants (SLV), 
double locus variants (DLV) and so on, a graphical representation will be 
displayed.  The central profile is indicated with an asterisk.

.. image:: /images/data_analysis/burst3.png

SLV profiles that match the central profile are shown within a red circle 
surrounding the central profile.  Most distant profiles (triple locus variants)
may be linked with a line.  Larger groups may additionally have DLV profiles.  
These are shown in a blue circle.

.. image:: /images/data_analysis/burst4.png 

Groups can get very large, where linked profiles form sub-groups and an attempt
is made to depict these.

.. image:: /images/data_analysis/burst5.png

.. index::
   single: codon usage

.. _codon_usage_plugin:

***********
Codon usage
***********
The codon usage plugin for isolate databases calculates the absolute and 
relative synonymous codon usage by isolate and by locus.

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
shortly. Click the link to follow the job progress and view the output.
  
.. image:: /images/data_analysis/codon_usage4.png

Four tab-delimited text files will be created.

* Absolute frequency of codon usage by isolate
* Absolute frequency of codon usage by locus
* Relative synonymous codon usage by isolate
* Relative synonymous codon usage by locus

.. image:: /images/data_analysis/codon_usage5.png

.. index::
   single: unique combinations

*******************
Unique combinations
*******************
The Unique Combinations plugin calculates the frequencies of unique file 
combinations within an isolate dataset.  Provenance fields, composite fields, 
allele designations and scheme fields can be combined.

The function can be selected by clicking the 'Unique combinations' link in the
Breakdown section of the main contents page.  This will run the analysis on the
entire database.

.. image:: /images/data_analysis/unique_combinations.png

Alternatively, it can be accessed following a query by clicking the 
'Combinations' button in the Breakdown list at the bottom of the results table.
This will run the analysis on the dataset returned from the query.  Please 
note that the list of functions here may vary depending on the setup of the 
database.

.. image:: /images/data_analysis/unique_combinations2.png

Select the combination of fields to analyse, e.g. serogroup and finetyping 
antigens.

.. image:: /images/data_analysis/unique_combinations3.png

Click submit.  When the analysis has completed you will see a table showing the
unique combinations of the selected fields along with the frequency and 
percentage of the combination.

.. image:: /images/data_analysis/unique_combinations4.png

The table can be downloaded in tab-delimited text or Excel formats by clicking
the links at the bottom of the page.

.. image:: /images/data_analysis/unique_combinations5.png

.. index::
   single: polymorphisms

.. _polymorphisms:

*************
Polymorphisms
*************
The Polymorphisms plugin generates a :ref:`Locus Explorer <locus_explorer>` 
polymorphic site analysis on the alleles designated in an isolate dataset 
following a query.

The analysis is accessed by clicking the 'Polymorphic sites' button in the 
Breakdown list at the bottom of a results table following a query.

.. image:: /images/data_analysis/polymorphisms.png

Select the locus that you would like to analyse from the list.

.. image:: /images/data_analysis/polymorphisms2.png

Click 'Analyse'.

A schematic of the locus is generated showing the polymorphic sites.  A full 
description of this can be found in the 
:ref:`Locus Explorer polymorphic site analysis <locus_explorer_snp>` section.

.. image:: /images/data_analysis/polymorphisms3.png

****************
Presence/absence
****************
This plugin displays the status of loci for isolate records.  It will shown 
whether a locus has been designated with an allele name, has a sequence tag, 
or both.

The function can be selected by clicking the 'Presence/absence status of loci' 
link in the 'Analysis' section of the main contents page.

.. image:: /images/data_analysis/presence.png

Alternatively, it can be accessed following a query by clicking the 
‘Presence/Absence’ button in the Analysis list at the bottom of the results 
table. Please note that the list of functions here may vary depending on the 
setup of the database.

.. image:: /images/data_analysis/presence2.png

Enter the ids of the isolate records to analyse - these will be already entered
if you accessed the plugin following a query. Select the loci you would like to
analyse, either from the dropdown loci list, and/or by selecting one or more 
schemes.

.. image:: /images/data_analysis/presence3.png

Click submit. The job will be submitted to the queue and will start running 
shortly. Click the link to follow the job progress and view the output.

.. image:: /images/data_analysis/presence4.png

When complete, a single text file will have been generated.

.. image:: /images/data_analysis/presence5.png

This is a tab-delimited text file that uses 'O' to represent presence and 'X' 
to represent a missing locus designation or tag. ::

  id	pgm	adk	abcZ	pdhC	gdh	fumC	aroE
  1	O	O	O	O	O	O	O
  2	O	O	O	O	O	O	O
  3	O	O	O	O	O	O	O
  4	O	O	O	O	O	O	O
  5	O	O	O	O	O	O	O
  6	O	O	O	O	O	O	O
  7	O	O	O	O	O	O	O
  8	O	O	O	O	O	O	O
  9	O	O	O	O	O	O	O
  10	O	O	O	O	O	O	O

Options
=======
There are a number of options that can be selected to modify the output.

.. image:: /images/data_analysis/presence6.png

With these you can change the symbols used and whether designations, or tags,
or both are counted.

You can also choose to generate a distance matrix based on presence/absence.

.. index::
   single: sequence tag; status

**********
Tag status
**********
The tag status plugin displays a graphical representation of the status of loci
designations or tags for isolate data.  It is accessed following a query by 
clicking the 'Tag status' button in the Breakdown section at the bottom of the 
results table.

.. image:: /images/data_analysis/tag_status.png

Select the loci you would like to analyse.

.. image:: /images/data_analysis/tag_status2.png

You should see a series of bars representing loci.  The colour of these bars 
designates whether they have an allele designation only, a sequence tag only, 
both designations or tags, or whether they have flags set.

.. image:: /images/data_analysis/tag_status3.png

Hovering the mouse over the bars will indicate the scheme represented.

.. note::
   Loci will be represented more than once if they are members of multiple 
   selected schemes.

Clicking any of the isolate id hyperlinks navigates to a page that breaks down 
the exact status for all loci of that isolate.

.. image:: /images/data_analysis/tag_status4.png

There is a column each for allele designations and sequence tags.  If an 
allele designation is defined, the allele identifier is displayed.  Cells 
shaded in blue show that the designation or tag is present, whereas red 
indicates thet they are absent.

