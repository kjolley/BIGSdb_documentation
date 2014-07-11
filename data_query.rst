#############
Querying data
#############

.. _sequence_query:

.. index::
   pair: identify; allele sequence

***********************************************
Querying sequences to determine allele identity
***********************************************
Sequence queries are performed in the sequence definition database.   Click 'Sequence query' from the contents page.

.. image:: /images/data_query/sequence_query.png 

Paste your sequence in to the box - there is no need to trim. Normally, you can leave the locus setting on 'All loci' - the software should identify the correct locus based on your sequence.  Sometimes, it may be quicker, however, to select the specific locus or scheme (e.g. MLST) that a locus belongs to. 

.. note::

   If the locus you are querying is a shorter version of another, e.g. an MLST fragment of a gene where the full length gene is also defined, you will need to select the specific locus or the scheme from the dropdown box.  Leaving the selection on 'All loci' will return a match to the longer sequence in preference to the shorter one. 

Click 'Submit'.

.. image:: /images/data_query/sequence_query2.png 

If an exact match is found, this will be indicated along with the start position of the locus within your sequence.

.. image:: /images/data_query/sequence_query3.png 

If only a partial match is found, the most similar allele is identified along with any nucleotide differences. The varying nucleotide positions are numbered both relative to the pasted in sequence and to the reference sequence. The start position of the locus within your sequence is also indicated.

.. image:: /images/data_query/sequence_query4.png 

As an alternative to pasting a sequence in to the box, you can also choose to upload sequences in FASTA format by clicking the file browse button.

.. image:: /images/data_query/sequence_query5.png 

.. index::
   pair: identify; sequence type

Querying whole genome data
==========================
The sequenced query is not limited to single genes.  You can also paste or upload whole genomes - these can be in multiple contigs.  If you select a specific scheme from the dropdown box, all loci belonging to that scheme will be checked (although only exact matches are reported for a locus if one of the other loci has an exact match).  If all loci are matched, scheme fields will also be returned if these are defined.  This, for example, enables you to identify the MLST sequence type of a genome in one step.

.. image:: /images/data_query/sequence_query6.png

.. _locus_specific_query:

*****************************************
Searching for specific allele definitions
*****************************************

.. todo:: Add description.

.. index::
   pair: browse; scheme profiles

***********************************
Browsing scheme profile definitions
***********************************
If a sequence definition database has schemes defined that include a primary key field, i.e. collections of loci that together create profiles, e.g. for MLST, click the link to 'Browse profiles'. 

.. image:: /images/data_query/browse_profiles.png

Choose the field to order the results by, the number of results per page to display, and click 'Browse all records'.

.. image:: /images/data_query/browse_profiles2.png

Clicking the hyperlink for any profile will display full information about the profile.

.. image:: /images/data_query/browse_profiles3.png

.. index::
   pair: query; scheme profiles

***********************************
Querying scheme profile definitions
***********************************
click the link to 'Search profiles' for the appropriate scheme on the main contents page.

.. image:: /images/data_query/query_profiles.png

Enter the search criteria you wish to search on. You may also see some drop-down list boxes that allow further filtering of results.  You can add search criteria by clicking the '+' button in the 'Locus/scheme fields' section.  These can be combined using 'AND' or 'OR'. 

.. image:: /images/data_query/query_profiles2.png

Each field can be queried using the following modifiers:

* =

  * Case insensitive exact match.

* contains

  * Case insensitive match to a partial string, e.g. searching for clonal complex 'contains' st-11 would return all STs belonging to the ST-11 complex.

* starts with

  * Match to values that start with the search term (case insensitive).

* ends with

  * Match to values that end with the search term (case sensitive).

* >

  * Greater than the search term.

* <

  * Less than the search term.

* NOT

  * Match to values that do not equal the search term (case insensitive).

* NOT contain

  * Match to values that do not contain the search term (case insensitive).

Clicking the hyperlink for any profile will display full information about the profile.

.. image:: /images/data_query/query_profiles3.png

.. _allele_differences:

********************************
Investigating allele differences
********************************

.. index::
   single: sequence similarity; determining

Sequence similarity
===================
To find sequences most similar to a selected allele within a sequence definition database, click 'Sequence similarity' on the contents page.

.. image:: /images/data_query/sequence_similarity.png

Enter the locus and allele identifer of the sequence to investigate and the number of nearest matches you'd like to see, then press submit.

