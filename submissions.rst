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
submission system.  This will need to be set up by a curator, so contact them
in the first instance.

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
alone sequence or multiple sequences in FASTA format.  Click submit.
   
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
box and click 'Add message'.  

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

Files can be added to the submission by clicking the 'Browse' button in the
'Supporting files' section.

.. image:: /images/submissions/submission11.png

Select the file in the selection box, then click 'Upload files'.

.. image:: /images/submissions/submission12.png

The file will be uploaded and shown in a table.

.. image:: /images/submissions/submission13.png

Files can be removed from the submission, by checking the appropriate 'Delete'
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
Even if the submission system has been enabled, submission of profiles has to
be specifically enabled.  Many databases require submission of representative
isolate data for any new allelic profile for schemes such as MLST.  In this
case any new profiles can be readily extracted from the isoate data so profiles
do not need to be submitted separately.

Start
=====
Click the appropriate profiles link under submission type on the submission 
management page.

.. image:: /images/submissions/submission16.png

Download the Excel submission template

.. image:: /images/submissions/submission17.png

Paste in profile(s)
===================
Fill in the template.  The first column 'id' can be used to enter an identifier
that is meaningful to you - it is used to report back the results but is not
uploaded to the database.  It can be left blank, or the entire column can be
removed - in which case individual profiles will be identified by row number.
Click submit.

.. image:: /images/submissions/submission18.png

Some basic checks will be performed.  These include whether the profile has
already been assigned and whether each allele identifier exists.  The 
submission cannot proceed if the checks fail.

.. image:: /images/submissions/submission19.png

Provided the checks pass, you will then be able to add additional information
to your submission

Add message to curator
======================
If you wish to enter a message to the curator, enter this in the messages box
and click 'Add message'.

.. image:: /images/submissions/submission20.png

The message will be attached.  A curator may respond to the message and attach
their own, with the full conversation becoming part of the submission record.

.. image:: /images/submissions/submission21.png

Add supporting files
====================
Some submissions may require the attachment of supporting files.  These files 
can be added to the submission by clicking the 'Browse' button in the 
'Supporting files' section.

Select the file in the selection box,then click 'Upload files'.

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