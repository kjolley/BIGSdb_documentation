##################
Concepts and terms
##################

******
BIGSdb
******
BIGSdb is the software platform - not a specific database.  There are many instances of BIGSdb databases, so referring to 'the BIGSdb' is meaningless.

.. index::
   single: loci

.. _loci:

****
Loci
****
Loci are regions of the genome that are identified by similarity to a known sequence.  They can be defined by DNA or peptide sequence.  They are often complete coding sequences (genes), but may represent gene fragments (such as used in MLST), antigenic peptide loops, or indeed any sequence feature.

In versions of BIGSdb prior to 1.8.0, an isolate record could only have one live :ref:`allele <alleles>` designation for a locus (inactive/pending designations could be stored within the database but were unavailable for querying or analysis purposes).  Since biology is rarely so clean, and some genomes may contain more than one copy of a gene, later versions of the software allow multiple allele designations for a locus, all of which can be queried and analysed. 

Paralogous loci can be difficult to differentiate by sequence similarity alone.  Because of this, loci can be further defined by context, where in silico PCR or hybridization reactions can be performed to :ref:`filter the genome <genome_filtering>` to specific regions based on sequence external to the locus.

.. index::
   single: alleles

.. _alleles:

*******
Alleles
*******
Alleles are instances of loci.  Every unique sequence, either DNA or peptide depending on the locus, is defined as a new allele and these are defined in a sequence definition database, where they are given an allele identifier.  These identifiers are usually integers, but can be text strings.  Allele identifiers in text format can be constrained by length and formatting.

When a specific allele of a locus is identified within the sequence data of an isolate record, the allele designation, i.e. identifier, is associated with the isolate record.  This efficiently stores the sequence variation found within an isolate.  Two isolates with the same allele designation for a locus have identical sequences at that locus.  Once the sequence variation within a genome has been reduced to a series of allele designations, genomes can be efficiently compared by identifying which loci vary between them.

It is important to note that allele identifiers are usually arbitrary and are allocated sequentially in the order of discovery.  Alleles with adjacent identifiers may vary by a single nucleotide or by many.

.. index::
   single: schemes
   single: MLST

.. _schemes:

*******
Schemes
*******
Schemes are collections of loci that may be associated with additional field values.  At their simplest they just group loci together.  Example uses of simple schemes include:

* Antibiotic resistance genes
* Genes involved in specific biochemical pathways
* Antigens
* Vaccine components
* Whole genome MLST (wgMLST)

When schemes are associated with additional fields, one of these fields must be the primary key, i.e. its value uniquely defines a particular combination of alleles at its member loci.  The pre-eminent example of this is MLST - where a sequence type (ST) is the primary key that uniquely defines combinations of alleles that make up the MLST profiles.  Additional fields can also then be included.  The values for these need not be unique.  In the MLST example, a field for clonal complex can be included, and the same value for this can be set for multiple STs.

.. index::
   single: profiles

.. _profiles:

********
Profiles
********
Profiles are instances of :ref:`schemes <schemes>`.  A profile consists of a set of :ref:`allele identifiers <alleles>` for the :ref:`loci <loci>` that comprise the scheme.  If the scheme has a primary key field, e.g. sequence type (ST) in MLST schemes, then the unique combination of alleles in a complete profile can be defined by the value of this field.

.. index::
   single: sequence tags

.. _sequence_tags:

*************
Sequence tags
*************
Sequence tags record locus position within an isolate record's sequence bin.  The process of creating these tags, is known as :ref:`tag-scanning <tag_scanning>`.  A sequence tag consists of:

* sequence bin id - this identifies a particular contig
* locus name
* start position
* end position
* flag to indicate if sequence is reversed
* flag to indicate if sequence is complete and does not continue off the end of the contig

.. index::
   single: sets

.. _sets:

****
Sets
****
Sets provide a means to take a large database with multiple loci and/or schemes and present a subset of these as though it was a complete database. The loci and schemes chosen to belong to a set can be renamed when used with this set. The rationale for this is that in a database with disparate isolates and a large number of loci, the naming of these loci may have to be long to specify a species name. For example, you may have a database that contains multiple MLST schemes for different species, but since these schemes may use different fragments of the same genes they may have to be named something like 'Streptococcus_pneumoniae_MLST_aroE' to uniquely specify them. If we define a set for 'Streptococcus pneumoniae' we can then choose to only include S. pneumoniae loci and therefore shorten their names, e.g. to 'aroE'.

Additional metadata fields can also be associated with each set so it is possible to have a database containing genomes from multiple species and a generic set of metadata, then have additional specific metadata fields for particular species or genera. These additional fields only become visible and searchable when the specific set that they belong to has been selected.