.. image:: /images/data_query/sequence_similarity2.png

A list of nearest alleles will be displayed, along with the percentage identity and number of gaps between the sequences.

.. image:: /images/data_query/sequence_similarity3.png

Click the appropriate 'Compare' button to display a list of nucleotide differences and/or a sequence alignment.

.. image:: /images/data_query/sequence_similarity4.png

Sequence comparison
===================
To directly compare two sequences click 'Sequence comparison' from the contents page of a sequence definition database.

.. image:: /images/data_query/sequence_comparison.png

Enter the locus and two allele identifiers to compare.  Press submit.

.. image:: /images/data_query/sequence_comparison2.png

A list of nucleotide differences and/or an alignment will be displayed.

.. image:: /images/data_query/sequence_comparison3.png

.. seealso::

   :ref:`Locus explorer plugin <locus_explorer>`.

.. _isolate_query:

*********************
Querying isolate data
*********************
The 'Search database' page of an isolate database allows you to search by combinations of provenance criteria, scheme and locus data, and more. 

.. image:: /images/data_query/query_isolates.png

To start with, only one provenance field search box is displayed but more can be added by clicking the '+' button (highlighted). These can be linked together by 'and' or 'or'.

.. image:: /images/data_query/query_isolates2.png

After the search has been submitted, the results will be displayed in a table.

.. image:: /images/data_query/query_isolates3.png

Each field can be queried using the following modifiers:

* =

  * Case insensitive exact match.

* contains

  * Case insensitive match to a partial string, e.g. searching for clonal complex 'contains' st-11 would return all STs belonging to the ST-11 complex.

* starts with

  * Match to values that start with the search term (case insensitive).

* ends with

  * Match to values that end with the search term (case sensitive).

* >

  * Greater than the search term.

* <

  * Less than the search term.

* NOT

  * Match to values that do not equal the search term (case insensitive).

* NOT contain

  * Match to values that do not contain the search term (case insensitive).

More search features are available by clicking the 'Modify form options' tab on the right-hand side of the screen.

.. image:: /images/data_query/query_isolates4.png

A tab will be displayed.  Different options will be available here depending on the database.  Possible options are:

* Allele designations/scheme field values

  * Search by combination of allele designations and/or scheme fields e.g. ST, clonal complex information.

* Allele designation status

  * Search by whether allele designation status is confirmed or provisional.

* Tagged sequence status

  * Search by whether tagged sequence data is available for a locus.  You can also search by sequence flags.

* Filters

  * Various filters may be available, including

    * Publications
    * Projects
    * MLST profile completion status
    * Clonal complex
    * Sequence bin size
    * Inclusion/exclusion of :ref:`old versions <versioning>` 

.. image:: /images/data_query/query_isolates5.png

Query by allele_designation/scheme field
========================================
Make sure that the allele designation/scheme field values fieldset is displayed by selecting it in the 'Modify form options' tab.

.. image:: /images/data_query/query_isolates6.png

Designations can be queried using the following modifiers:

* =

  * Case insensitive exact match.

* contains

  * Case insensitive match to a partial string, e.g. searching for clonal complex 'contains' st-11 would return all STs belonging to the ST-11 complex.

* starts with

  * Match to values that start with the search term (case insensitive).

* ends with

  * Match to values that end with the search term (case sensitive).

* >

  * Greater than the search term.

* <

  * Less than the search term.

* NOT

  * Match to values that do not equal the search term (case insensitive).

* NOT contain

  * Match to values that do not contain the search term (case insensitive).

Additional search terms can be combined using the '+' button.

.. image:: /images/data_query/query_isolates7.png

Query by allele designation status
==================================

.. todo:: Add description.

Query by tagged sequence status
===============================

.. todo:: Add description.

Query filters
=============

.. todo:: Add description.

*************************
User-configurable options
*************************

.. index::
   pair: provenance fields; modifying display
   single: options; display
   single: options; querying

General options
===============

.. index::
   pair: schemes; modifying display
   pair: loci; modifying display

Modifying locus and scheme display options
==========================================

.. todo:: Add description.

***************************
Querying by allelic profile
***************************

.. todo:: Add description.

***************************************
Retrieving list of isolates or profiles
***************************************

.. todo:: Add description.

*****************************************
Retrieving isolates by linked publication
*****************************************

.. todo:: Add description.



