########
Appendix
########

.. _query_operators:

***************
Query operators
***************
Various query forms have operators for use with field values.  Available operators are:

* =

  * Case insensitive exact match.

* contains

  * Case insensitive match to a partial string, e.g. searching for clonal complex 'contains' st-11 would return all STs belonging to the ST-11 complex.

* starts with

  * Match to values that start with the search term (case insensitive).

* ends with

  * Match to values that end with the search term (case sensitive).

* >

  * Greater than the search term.

* <

  * Less than the search term.

* NOT

  * Match to values that do not equal the search term (case insensitive).

* NOT contain

  * Match to values that do not contain the search term (case insensitive).

.. _sequence_tag_flags:

******************
Sequence tag flags
******************
Sequences tagged in the sequence bin can have features indicated by specific flags.  The presence of these flags can be queried.  These are a superset of :ref:`flags available for allele sequences <allele_sequence_flags>`. Available flags are:

* ambiguous read

  * Genome sequence contains ambiguous nucleotides in coding sequence.

* apparent misassembly

  * Sequence has a region of very high identity to existing allele in one region but looks completely different in another.

* atypical

  * Catch-all term for a sequence that is unusual compared to other alleles of locus.

* contains IS element

  * Coding sequence is interrupted by insertion sequence.

* downstream fusion

  * No stop codon present resulting in translation continuing.

* frameshift

  * Frameshift in sequence relative to other alleles, not resulting in internal stop codon.

* internal stop codon

  * Frameshift in sequence relative to other alleles, resulting in internal stop codon.

* no start codon

  * No apparent start codon in immediate vicinity of usual start.

* phase variable: off

  * Coding sequence has a homopolymeric run with a frameshift resulting in a stop codon preventing complete translation.

* truncated

  * Coding sequence is unusually short resulting in a truncated protein (not the same as running off the end of a contig).

* upstream fusion

  * No apparent start codon in immediate vicinity of usual start, likely due to a gene fusion (sequence is transcribed together with upstream coding sequence).

.. _allele_sequence_flags:

*********************
Allele sequence flags
*********************
Sequences can be flagged with specific attributes - these are searchable when doing a sequence attribute query.  These are a subset of :ref:`flags available for tagged sequences <sequence_tag_flags>`. These are mainly for use with whole genome MLST type data.  Multiple flags can be selected by Ctrl-clicking the list.  Available flags are:

* atypical

  * Catch-all term for a sequence that is unusual compared to other alleles of locus.

* contains IS element

  * Coding sequence is interrupted by insertion sequence.

* downstream fusion

  * No stop codon present resulting in translation continuing.

* frameshift

  * Frameshift in sequence relative to other alleles, not resulting in internal stop codon.

* internal stop codon

  * Frameshift in sequence relative to other alleles, resulting in internal stop codon.

* no start codon

  * No apparent start codon in immediate vicinity of usual start.

* phase variable: off

  * Coding sequence has a homopolymeric run with a frameshift resulting in a stop codon preventing complete translation.

* truncated

  * Coding sequence is unusually short resulting in a truncated protein (not the same as running off the end of a contig).

* upstream fusion

  * No apparent start codon in immediate vicinity of usual start, likely due to a gene fusion (sequence is transcribed together with upstream coding sequence).
