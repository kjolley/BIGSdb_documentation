.. index::
   pair: Microreact; spatio-temporaral trees

**********
Microreact
**********
Microreact is a tool for visualising genomic epidemiology and phylogeography.
Individual nodes on a displayed tree are linked to nodes on a geographical map
and/or timeline, making any spatial and temporal relationships between isolates
apparent.

The Microreact plugin generates Neighbour-joining trees from concatenated
sequences for any selection of loci or schemes and uploads these, together with
country and year field values to the `Microreact website
<https://microreact.org>`_ for display.

.. note::

 While Microreact itself is able to display isolates using GPS coordinates, the
 BIGSdb plugin is currently limited to the level of country.
 
Microreact can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/analysis.png

Jump to the 'Third party' category, follow the link to Microreact, then click 
'Launch Microreact'.

.. image:: /images/data_analysis/microreact1.png 

Alternatively, it can be accessed following a query by clicking the 
'Microreact' button at the bottom of the results table.  Isolates returned 
from the query will be automatically selected within the Microreact plugin
interface.

.. image:: /images/data_analysis/microreact2.png

Select the isolates to include. The tree can be generated from allelic profiles
of any selection of loci, or more conveniently, you can select a scheme in the
scheme selector, or from a list of recommended schemes if these have been set,
to include all loci belonging to that scheme.

Additional fields can be selected to be included as metadata for use in 
colouring nodes - select any fields you wish to include. Multiple selections
can be made by holding down shift or ctrl while selecting. Click 'Submit' to 
start the analysis.

.. image:: /images/data_analysis/microreact3.png

The job will be sent to the job queue. When it has finished, click the button
marked 'Launch Microreact'.

.. image:: /images/data_analysis/microreact4.png

The generated tree will be uploaded to the Microreact website and displayed.
Clicking any node will show its position(s) within the tree, map and timeline.
A node on the map may correspond to multiple nodes in the tree or timeline.

.. image:: /images/data_analysis/microreact5.png
