.. index::
   pair: GrapeTree; minimum-spanning trees

*********
GrapeTree
*********
GrapeTree is a tool for generating and visualising minimum spanning trees. It 
has been developed to handle large datasets (in the region of 1000s of genomes)
and works with 1000s of loci as used in cgMLST. It uses an improved minimum
spanning algorithm that is better able to handle missing data than alternative
algorithms and is able to produce publication quality outputs. Datasets can
include metadata which allows nodes in the resultant tree to be coloured 
interactively.

GrapeTree can be accessed from the contents page by clicking the 'GrapeTree'
link.

.. image:: /images/data_analysis/grapetree.png 

Alternatively, it can be accessed following a query by clicking the 'GrapeTree'
button at the bottom of the results table.  Isolates returned from the query 
will be automatically selected within the GrapeTree interface.

.. image:: /images/data_analysis/grapetree2.png

Select the isolates to include. The tree can be generated from allelic profiles
of any selection of loci, or more conveniently, you can select a scheme in the
scheme selector to include all loci belonging to that scheme.

Additional fields can be selected to be included as metadata for use in 
colouring nodes - select any fields you wish to include. Multiple selections
can be made by holding down shift or ctrl while selecting. Click 'Submit' to 
start the analysis.

.. image:: /images/data_analysis/grapetree3.png

The job will be sent to the job queue. When it has finished, click the button
marked 'Launch GrapeTree'.

.. image:: /images/data_analysis/grapetree4.png

The generated tree will be rendered in the GrapeTree application page.

.. image:: /images/data_analysis/grapetree5.png

The image can be manipulated in various ways. These include modifying the tree
layout, customising node labels and size, modifying branch lengths and 
collapsing branches. The image can be saved in SVG format which can be further
edited in image publishing software such as Inkscape.

As an example, the default cgMLST tree (above) has been modified (below) as 
follows:

  * Nodes coloured by clonal complex
  * Labels removed
  * Branches collapsed where <=100 loci different
  * Node size set to 200%
  * Kurtosis (node size relative to number of isolates) set to 75%
  * Dynamic rendering allowed to run to fan out nodes
  
.. image:: /images/data_analysis/grapetree6.png

Full details can be found in
the `GrapeTree manual <https://bitbucket.org/enterobase/enterobase-web/wiki/GrapeTree>`_.

.. note::
   GrapeTree has been described in the following publication:
   
   Z Zhou, NF Alikhan, MJ Sergeant, N Luhmann, C Vaz, AP Francisco, JA Carrico,
   M Achtman (2018) GrapeTree: Visualization of core genomic relationships 
   among 100,000 bacterial pathogens. 
   `Genome Res 28:1395-1404 <https://www.ncbi.nlm.nih.gov/pubmed/30049790>`_.
