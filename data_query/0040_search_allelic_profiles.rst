.. index::
   pair: query; ST definitions from allelic profiles

.. _profile_definitions:

***************************************
Identifying allelic profile definitions
***************************************
For schemes such as MLST you can query allelic combinations to identify 
the sequence type (or more generically, the primary key of the profile).

Click the 'By allelic profile' link in the 'Search for allelic profiles'
section on a the sequence definition contents page.

.. image:: /images/data_query/allelic_profile1.png

If multiple schemes are defined in the database you should select the scheme
you wish to check.

.. image:: /images/data_query/allelic_profile2.png

Enter a combination of allelic values (you can enter a partial profile if you
wish).

.. image:: /images/data_query/allelic_profile3.png

Alternatively, you can automatically populate a profile by entering a value
for the scheme primary key field (e.g. ST) and clicking 'Autofill'.

.. image:: /images/data_query/allelic_profile4.png

To find the closest or exact match, leave the search box on 'Exact or nearest
match' and click 'Submit'. The best match will be displayed.

.. image:: /images/data_query/allelic_profile5.png

Alternatively, if you wish to find all profiles that match the query profile
by at least a set number of loci, select the appropriate value in the search
dropdown box, e.g. '4 or more matches' will show related profiles that share
at least 4 alleles with the query.

.. image:: /images/data_query/allelic_profile6.png

.. index::
   pair: query; batch profile definitions

.. _batch_profile_queries:

*********************
Batch profile queries
*********************
To lookup scheme definitions, e.g. the sequence type for multiple profiles, 
click 'In a batch' from the 'Search for allelic profiles' section of the
sequence definition contents page.

.. image:: /images/data_query/batch_profile1.png

If multiple schemes are defined in the database you should select the scheme
you wish to check.

.. image:: /images/data_query/batch_profile2.png

Copy and paste data from a spreadsheet. The first column is the record 
identifier, and the remaining columns are the alleles for each locus in the
standard locus order defined for the scheme. There are links to the column
order which can be used as a header line for your spreadsheet and to example
data.

Click submit after pasting in the data.

.. image:: /images/data_query/batch_profile3.png

A results table will be displayed.

.. image:: /images/data_query/batch_profile4.png
