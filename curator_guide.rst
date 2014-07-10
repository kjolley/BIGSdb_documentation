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

.. todo:: Add description.

***************************************
Batch updating multiple isolate records
***************************************

.. todo:: Add description.

*********************************
Deleting multiple isolate records
*********************************

.. todo:: Add description.

*************************************************
Setting and modifying isolate allele designations
*************************************************

.. todo:: Add description.

****************************************************
Uploading sequence contigs linked to isolate records
****************************************************

.. todo:: Add description.

.. _tag_scanning:

************************************
Automated web-based sequence tagging
************************************

.. todo:: Add description.

********
Projects
********

.. todo:: Add description.
