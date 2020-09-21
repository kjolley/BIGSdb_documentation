.. _link_contigs:

.. index::
   single: linking remote contigs

*****************************************
Linking remote contigs to isolate records
*****************************************
If :ref:`remote contigs have been enabled<accessing_remote_contigs>`, isolates
can be linked to contigs stored in an external BIGSdb database, rather than
directly uploaded. These well then be loaded when needed, for example during 
scanning or data export. This will be marginally slower than hosting contigs 
within the same database, but minimises duplication of sequence data and 
associated storage. Contigs need to be accessible via the BIGSdb 
:ref:`RESTful API<restful_api>`.

Click the sequences link icon on the curator's main page.

.. image:: /images/curation/link_contigs.png

Either select the isolate id from the dropdown list, or enter it manually 
(list is disabled if there are >1000 records in the database). Enter the URI
for the RESTful API of the parent isolate record, e.g. 
http://rest.pubmlst.org/db/pubmlst_rmlst_isolates/isolates/933. This URI can
require authentication if credentials have been 
:ref:`set up<oauth_remote_contigs>`.

Press submit.

.. image:: /images/curation/link_contigs2.png

Summary information about the number of contigs and their total length will
be downloaded from the remote isolate record. You will then be prompted to
upload this information to the database, by clicking the 'Upload' button.

.. image:: /images/curation/link_contigs3.png

The contigs will be downloaded in bulk in order to determine their lengths. 
This information is stored within the local database as it is required for 
various outputs. Full metadata is not stored at this stage.

.. image:: /images/curation/link_contigs4.png

This is all that is required for the contigs to be used as normal. In order
to get the full metadata about the contigs (sequencing platform used, sender
and datestamp information), you can choose to process the contigs by clicking
the 'Process contigs now' button. This will download each contig in turn, and
store its provenance metadata locally. 

.. image:: /images/curation/link_contigs5.png

Alternatively, this step can be 
:ref:`performed offline automatically<processing_remote_contigs>`. 
