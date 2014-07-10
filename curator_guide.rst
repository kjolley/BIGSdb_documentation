###############
Curator's guide
###############

Please note that links displayed within the curation interface will vary depending on database contents and the permissions of the curator.

.. index::
   single: users; adding

*************************
Adding new sender details
*************************
All records within the databases are associated with a sender.  Whenever somebody new submits data, they should be added to the users table so that their name appears in the dropdown lists on the data upload forms.

To add a user, click the add users (+) link on the curator's contents page.

.. image:: /images/curation/add_users.png 

Enter the user's details in to the form.

.. image:: /images/curation/add_users2.png 

Normally the status should be set as 'user'.  Only admins and curators with special permissions can create users with a status of curator or admin.

.. index::
   single: allele sequences; adding

**************************************
Adding new allele sequence definitions
**************************************

Single allele
=============
To add a single new allele, click the sequences (all loci) add (+) link on the curator's main page - if only a few loci are defined with permission for the current user to curate then they will be listed individually and the specific locus allele addition links can also be used.

.. image:: /images/curation/add_alleles.png 

Select the locus from the dropdown list box. The next available allele id will be entered automatically (if the allele id format is set to integer). Paste the sequence in to form, set the status and select the sender name from the dropdown box. If the sender does not appear in the box, you will need to add them to the registered users.

The status can either be:

* Sanger trace checked
* WGS: manual extract
* WGS: automated extract
* unchecked

.. image:: /images/curation/add_alleles2.png 

Press submit. By default, the system will test whether your sequence is similar enough to existing alleles defined for that locus. The sequence will be rejected if it isn't considered similar enough. This test can be overridden by checking the 'Override sequence similarity check' checkbox at the bottom.

Sequences can be flagged with specific attributes - these are searchable when doing a sequence attribute query.  These are mainly for use with whole genome MLST type data.  Multiple flags can be selected by Ctrl-clicking the list.  Available flags are:

* atypical
* contains IS element
* downstream fusion
* frameshift
* internal stop codon
* no start codon
* phase variable: off
* truncated
* upstream fusion

Sequences can also be associated with PubMed, ENA or Genbank id numbers by entering these as lists (one value per line) in the appropriate form box.

Batch adding multiple alleles
=============================
There are two methods of batch adding alleles.  You can either upload a spreadsheet with all fields in tabular format, or you can upload a FASTA file provided all sequences are for the same locus and have the same status.

Upload using a spreadsheet
--------------------------
Click the batch add (++) sequences (all loci) link on the curator's main page.

.. image:: /images/curation/add_alleles3.png 

Download a template Excel file from the following page.

.. image:: /images/curation/add_alleles4.png

Fill in the spreadsheet.  If the locus uses integer allele identifiers, the allele_id can be left blank and the next available number will be used automatically.   Paste the entire sheet in to the web form and select the sender from the dropdown box.

Additionally, there are a number of options available.  Some of these will ignore sequences if they don't match certain criteria - this is useful when sequence data has been extracted from genomes automatically.  Available options are:

* Ignore existing or duplicate sequences.
* Ignore sequences containing non-nucleotide characters.
* Silently reject all sequences that are not complete reading frames - these must have a start and in-frame stop codon at the ends and no internal stop codons. Existing sequences are also ignored.
* Override sequence similarity check.

.. image:: /images/curation/add_alleles5.png

Press submit.  You will be presented with a page indicating what data will be uploaded.  This gives you a chance to back out of the upload.  Click 'Import data'.

.. image:: /images/curation/add_alleles6.png

If there are any problems with the submission, these should be indicated at this stage, e.g.:

.. image:: /images/curation/add_alleles7.png

Upload using a FASTA file
-------------------------
Uploading new alleles from a FASTA file is usually more straightforward than generating an Excel sheet.

Click 'FASTA' upload on the curator's contents page.

.. image:: /images/curation/add_alleles8.png

Select the locus, status and sender from the dropdown boxes and paste in the new sequences in FASTA format.

