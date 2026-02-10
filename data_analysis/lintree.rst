.. index::
   pair: LINtree; LIN codes

*******
LINtree
*******
LINtree is a tool to infer prefix trees with branch lengths from sets of Life 
Identification Number (LIN) codes. Such LIN-based prefix trees are very useful
to reflect the phylogenetic relationships among genomes typed by cgMLST where 
LIN codes have been assigned. Once the tree has been generated, the resultant
Newick file is uploaded to iTOL for visualisation (if enabled) along with 
selected metadata that can be used to annotate it.

.. image:: /images/data_analysis/lintree1.png

Only isolates with an assigned LIN code can be included in the tree.

Lintree can be accessed by selecting the 'Analysis' section on the main 
contents page.

.. image:: /images/data_analysis/analysis.png

Jump to the 'Third party' category, follow the link to LINtree, then click 
'Launch LINtree'.

LINtree can be accessed from the contents page by clicking the 'LINtree' link.

.. image:: /images/data_analysis/lintree2.png

Alternatively, it can be accessed following a query by clicking the 'iTOL'
button at the bottom of the results table.  Isolates returned from the query 
will be automatically selected within the iTOL interface.

.. image:: /images/data_analysis/lintree3.png

Select the isolates to include. If there is more than one scheme in the 
database that has LIN codes assigned, then select the required scheme.

Additional fields can be selected to be included as metadata for use in 
colouring nodes - select any fields you wish to include in the 'iTOL datasets'
list. Multiple selections can be made. You can also choose how nodes are 
labeled by metadata - either by colouring the labels or using coloured strips.
LIN codes are selected by default.

Click 'Submit' to start the analysis.

.. image:: /images/data_analysis/lintree4.png

The job will be sent to the job queue. When it has finished, the generated
tree and associated metadata will be uploaded to the Interactive Tree of Life
website (https://itol.embl.de/). Click the button marked 'Launch iTOL'.

.. image:: /images/data_analysis/lintree5.png

Your browser will open the iTOL website with your tree.

.. note::
   LINtree has been developed by Alexis Criscuolo. The code can be found 
   at https://gitlab.pasteur.fr/GIPhy/LINtree.

   Genome Informatics & Phylogenetics (GIPhy), Centre de Ressources Biologiques
   de l'Institut Pasteur (CRBIP), Institut Pasteur, Paris, France
   
  