###########################################
Submitting data using the submission system
###########################################
The automated submission system allows users to submit data (new alleles,
profiles, or isolates) to the database curators for assignment and upload to
the database. The submission system is enabled on a per-database basis so will
not always be available.

If the system is enabled, new submissions can be made by clicking the 'Manage
submissions' link on the database front page.

.. image:: /images/submissions/submission1.png

**************************
Registering a user account
**************************
You must have an account for the appropriate database in order to use the 
submission system.  On systems utilizing site-wide databases, such as PubMLST,
this can be done automatically via the web. Other sites may require you to
contact a curator to set this up.

*****************
Allele submission
*****************
New allele data can only be submitted from within the appropriate sequence 
definition database.  Submissions consist of one or more new allele sequences
for a single locus.  You will need to create separate submissions for each 
locus - this is because different loci may be handled by different curators.

Start
=====
Click the 'alleles' link under submission type on the submission management 
page.

.. image:: /images/submissions/submission2.png

Select the submission locus
===========================
Select the locus from the locus list box:

.. image:: /images/submissions/submission3.png

The locus list may be very long in some databases.  It may be possible to 
filter these to those belonging to specific schemes.  If the scheme tree is
shown, select the appropriate scheme, e.g. 'MLST' and click 'Filter'.

.. image:: /images/submissions/submission4.png
   
The locus list is now constrained making selection easier.
   
.. image:: /images/submissions/submission5.png

Enter details of sequencing method
==================================
There are a number of fields that must be filled in so that the curator knows
how the sequence was obtained:

* technology - the sequncing platform used, allowed values are:
   
  * 454
  * Illumina
  * Ion Torrent
  * PacBio
  * Oxford Nanopore
  * Sanger
  * Solexa
  * SOLiD
  * other
  * unknown
     
* read length - this is the length of sequencing reads. This is a required 
  field for Illumina data, and not relevant to Sanger sequencing. Allowed 
  values are:

  * <100
  * 100-199
  * 200-299
  * 300-499
  * >500
  
* coverage - the mean number of reads covering each nucleotide position of 
  the sequence.  This is not relevant to Sanger sequencing,  Allowed values
  are:
  
  * <20x
  * 20-49x
  * 50-99x
  * >100x
  
* assembly - the means of generating the submitted sequence from the 
  sequencing reads.  Allowed values are:
  
  * de novo
  * mapped
  
* assembly software - this is a free text field where you should enter the 
  name of the software used to generate the submitted sequence.
  
Paste in sequence(s)
====================
Paste in the new variant sequences to the box.  This can either be a stand-
alone sequence or multiple sequences in FASTA format.  The sequences must be
trimmed to the start and end points of the loci - check existing allele 
definitions if in doubt.  The submission is likely to be rejected if sequences
are not trimmed.  Click submit.
   
.. image:: /images/submissions/submission6.png
   
The system will perform some basic checks on the submitted sequences.  If any 
of the sequences have been defined previously they must be removed from the
submission before you can proceed.  Curators do not want to waste their time
dealing with previously defined sequences.

.. image:: /images/submissions/submission7.png

Assuming the preliminary checks have passed you will then be able to add 
additional information to your submission.

.. image:: /images/submissions/submission8.png

Add message to curator
======================
If you wish to enter a message to the curator, enter this in the messages
box and click 'Append'. This is not normally necessary for routine submissions.

.. image:: /images/submissions/submission9.png

The message will be attached.  A curator may respond to the message and attach
their own, with the full conversation becoming part of the submission record.

.. image:: /images/submissions/submission10.png

Add supporting files
====================
Some submissions will require the attachment of supporting files.  This will
depend on the policies of the individual databases.  Sequences determined by
Sanger sequencing should normally have forward and reverse trace files 
attached.

Files can be added to the submission by dragging and dropping in to the large
dotted area in the 'Supporting files' section. Alternatively, you can click 
this area and select files from the local file system.

.. image:: /images/submissions/submission11.png

The files will be uploaded and shown in a table.

.. image:: /images/submissions/submission13.png

Files can be removed from the submission by checking the appropriate 'Delete'
box and clicking 'Delete selected files'.

Finalize submission
===================
Make sure the 'E-mail submission updates' box is checked if you wish to receive
E-mail notification of the result of your submission.  This setting is 
remembered between submissions.

Click 'Finalize submission!'.

.. image:: /images/submissions/submission14.png

Your submission will then be listed under 'Pending submissions' on your 
submission page.

.. image:: /images/submissions/submission15.png

******************
Profile submission
******************

Start
=====
.. note::

   Most MLST databases on PubMLST.org require you to submit an isolate record
   for each new ST that you wish to be defined. In these cases, you should add
   the isolate name to the id field of your profile submission and make a
   corresponding :ref:`isolate submission<isolate_submissions>` containing the 
   allelic profile.

Click the appropriate profiles link under submission type on the submission 
management page.

.. image:: /images/submissions/submission16.png

Download the Excel submission template.

.. image:: /images/submissions/submission17.png