.. image:: /images/curation/add_alleles9.png

For loci with integer ids, the next available id number will be used by default (and the identifier in the FASTA file will be ignored).  Alternatively, you can indicate the allele identifier within the FASTA file (do not include the locus name in this identifier).

As with the spreadsheet upload, you can select options to ignore selected sequences if they don't match specific criteria.

Click 'Check'.

The sequences will be checked.  You will be presented with a page indicating what data will be uploaded.  This gives you a chance to back out of the upload.  Click 'Upload valid sequences'.

.. image:: /images/curation/add_alleles10.png

Any invalid sequences will be indicated in this confirmation page and these will not be uploaded (you can still upload the others), e.g.

.. image:: /images/curation/add_alleles11.png

*************************************************
Updating and deleting allele sequence definitions
*************************************************
.. note::

   You cannot update the sequence of an allele definition. This is for reasons of data integrity since an allele may form part of a scheme profile and be referred to in multiple databases. If you really need to change a sequence, you will have to remove the allele definition and then re-add it.

In order to update or delete an allele, first you must select it. Click the query (?) sequences (all loci) link - if only a few loci are defined with permission for the current user to curate then they will be listed individually and the specific locus query links can also be used.

.. image:: /images/curation/update_alleles.png

Either search for specific attributes in the search form, or leave it blank and click 'Submit' to return all alleles. For a specific allele, select the locus in the filter and enter the allele number in the allele_id field.

.. image:: /images/curation/update_alleles2.png

Click the appropriate link to either update the allele attributes or to delete it. If you have appropriate permissions, there may also be a link to 'Delete ALL'. This allows you to quickly delete all alleles returned from a search.

.. image:: /images/curation/update_alleles3.png

If you choose to delete, you will be presented with a final confirmation screen. To go ahead, click 'Delete!'. Deletion will not be possible if the allele is part of a scheme profile - if it is you will need to delete any profiles that it is a member of first.

.. image:: /images/curation/delete_allele.png

If instead you clicked 'Update', you will be able to modify attributes of the sequence, or link PubMed, ENA or Genbank records to it. You will not be able to modify the sequence itself.

.. note::

   Adding flags and  comments to an allele record requires that this feature is enabled in the :ref:`database configuration <seqdef_xml>`.

.. image:: /images/curation/update_alleles4.png

*************************************
Adding new scheme profile definitions
*************************************
Provided a scheme has been set up with at least one locus and a scheme field set as a primary key, there will be links on the curator's main page to add profiles for that scheme.

To add a single profile you can click the add (+) profiles link next to the scheme name (e.g. MLST):

.. image:: /images/curation/add_scheme_profile.png

A form will be displayed with the next available primary key number already entered (provided integers are used for the primary key format). Enter the new profile, associated scheme fields, and the sender, then click 'Submit'. The new profile will be added provided the primary key or the profile has not previously been entered.

.. image:: /images/curation/add_scheme_profile2.png

More usually, profiles are added in a batch mode. It is often easier to do this even for a single profile since it allows copying and pasting data from a spreadsheet.

Click the batch add (++) profiles link next to the scheme name:

.. image:: /images/curation/add_scheme_profile3.png

Click the 'Download submission template (xlsx format)' link to download an Excel submission template.

.. image:: /images/curation/add_scheme_profile4.png

Fill in the spreadsheet using the copied template, then copy and paste the whole spreadsheet in to the large form on the upload page. If the primary key has an integer format, you can exclude this column and the next available number will be used automatically. If the column is included, however, a value must be set.  Select the sender from the dropdown list box and then click 'Submit'.

.. image:: /images/curation/add_scheme_profile5.png

You will be given a final confirmation page stating what will be uploaded.  If you wish to proceed with the submission, click 'Import data'.

.. image:: /images/curation/add_scheme_profile6.png

************************************************
Updating and deleting scheme profile definitions
************************************************
In order to update or delete a scheme profile, first you must select it. Click the query (?) profiles link next to the scheme name (e.g. MLST):

