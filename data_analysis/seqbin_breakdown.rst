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

There is also an option to determine the mean G+C content and various assembly
stats of the sequence bin of each isolate. Note that selecting these will make
the analysis run much slower since each contig needs to be examined.

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