Paste in profile(s)
===================
Fill in the template.  The first column 'id' can be used to enter an identifier
that is meaningful to you - it is used to report back the results but is not
uploaded to the database.  It can be left blank, or the entire column can be
removed - in which case individual profiles will be identified by row number.

Copy and paste the entire contents of the submission worksheet. Click submit.

.. image:: /images/submissions/submission18.png

Some basic checks will be performed.  These include whether the profile has
already been assigned and whether each allele identifier exists.  The 
submission cannot proceed if the checks fail.

.. image:: /images/submissions/submission19.png

Provided the checks pass, you will then be able to add additional information
to your submission. New profile submissions usually don't require supporting
files directly in the submission. You generally will need to make a 
corresponding :ref:`submission to the isolate database<isolate_submissions>` 
though.

Add message to curator
======================
If you wish to enter a message to the curator, enter this in the messages box
and click 'Append'.

.. image:: /images/submissions/submission20.png

The message will be attached.  A curator may respond to the message and attach
their own, with the full conversation becoming part of the submission record.

.. image:: /images/submissions/submission21.png

Finalize submission
===================
Make sure the 'E-mail submission updates' box is checked if you wish to receive
E-mail notification of the result of your submission.  This setting is 
remembered between sessions.

Click 'Finalize submission!'.

.. image:: /images/submissions/submission22.png

Your submission will then be listed under 'Pending submissions' on your 
submission page.

.. image:: /images/submissions/submission23.png

.. _isolate_submissions: 

******************
Isolate submission
******************
New isolate data can only be submitted from within the appropriate isolate
database.  You may be required to submit isolate data if you would like to get
a new MLST sequence type defined, but this depends on individual database 
policy.

Start
=====
Click the 'isolates' link under submission type on the submission management
page.

.. image:: /images/submissions/submission24.png

Download the Excel submission template.

.. image:: /images/submissions/submission25.png

Paste in isolate data
=====================
Fill in the template.  Some fields are required and cannot be left blank.  
Check the 'Description of database fields' link on the database contents page
to see a description of the fields and allowed values where these have been
defined.  Where allowed values have been set, the template will have dropdown
boxes (although these require newer versions of Excel to work).

Some databases may have hundreds of loci defined, and most will not have a 
column in the template. You can add new columns for any loci that have been 
defined and for which you would like to include allelic information for. 
These locus names must be the primary locus identifier.  A list of loci can be
found in the 'allowed_loci' tab of the Excel submission template.

Copy and paste the entire contents of the submission worksheet. Click submit.

.. image:: /images/submissions/submission26.png

Some basic checks will be performed.  These include checking all field values
conform to allowed lists or data types.  The submission cannot proceed if any
checks fail.

.. image:: /images/submissions/submission27.png

Provided the checks pass, you will then be able to add additional information
to your submission.

.. _isolate_submission_message:

Add message to curator
======================
If you wish to enter a message to the curator, enter this in the messages box
and click 'Append'.

.. image:: /images/submissions/submission28.png

The message will be attached.  A curator may respond to the message and attach
their own, with the full conversation becoming part of the submission record.

.. image:: /images/submissions/submission29.png

Add supporting files
====================
You can add any files required to support the submission, although this is not
normally needed for an isolate submission (if you wish to submit genome 
assemblies then you need to make a :ref:`genome submission<genome_submission>`,
rather than an isolate submission.

Files can be added to the submission
by dragging and dropping in to the large dotted area in the ‘Supporting files’
section. Alternatively, you can click this area and select files from the local
file system.

.. image:: /images/submissions/submission30.png

Finalize submission
===================
Make sure the 'E-mail submission updates' box is checked if you wish to receive
E-mail notification of the result of your submission.  This setting is 
remembered between sessions.

Click 'Finalize submission!'.

.. image:: /images/submissions/submission33.png

Your submission will then be listed under 'Pending submissions' on your 
submission page.

.. image:: /images/submissions/submission34.png

.. _genome_submission:

*****************
Genome submission
*****************
Submitting genomes uses the same process as standard 
:ref:`isolate submission<isolate_submissions>`. The only difference is that 
there are a couple of extra required fields in the submission table:

* assembly_filename - this is the name of the FASTA file containing the
  assembly contigs. This must be uploaded as a supporting file - you will not
  be able to finalize the submission until every isolate record has a matching
  contig file.
  
* sequence_method - the sequencing technology used to generate the sequences. 
  The allowed values are listed on the submission page.
  
To start the submission, click the 'genomes' link under submission type on the
submission management page.

.. image:: /images/submissions/submission36.png

Then follow the steps for :ref:`isolate submission<isolate_submissions>`, 
uploading the contigs files as supporting files.

************************************************
Removing submissions from your notification list
************************************************
Once a submission has been closed by a curator, the results will be displayed
in your 'Manage submissions' area.  You can remove submissions once you have 
noted the result by clicking the 'Remove' link.

.. image:: /images/submissions/submission35.png

Alternatively, submissions will be removed automatically a specified period of
time after closure.  By default, this time is 90 days, but this can vary 
depending on the site configuration.