.. image:: /images/curation/update_scheme_profile.png

Search for your profile by entering search criteria (alternatively you can use the browse or list query functions).

.. image:: /images/curation/update_scheme_profile2.png

To delete the profile, click the 'Delete' link next to the profile. Alternatively, if your account has permission, you may be able to 'Delete ALL' records retrieved from the search.

For deletion of a single record, the full record will be displayed. Confirm deletion by clicking 'Delete!'.

.. image:: /images/curation/delete_scheme_profile.png

To modify the profile, click the 'Update' link next to the profile following the query. A form will be displayed - make any changes and then click 'Update'.

.. image:: /images/curation/update_scheme_profile3.png

**********************
Adding isolate records
**********************
To add a single record, click the add (+) isolates link on the curator's index page.

.. image:: /images/curation/add_isolate.png

The next available id will be filled in automatically but you are free to change this. Fill in the individual fields. Required fields are listed first and are marked with an exclamation mark (!). Some fields may have drop-down list boxes of allowed values. You can also enter allele designations for any loci that have been defined.

.. image:: /images/curation/add_isolate2.png

Press submit when finished.

More usually, isolate records are added in batch mode, even when only a single record is added, since the submission can be prepared in a spreadsheet and copied and pasted.

Select batch add (++) isolates link on the curator's index page.

.. image:: /images/curation/add_isolate3.png

Download a submission template in Excel format from the link.

.. image:: /images/curation/add_isolate4.png

Prepare your data in the spreadsheet - the column headings must match the database fields.  In databases with large numbers of loci, there won't be columns for each of these.  You can, however, manually add locus columns.

Pick a sender from the drop-down list box and paste the data from your spreadsheet in to the web form. The next available isolate id number will be used automatically (this can be overridden if you manually add an id column).

.. image:: /images/curation/add_isolate5.png

Press submit. Data are checked for consistency and if there are no problems you can then confirm the submission.

.. image:: /images/curation/add_isolate6.png

Any problems with the data will be listed and highlighted within the table. Fix the data and resubmit if this happens.

.. image:: /images/curation/add_isolate7.png

********************************************
Updating and deleting single isolate records
********************************************
First you need to locate the isolate record. You can either browse or use a search or list query.

.. image:: /images/curation/update_isolate.png

The query interface is the same as the :ref:`public query interface <isolate_query>`. Following a query, a results table of isolates will be displayed. There will be delete and update links for each record.

.. image:: /images/curation/update_isolate2.png

Clicking the 'Delete' link takes you to a page displaying the full isolate record. 

.. image:: /images/curation/delete_isolate.png

Pressing 'Delete' from this record page confirms the deletion. 

Clicking the 'Update' link for an isolate takes you to an update form. Make the required changes and click 'Update'.

.. image:: /images/curation/update_isolate3.png

Allele designations can also be updated by clicking within the scheme tree and selecting the 'Add' or 'Update' link next to a displayed locus.

.. image:: /images/curation/update_isolate4.png

.. image:: /images/curation/update_isolate5.png

Schemes will only appear in the tree if data for at least one of the loci within the scheme has been added.  You can additionally add or update allelic designations for a locus by choosing a locus in the drop-down list box and clicking 'Add/update'.

.. image:: /images/curation/update_isolate6.png

The allele designation update page allows you to modify an existing designation, or alternatively add additional designations. The sender, status (confirmed/provisional) and method (manual/automatic) needs to be set for each designation (all pending designations have a provisional status). The method is used to differentiate designations that have been determined manually from those determined by an automated algorithm.

.. image:: /images/curation/update_isolate7.png

***************************************
Batch updating multiple isolate records
***************************************
Select 'batch update' isolates link on the curator's index page.

.. image:: /images/curation/batch_update_isolate.png

Prepare your update data in 3 columns in a spreadsheet:

#. Unique identifier field
#. Field to be updated
#. New value for field

You should also include a header line at the top - this isn't used so can contain anything but it should be present.

Columns must be tab-delimited which they will be if you copy and paste directly from the spreadsheet.

