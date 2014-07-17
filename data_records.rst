############
Data records
############
Record pages for different types of data can be accessed following a query by clicking appropriate hyperlinks.

.. index::
   pair: isolate; records 

.. _isolate_records:

***************
Isolate records
***************
An Isolate record page displays everything known about an isolate.  

.. image:: /images/data_records/isolate_record.png

Each record will have some or all of the following sections:

Projects
========

.. image:: /images/data_records/isolate_record2.png

This displays a list of projects that the isolate is a member of.  Only projects that have a full description will be displayed. 

Provenance metadata
===================

.. image:: /images/data_records/isolate_record3.png

This section includes:

* provenance fields
* housekeeping data

  * who sent the isolate
  * who last curated
  * record creation times
  * last update times
  * links to update history

The update link displays page with exact times of who and when updated the record.

.. image:: /images/data_records/isolate_record7.png

Publications
============

.. image:: /images/data_records/isolate_record8.png

This section includes full citation for papers linked to the isolate record.  Each citation has a button that will return a dataset of all isolates linked to the paper.

If there are five or more references they will be hidden by default to avoid cluttering the page too much.  Click the 'Show/hide' button to display them in this case.

Sequence bin summary
====================

.. image:: /images/data_records/isolate_record4.png

This section contains basic statistics describing the sequence bin.  Clicking the 'Display' button navigates to the :ref:`sequence bin record <sequence_bin_records>`.

Scheme and locus data
=====================
A hierarchical tree displays available schemes.  Click within internal nodes to expand them. 

.. image:: /images/data_records/isolate_record5.png

Clicking any terminal node will display data available for a scheme or group of schemes.

.. image:: /images/data_records/isolate_record6.png

Click an allele number within the scheme profile, will display the appropriate :ref:`allele definition record <allele_definition_records>`.  Clicking the green 'S' link will display the appropriate :ref:`sequence tag record <sequence_tag_records>`.

.. index::
   pair: allele definition; records 

.. _allele_definition_records:

*************************
Allele definition records
*************************
An allele definition record displays information about a defined allele in a sequence definition database.

.. image:: /images/data_records/allele_definition_record.png

If the allele is a member of a scheme profile, e.g. MLST, this will be listed.  In this case, there will be a button to display all profiles of that scheme that contain the allele.

Similarly, if a :ref:`client database <client_databases>` has been setup for the database and the allele has been identified in an isolate, there will be a button to display all isolates that have that allele.

.. index::
   pair: sequence tag; records 

.. _sequence_tag_records:

********************
Sequence tag records
********************

.. image:: /images/data_records/sequence_tag_record.png

A sequence tag record displays information about the location within a contig of a region associated with a locus.  The nucleotide sequence will be displayed along with upstream and downstream flanking sequence.  The length of these flanking sequences can be modified within the :ref:`general options <general_options>`.

If the tag is for a DNA locus and it is marked as a coding sequence, the three-frame translation will also be displayed.

.. index::
   pair: profile; records 

.. _profile_records:

***************
Profile records
***************

.. image:: /images/data_records/profile_record.png

A profile record displays information about a scheme, e.g. MLST, profile.  Each allele number within the profile will be hyperlinked.  Clicking these will take you to the appropriate :ref:`allele definition record <allele_definition_records>`.

If a :ref:`client database <client_databases>` has been setup for the database and an isolate has the profile, there will be a button to display all isolates that have the profile.

.. index::
   pair: sequence bin; records 

.. _sequence_bin_records:

********************
Sequence bin records
********************

.. image:: /images/data_records/seqbin_record.png

A sequence bin record contains information about that contigs associated with an isolate record.  This includes:

* Number of contigs
* Total length
* Minimum length
* Maximum length
* N50, N90 and N95 values
* Size distribution charts

There are also links to download the contigs in FASTA or EMBL format.

Finally there is a table that shows the loci that are tagged on each contig.  Individual contigs can also be downloaded in EMBL format.
