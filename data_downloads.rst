####################
Definition downloads
####################
The sequence definition database defines alleles, i.e. links an allele identifier to a sequence.  It also defines scheme, e.g. MLST, profiles.

.. _download_alleles:

***************************
Allele sequence definitions
***************************
Click the 'Allele sequences' link in the 'Downloads' section.  Depending on the database, you may see either a hierarchical scheme tree or a table of loci.  You can choose to display links either by scheme using the scheme tree, as an alphabetical list or a page of all schemes, by selecting the approrpiate link at the top of the page.

Scheme tree
===========
.. image:: /images/data_downloads/alleles.png

You can drill down through the tree by clicking branch nodes.  Clicking the labels of internal nodes will display tables of all schemes belonging to that scheme group.  Clicking the labels of terminal nodes will display that single scheme table.

.. image:: /images/data_downloads/alleles2.png

Click the green download link for the required locus

.. image:: /images/data_downloads/alleles3.png

Alleles will be downloaded in FASTA format, e.g. ::

  >fumC_1
  GAAGCCTTGGGCGGACGCGATGCCGCCGTTGCCGCTTCGGGCGCATTGAAAACGCTGGCG
  GCAAGCCTGAATAAAATCGCCAACGACATCCGCTGGCTGGCAAGCGGCCCGCGCTGCGGT
  TTGGGCGAAATCAAAATCCCCGAAAACGAGCCGGGTTCGTCCATCATGCCGGGCAAAGTC
  AACCCGACCCAATGCGAAGCGATGACCATGGTGTGCTGCCAAGTGTTCGGCAACGACGTT
  ACCATCGGTATGGCGGGCGCGTCGGGCAATTTCGAGCTGAACGTCTATATGCCCGTCATC
  GCCTACAACCTCTTGCAATCCATCCGCCTGTTGGGCGACGCGTGCAACAGCTTCAACGAA
  CACTGCGCCGTCGGCATTGAACCCGTACCGGAAAAAATCGACTATTTCCTGCACCATTCC
  CTGATGCTCGTTACCGCGTTAAACCGCAAAATCGGTTACGAAAAC
  >fumC_2
  GAAGCCTTGGGCGGACGCGATGCCGCCGTTGCCGCTTCGGGCGCATTGAAAACGCTGGCG
  GCAAGCCTGAATAAAATCGCCAACGACATCCGCTGGCTGGCAAGCGGCCCGCGCTGCGGT
  TTGGGCGAAATCAAAATCCCCGAAAACGAGCCGGGTTCGTCCATCATGCCGGGCAAAGTC
  AACCCGACCCAATGCGAAGCGATGACCATGGTGTGCTGCCAAGTGTTCGGCAACGACGTT
  ACCATCGGCATGGCGGGCGCGTCGGGCAATTTCGAGCTGAACGTCTATATGCCCGTTATC
  GCCTACAACCTCTTGCAATCCATCCGCCTCTTGGGCGACGCGTGCAACAGCTTCAACGAA
  CACTGCGCCATCGGCATCGAACCCGTACCGGAAAAAATCGACTATTTCCTGCACCATTCC
  CTGATGCTCGTTACCGCGTTAAACCGCAAAATCGGTTACGAAAAC
  >fumC_3
  GAAGCCTTGGGCGGACGCGATGCCGCCGTTGCCGCTTCGGGCGCATTGAAAACGCTGGCG
  GCAAGCCTGAATAAAATCGCCAACGACATCCGCTGGCTGGCAAGCGGCCCGCGCTGCGGT
  TTGGGCGAAATCAAAATCCCCGAAAACGAGCCGGGTTCGTCCATCATGCCGGGCAAAGTC
  AACCCGACCCAATGCGAAGCGATGACCATGGTGTGCTGCCAAGTGTTCGGCAACGACGTT
  ACCATCGGCATGGCGGGCGCGTCGGGCAATTTCGAGCTGAACGTCTATATGCCCGTTATC
  GCCTACAACCTCTTGCAATCCATCCGCCTGTTGGGCGACGCGTGCAACAGCTTCAACGAA
  CACTGCGCCGTCGGCATCGAACCCGTACCGGAAAAAATCGACTATTTCCTGCACCATTCC
  CTGATGCTGGTTACTGCGTTAAACCGTAAAATCGGCTACGAAAAC

Alphabetical list
=================
Loci can be displayed in an alphabetical list.  Loci will be grouped in to tables by initial letter.  If common names are set for loci, they will be listed by both primary and common names.

.. image:: /images/data_downloads/alleles4.png

Click the green download links for the required locus.

All loci by scheme
==================
Loci can also be displayed by scheme with all schemes displayed.

.. image:: /images/data_downloads/alleles5.png

Click the green download links for the required locus.

Download locus table
====================
The locus table can be downloaded in tab-delimited text or Excel formats by clicking the links following table display.

.. image:: /images/data_downloads/alleles6.png

**************************
Scheme profile definitions
**************************
Scheme profiles, e.g. those for MLST, can be downloaded by clicking the appropriate link on the contents page.

.. image:: /images/data_downloads/profiles.png

If multiple schemes are available, you will need to select the scheme in the dropdown box and click 'Download profiles'

.. image:: /images/data_downloads/profiles2.png

Profiles will be downloaded in tab-delimited format, e.g. ::

  ST	abcZ	adk	aroE	fumC	gdh	pdhC	pgm	clonal_complex
  1	1	3	1	1	1	1	3	ST-1 complex/subgroup I/II
  2	1	3	4	7	1	1	3	ST-1 complex/subgroup I/II
  3	1	3	1	1	1	23	13	ST-1 complex/subgroup I/II
  4	1	3	3	1	4	2	3	ST-4 complex/subgroup IV
  5	1	1	2	1	3	2	3	ST-5 complex/subgroup III
  6	1	1	2	1	3	2	11	ST-5 complex/subgroup III
  7	1	1	2	1	3	2	19	ST-5 complex/subgroup III
  8	2	3	7	2	8	5	2	ST-8 complex/Cluster A4
  9	2	3	8	10	8	5	2	ST-8 complex/Cluster A4
  10	2	3	4	2	8	15	2	ST-8 complex/Cluster A4
  11	2	3	4	3	8	4	6	ST-11 complex/ET-37 complex
  12	4	3	2	16	8	11	20	
  13	4	10	15	7	8	11	1	ST-269 complex
  14	4	1	15	7	8	11	1	ST-269 complex