So, to update isolate id-100 and id-101 to serogroup B you would prepare the following: ::

  id     field     value
  100    serogroup B
  101    serogroup B

Select the field you are using as a unique identifier, in this case id, from the drop-down list box, and paste in the data. If the fields already have values set, you should also check the 'Overwrite existing data' checkbox.  Press 'submit'.

.. image:: /images/curation/batch_update_isolate2.png

A confirmation page will be displayed if there are no problems. If there are problems, these will be listed.  Press 'Upload' to upload the changes.

.. image:: /images/curation/batch_update_isolate3.png

You can also use a secondary selection field such that a combination of two fields uniquely defines the isolate, for example using country and isolate name.

So, for example, to update the serogroups of isolates CN100 and CN103, both from the UK, select the appropriate primary and secondary fields and prepare the data as follows: ::

  isolate     country     field      value
  CN100       UK          serogroup  B
  CN103	      UK	  serogroup  B

*********************************
Deleting multiple isolate records
*********************************

.. note::

   Please note that standard curator accounts may not have permission to delete multiple isolates. Administrator accounts are always able to do this.

Before you can delete multiple records, you need to search for them. From the curator's main page, click the Query isolates link:

.. image:: /images/curation/batch_delete_isolate.png

Enter search criteria that specifically return the isolates you wish to delete. Click 'Delete ALL'.

.. image:: /images/curation/batch_delete_isolate2.png

You will have a final chance to change your mind:

.. image:: /images/curation/batch_delete_isolate3.png

Click 'Confirm deletion!'.

****************************************************
Uploading sequence contigs linked to isolate records
****************************************************

Select isolate from drop-down list
==================================
To upload sequence data, click the sequences batch add (++) link on the curator's main page.

.. image:: /images/curation/upload_contigs.png

Select the isolate that you wish to link the sequence to from the dropdown list box. You also need to enter the person who sent the data. Optionally, you can add the sequencing method used.

Paste sequence contigs in FASTA format in to the form.

.. image:: /images/curation/upload_contigs2.png

Click 'Submit'. A summary of the number of isolates and their lengths will be displayed. To confirm upload, click 'Upload'.

.. image:: /images/curation/upload_contigs3.png

It is also possible to upload data for multiple isolates at the same time, but these must exist as single contigs for each isolate. To do this, select 'Read identifier from FASTA' in the isolate id field and select the field that you wish to use as the identifier in the 'identifier field', e.g. to use isolate names select 'isolate' here.

.. image:: /images/curation/upload_contigs4.png

Provided the identifier used uniquely identifies the isolate you will get a confirmation screen. If the isolate name does not do this you'll probably have to use the database id number instead. Click 'Upload' to confirm.

.. image:: /images/curation/upload_contigs5.png

Select from isolate query
=========================
As an alternative to selecting the isolate from a dropdown list (which can become unwieldy for large databases), it is also possible to upload sequence data following an isolate query.

Click the isolate query link from the curator's main page.

.. image:: /images/curation/upload_contigs6.png

Enter your search criteria. From the list of isolates displayed, click the 'Upload' link in the sequence bin column of the appropriate isolate record.

.. image:: /images/curation/upload_contigs7.png

The same upload form as detailed above is shown. Instead of a dropdown list for isolate selection, however, the chosen isolate will be pre-selected.

.. image:: /images/curation/upload_contigs8.png

Upload options
==============
On the upload form, you can select to filter out short sequences from your contig list.

If your database has experiments defined (experiments are used for grouping sequences and can be used to filter the sequences used in :ref:`tag scanning <tag_scanning>`), you can also choose to upload your contigs as part of an experiment. To do this, select the experiment from the dropdown list box.

.. image:: /images/curation/upload_contigs9.png

.. _tag_scanning:

************************************
Automated web-based sequence tagging
************************************

.. todo:: Add description.

********
Projects
********

.. todo:: Add description.

*************************
Isolate record versioning
*************************

.. todo:: Add description.
