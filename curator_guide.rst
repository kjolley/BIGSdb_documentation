###############
Curator's guide
###############

Please note that links displayed within the curation interface will vary depending on database contents and the permissions of the curator.

*************************
Adding new sender details
*************************
All records within the databases are associated with a sender.  Whenever somebody new submits data, they should be added to the users table so that their name appears in the dropdown lists on the data upload forms.

To add a user, click the add users (+) link on the curator's contents page.

.. image:: /images/curation/add_users.png 

Enter the user's details in to the form.

.. image:: /images/curation/add_users2.png 

Normally the status should be set as 'user'.  Only admins and curators with special permissions can create users with a status of curator or admin.

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

.. todo:: Add description.

*************************************
Adding new scheme profile definitions
*************************************

.. todo:: Add description.

************************************************
Updating and deleting scheme profile definitions
************************************************

.. todo:: Add description.

**********************
Adding isolate records
**********************

.. todo:: Add description.

********************************************
Updating and deleting single isolate records
********************************************

.. todo:: Add description.

**********************************
Batch updating of multiple records
**********************************

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
