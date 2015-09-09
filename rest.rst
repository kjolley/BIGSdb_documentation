###############################################
RESTful Application Programming Interface (API)
###############################################
The REST API allows third-party applications to retrive data stored within
BIGSdb databases.  To use the REST API, your application will make a HTTP
request and parse the response.  The response format is JSON (except for routes
that request a FASTA file).  

***************************
Passing optional parameters
***************************
Optional parameters can be passed as arguments to the query URL by adding a '?'
followed by the first argument and its value (separated by a '=').  Additional
parameters are separated by a '&', e.g.

http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates?page=2&page_size=100

*********
Resources
*********
* :ref:`/ or /db<db>`
* :ref:`/db/{database}<db>`
* :ref:`/db/{database}/loci<db_loci>`
* :ref:`/db/{database}/loci/{locus}<db_loci_locus>`
* :ref:`/db/{database}/loci/{locus}/alleles<db_loci_locus_alleles>`
* :ref:`/db/{database}/loci/{locus}/alleles_fasta<db_loci_locus_alleles_fasta>`
* :ref:`/db/{database}/loci/{locus}/alleles/{allele_id}<db_loci_locus_alleles_allele_id>`
* :ref:`/db/{database}/schemes<db_schemes>`
* :ref:`/db/{database}/schemes/{scheme_id}<db_schemes_scheme_id>`
* :ref:`/db/{database}/schemes/{scheme_id}/fields/{field}<db_schemes_scheme_id_fields_field>`
* :ref:`/db/{database}/schemes/{scheme_id}/profiles<db_schemes_scheme_id_profiles>`
* :ref:`/db/{database}/schemes/{scheme_id}/profiles_csv<db_schemes_scheme_id_profiles_csv>`
* :ref:`/db/{database}/schemes/{scheme_id}/profiles/{profile_id}<db_schemes_scheme_id_profiles_profile_id>`
* :ref:`/db/{database}/isolates<db_isolates>`
* :ref:`/db/{database}/isolates/{isolate_id}<db_isolates_isolate_id>`
* :ref:`/db/{database}/isolates/{isolate_id}/allele_designations<db_isolates_isolate_id_allele_designations>`
* :ref:`/db/{database}/isolates/{isolate_id}/allele_designations/{locus}<db_isolates_isolate_id_allele_designations_locus>`
* :ref:`/db/{database}/isolates/{isolate_id}/allele_ids<db_isolates_isolate_id_allele_ids>`
* :ref:`/db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_designations<db_isolates_isolate_id_schemes_scheme_id_allele_designations>`
* :ref:`/db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_ids<db_isolates_isolate_id_schemes_scheme_id_allele_ids>`
* :ref:`/db/{database}/isolates/{isolate_id}/contigs<db_isolates_isolate_id_contigs>`
* :ref:`/db/{database}/isolates/{isolate_id}/contigs_fasta<db_isolates_isolate_id_contigs_fasta>`
* :ref:`/db/{database}/contigs/{contig_id}<db_contigs_contig_id>`
* :ref:`/db/{database}/fields<db_fields>`
* :ref:`/db/{database}/users/{user_id}<db_users_user_id>`
* :ref:`/db/{database}/projects<db_projects>`
* :ref:`/db/{database}/projects/{project_id}<db_projects_project_id>`
* :ref:`/db/{database}/projects/{project_id}/isolates<db_projects_project_id_isolates>`

.. _db_no_arg:

.. index::
   single: API resources; /db
   single: API resources; /
   
/ or /db
========
Lists database resources available using the API.

**Supported methods:** GET, POST

**Required query parameters:** None

**Optional query parameters:** None

**Example request URI:** http://rest.pubmlst.org/

**Response:** List of resource groupings (ordered by name).  Groups may consist
of paired databases for sequence definitions and isolate data, or any set of
related resources.  Each group contains:

* name [string] - short name (usually a single word)
* description [string] - fuller description
* databases [array] - list of database objects, each consists of three 
  key/value pairs:

   * name [string] - name of database config
   * description [string] - short description of resource
   * href [string] - URI to access resource
   
.. _db:

.. index::
   single: API resources; /db/{database}

/db/{database}
==============
Lists resources available for specified database configuration.  These will 
vary depending on whether the resource is an isolate or a sequence definition
database.

**Supported methods:** GET, POST

**Required query parameter:** {database} - Database configuration name [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates

**Response:** Object containing a subset of the following key/value pairs:

* :ref:`fields<db_fields>` [string] - URI to isolate provenance field information
* :ref:`isolates<db_isolates>` [string] - URI to isolate records
* :ref:`schemes<db_schemes>` [string] - URI to list of schemes
* :ref:`loci<db_loci>` [string] - URI to list of loci
* :ref:`projects<db_projects>` [string] - URI to list of projects
* records [integer] - count of available records

.. _db_loci:

.. index::
   single: API resources; /db/{database}/loci

/db/{database}/loci
===================
Lists loci defined within specified database configuration.

**Supported methods:** GET, POST

**Required query parameter:** {database} - Database configuration name [string]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/loci

**Response:** Object containing:

* loci [array] - List of :ref:`URIs to defined locus records<db_loci_locus>`.  
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_loci_locus:

.. index::
   single: API resources; /db/{database}/loci/{locus}

/db/{database}/loci/{locus}
===========================
Provides information about a locus, including links to allele sequences (in 
seqdef databases).

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {locus} - Locus name [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/loci/abcZ

**Response:** Object containing a subset of the following key/value pairs:

* id [string] - locus name
* data_type [string] - 'DNA' or 'peptide'
* allele_id_format [string] - 'integer' or 'text'
* allele_id_regex [string] - regular expression constraining allele ids
* common_name [string]
* aliases [array] - list of alternative names of the locus
* length_varies [boolean]
* length [integer] - length if alleles are of a fixed length
* coding_sequence [boolean]
* orf [integer] - 1-6
* schemes [array] - list of scheme objects, each consisting of:
   * scheme [string] - URI to scheme information
   * description [string]
* min_length [integer] (seqdef databases) - minimum length for variable length
  loci
* max_length [integer] (seqdef databases) - maximum length for variable length
  loci
* alleles [string] (seqdef databases) - :ref:`URI to list of allele records
  <db_loci_locus_alleles>`
* alleles_fasta [string] (seqdef databases) - :ref:`URI to FASTA file of all
  alleles of locus<db_loci_locus_alleles_fasta>`
* curators [array] (seqdef databases) - list of 
  :ref:`URIs to user records<db_users_user_id>` of curators of the locus
* publications [array] (seqdef databases) - list of PubMed id numbers of papers
  describing the locus
* full_name [string] (seqdef databases)
* product [string] (seqdef databases)
* description [string] (seqdef databases)
* extended_attributes [array] (seqdef databases) - list of extended attribute
  objects.  Each consists of a subset of the following fields:
  
    * field [string] - field name
    * value_format [string] - 'integer', 'text', or 'boolean' 
    * value_regex [string] - regular expression constraining value
    * description [string] - description of field
    * length [integer] - maximum length of field
    * required [boolean]
    * allowed_values [array] - list of allowed values
    
* genome_position [integer] (isolate databases)

.. _db_loci_locus_alleles:

.. index::
   single: API resources; /db/{database}/loci/{locus}/alleles

/db/{database}/loci/{locus}/alleles
===================================
Lists alleles defined for specific locus.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {locus} - Locus name [string]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/loci/abcZ/alleles

**Response:** Object containing:

* alleles [array] - List of :ref:`URIs to defined allele records
  <db_loci_locus_alleles_allele_id>`.  
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_loci_locus_alleles_fasta:

.. index::
   single: API resources; /db/{database}/loci/{locus}/alleles_fasta

/db/{database}/loci/{locus}/alleles_fasta
=========================================
Provides all alleles defined for a locus in FASTA format.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {locus} - Locus name [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/loci/abcZ/alleles_fasta

**Response:** FASTA format file of alleles sequences 
   
.. _db_loci_locus_alleles_allele_id:

.. index::
   single: API resources; /db/{database}/loci/{locus}/alleles/{allele_id} 
   
/db/{database}/loci/{locus}/alleles/{allele_id}
===============================================
Provides information about an allele including its sequence.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {locus} - Locus name [string]
* {allele_id} - Allele identifier [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/loci/abcZ/alleles/5

**Response:** Object containing the following key/value pairs:   

* locus [string] - :ref:`URI to locus description<db_loci_locus>`
* allele_id [string] - allele identifier
* sequence [string] - sequence
* status [string] - either 'Sanger trace checked', 'WGS: manual extract', 
  'WGS: automated extract', or 'unchecked'
* sender [string] - :ref:`URI to user details<db_users_user_id>` of sender
* curator [string] - :ref:`URI to user details<db_users_user_id>` of curator
* date_entered [string] - record creation date (ISO 8601 format)
* datestamp [string] - last updated date (ISO 8601 format)

.. _db_schemes:

.. index::
   single: API resources; /db/{database}/schemes 

/db/{database}/schemes
======================
Lists schemes defined within specified database configuration.

**Supported methods:** GET, POST

**Required query parameter:** {database} - Database configuration name [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes

**Response:** List of scheme objects, each containing:

* scheme [string] - URI to scheme information
* description [string] 

.. _db_schemes_scheme_id:

.. index::
   single: API resources; /db/{database}/schemes/{scheme_id}

/db/{database}/schemes/{scheme_id}
==================================
Provides information about a scheme, including links to allelic profiles (in 
seqdef databases, if appropriate).

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {scheme_id} - Scheme id number [integer]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes/1

**Response:** Object containing a subset of the following key/value pairs:

* id [integer]
* description [string]
* locus_count [integer] - number of loci belonging to scheme
* loci [array] - list of :ref:`URIs to locus descriptions<db_loci_locus>`
* has_primary_key_field [boolean]
* fields [array] - list of :ref:`URIs to scheme field descriptions
  <db_schemes_scheme_id_fields_field>`
* primary_key_field [string] - :ref:`URI to primary key field description
  <db_schemes_scheme_id_fields_field>`
* profile_count [integer] - number of defined profiles (only for schemes with
  primary keys defined - only seqdef databases)
* profiles [array] - URI to list of profile definitions (only seqdef databases)
* profiles_csv [string] - URI to tab-delimited file of all scheme profiles
* curators [array] (seqdef databases) - list of 
  :ref:`URIs to user records<db_users_user_id>` of curators of the scheme

.. _db_schemes_scheme_id_fields_field:

.. index::
   single: API resources; /db/{database}/schemes/{scheme_id}/fields/{field}

/db/{database}/schemes/{scheme_id}/fields/{field}
=================================================
Provides information about scheme fields.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {scheme_id} - Scheme id number [integer]
* {field} - Field name [string]
 
**Optional parameters:** None
 
**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes/1/fields/ST
 
**Response:** Object containing the following key/value pairs:
 
* field [string] - field name
* type [string] - data type of field (integer or text)
* primary_key [boolean] - true if field is the scheme primary key

.. _db_schemes_scheme_id_profiles:

.. index::
   single: API resources; /db/{database}/schemes/{scheme_id}/profiles

/db/{database}/schemes/{scheme_id}/profiles
===========================================
Lists allelic profiles defined for a specific scheme.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {scheme_id} - Scheme id [integer]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes/1/profiles

**Response:** Object containing:

* profiles [array] - List of URIs to defined profile records. 
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_schemes_scheme_id_profiles_csv:

.. index::
   single: API resources; /db/{database}/schemes/{scheme_id}/profiles_csv
   
/db/{database}/schemes/{scheme_id}/profiles_csv
===============================================
Provides all profiles defined for a scheme in CSV (tab-delimited) format.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {scheme_id} - Scheme id [integer]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes/1/profiles_csv

**Response:**  Tab-delimited text file of allelic profiles

.. _db_schemes_scheme_id_profiles_profile_id:

.. index::
   single: API resources; /db/{database}/schemes/{scheme_id}/profiles/{profile_id}

/db/{database}/schemes/{scheme_id}/profiles/{profile_id}
========================================================
Provides information about a specific allelic profile defined for a scheme.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {scheme_id} - Scheme id [integer]
* {profile_id} - Profile id [string/integer] 

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/schemes/1/profiles/11

**Response:** Object containing the following key/value pairs:   

* *primary_key_term* [string/integer] - The field name is the primary key, 
  e.g. ST.  The value is the primary key value (primary_id used as an 
  argument).
* alleles [object] - :ref:`list of URIs to allele descriptions
  <db_loci_locus_alleles_allele_id>`
* *other_scheme_fields* [string/integer] - Each scheme field will have its own
  value if defined.  The field name is the name of the field.
* sender [string] - :ref:`URI to user details<db_users_user_id>` of sender
* curator [string] - :ref:`URI to user details<db_users_user_id>` of curator
* date_entered [string] - record creation date (ISO 8601 format)
* datestamp [string] - last updated date (ISO 8601 format)

.. _db_isolates:

.. index::
   single: API resources; /db/{database}/isolates 

/db/{database}/isolates
=======================
Provides list of isolate records.

**Supported methods:** GET, POST

**Required query parameter:** {database} - Database configuration name [string]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates

**Response:** Object containing:

* isolates [array] - List of URIs to isolate records.  
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)

.. _db_isolates_isolate_id:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}
   
/db/{database}/isolates/{isolate_id}
====================================
Provides information about an isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1

**Response:** Object containing some or all of the following key/value pairs:

* provenance [object] - set of key/value pairs.  Keys are defined by calling
  the :ref:`/fields route<db_fields>`.  The fields will vary by database but 
  will always contain the following:
  
   * id [integer]
   * sender [string] - :ref:`URI to user details<db_users_user_id>` of sender
   * curator [string] - :ref:`URI to user details<db_users_user_id>` of curator
   * date_entered [string] - record creation date (ISO 8601 format)
   * datestamp [string] - last updated date (ISO 8601 format) 
   
* publications [array] (seqdef databases) - list of PubMed id numbers of papers
  that refer to the isolate
* sequence_bin [object] - consists of the following key/value pairs:

   * contigs_fasta [string] - :ref:`URI to FASTA file containing all the contigs
     belonging to this isolate<db_isolates_isolate_id_contigs_fasta>`
   * contigs [string] - :ref:`URI to list of contig records
     <db_isolates_isolate_id_contigs>`
   * contig_count [integer] - number of contigs
   * total_length [integer] - total length of contigs
   
* allele_designations [object] - consists of the following key/value pairs:

   * allele_ids - :ref:`URI to list of all allele_id values
     <db_isolates_isolate_id_allele_ids>` defined for the isolate
   * designation_count - number of allele designations defined for the isolate
   * full_designations - :ref:`URI to list of full allele designation records
     <db_isolates_isolate_id_allele_designations>`
   
* schemes [array] - list of scheme objects, each containing the following:

   * description [string] - description of scheme
   * loci_designated_count [integer] - number of loci within scheme that have
     an allele designated for this isolate.
   * allele_ids [string] - :ref:`URI to list of all allele_id values defined for this
     scheme<db_isolates_isolate_id_schemes_scheme_id_allele_ids>` for this 
     isolate
   * full_designations [string] - :ref:`URI to list of full allele designation 
     records<db_isolates_isolate_id_schemes_scheme_id_allele_designations>` for
     this isolate
   * fields [object] - consisting of key/value pairs where the key is the name
     of each scheme field
     
* projects [array] - list of project objects, each containing the following:

   * id [string] - :ref:`URI to project information<db_projects_project_id>`
   * description [string] - description of project
   
* new_version [string] - URI to newer version of record
* old_version [string] - URI to older version of record
     
.. _db_isolates_isolate_id_allele_designations:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/allele_designations
     
/db/{database}/isolates/{isolate_id}/allele_designations
========================================================
Provides a list of full allele designation records for the specified isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/allele_designations

**Response:** Object containing:

* allele_designations [array] - List of :ref:`URIs to allele designation records
  <db_isolates_isolate_id_allele_designations_locus>`
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_isolates_isolate_id_allele_designations_locus:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/allele_designations/{locus}  
   
/db/{database}/isolates/{isolate_id}/allele_designations/{locus}
================================================================
Provides a full allele designation record.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]
* {locus} - Locus mame [string]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/allele_designations/BACT000065

**Response:** List of allele_designation objects (there may be multiple 
designations for the same locus), each containing:

* locus [string] - :ref:`URI to locus description<db_loci_locus>`
* allele_id [string]
* method [string] - either 'manual' or 'automatic'
* status [string] - either 'confirmed' or 'provisional'
* comments [string]
* sender [string] - :ref:`URI to user details<db_users_user_id>` of sender
* curator [string] - :ref:`URI to user details<db_users_user_id>` of curator
* datestamp [string] - last updated date (ISO 8601 format)

.. _db_isolates_isolate_id_allele_ids:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/allele_ids

/db/{database}/isolates/{isolate_id}/allele_ids
===============================================
Returns array of allele identifiers for isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/allele_ids

**Response:** Object containing:

* allele_ids [array] - List of allele id objects, each consisting of a 
  key/value pair where the key is the locus name.  
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_isolates_isolate_id_schemes_scheme_id_allele_designations:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_designations
     
  
/db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_designations
============================================================================
Provides a list of full allele designation records for loci belonging to 
the specified scheme and isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]
* {scheme_id} - Scheme identifier [integer]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/schemes/1/allele_designations

**Response:** Array containing :ref:`allele designation objects
<db_isolates_isolate_id_allele_designations_locus>` for each locus in the 
specified scheme that has been designated.

.. _db_isolates_isolate_id_schemes_scheme_id_allele_ids:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_ids

/db/{database}/isolates/{isolate_id}/schemes/{scheme_id}/allele_ids
===================================================================
Provides a list of allele identifiers for loci belonging to the specified
scheme and isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]
* {scheme_id} - Scheme identifier [integer]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/schemes/1/allele_ids

**Response:** Array containing allele id objects for each locus in the 
specified scheme that has been designated.  Each allele_id object contains a 
key which is the name of the locus with a value that may be either a string, 
integer or array of strings or integers (required where there are multiple
designations for a locus).  The data type depends on the allele_id_format set
for the specific locus.

.. _db_isolates_isolate_id_contigs:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/contigs

/db/{database}/isolates/{isolate_id}/contigs
============================================
Returns a list of contig records for the specified isolate.

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {isolate_id} - Isolate identifier [integer]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/contigs

**Response:** Object containing:

* contigs [array] - List of :ref:`URIs to contig records
  <db_contigs_contig_id>`
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)
   
.. _db_isolates_isolate_id_contigs_fasta:

.. index::
   single: API resources; /db/{database}/isolates/{isolate_id}/contigs_fasta
   
/db/{database}/isolates/{isolate_id}/contigs_fasta
==================================================
Provides all contigs associated with an isolate record in FASTA format.

**Supported methods:** GET, POST

**Required query parameters:** 
 * {database} - Database configuration name [string]
 * {isolate_id} - Isolate identifier [integer]

**Optional parameter:** 
 * header [string] - either 'original_designation' or 'id' (default is 
   'id'). This selects whether the FASTA header lines contain
   the originally uploaded FASTA headers or the sequence bin id numbers.

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/isolates/1/contigs_fasta?header=original_designation

**Response:** FASTA format file of isolate contig sequences

.. _db_contigs_contig_id:

.. index::
   single: API resources; /db/{database}/contigs/{contig_id}

/db/{database}/contigs/{contig_id}
=======================================================
Provides a record of a specified contig.

**Supported methods:** GET, POST

**Required query parameters:** 
 * {database} - Database configuration name [string]
 * {contig_id} - Contig identifier [integer]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/contigs/180062

**Response:** Contig object consisting of the following key/value pairs:

* id [integer] - contig identifier
* isolate_id [integer] - isolate identifier
* sequence [string] - contig sequence
* length [integer] - length of contig sequence
* method [string] - sequencing method
* sender [string] - :ref:`URI to user details<db_users_user_id>` of sender
* curator [string] - :ref:`URI to user details<db_users_user_id>` of curator
* date_entered [string] - record creation date (ISO 8601 format)
* datestamp [string] - last updated date (ISO 8601 format) 

.. _db_fields:

.. index::
   single: API resources; /db/{database}/fields 

/db/{database}/fields
=====================
Provides a list of isolate provenance field descriptions.

**Supported methods:** GET, POST

**Required query parameters:** 
 * {database} - Database configuration name [string]

**Optional parameters:** None

**Example request URI:** 
http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/fields

**Response:** Array of field objects, each consisting of some or all of the
following key/value pairs:

* name [string] - name of field
* type [string] - data type (int, text, date, float)
* length [integer] - maximum length of field
* required [boolean] - true if field value is required
* min [integer] - minimum value for integer values
* max [integer] - maximum value for integer values
* regex [string] - regular expression that constrains the allowed value of the
  field
* comments [string]
* allowed values [array] - list of allowed values for the field [string]

.. _db_users_user_id:

.. index::
   single: API resources; /db/{database}/users/{user_id} 

/db/{database}/users/{user_id}
==============================
Provides information about data senders and curators.

**Supported methods:** GET, POST

**Required query parameters:** 
 * {database} - Database configuration name [string]
 * {user_id} - User id number [integer]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_seqdef/users/2

**Response:** Object containing the following key/value pairs:

* id [integer] - user id number
* first_name [string]
* surname [string]
* affiliation [string] - institutional affiliation
* email [string] - E-mail address

.. _db_projects:

.. index::
   single: API resources; /db/{database}/projects

/db/{database}/projects
=======================
Lists projects defined within specified isolate database configuration.

**Supported methods:** GET, POST

**Required query parameter:** {database} - Database configuration name [string]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/projects

**Response:** List of project objects, each containing:

* project [string] - :ref:`URI to project information<db_projects_project_id>`
* description [string] 
* isolate_count [integer] - number of isolates in project

.. _db_projects_project_id:

.. index::
   single: API resources; /db/{database}/projects/{project_id}

/db/{database}/projects/{project_id}
====================================
Provides information about a project, including links to member isolates (in 
isolate databases).

**Supported methods:** GET, POST

**Required query parameters:** 

* {database} - Database configuration name [string]
* {project_id} - Project id number [integer]

**Optional parameters:** None

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/projects/3

**Response:** Object containing a subset of the following key/value pairs:

* id [integer]
* description [string]
* isolate_count [integer] - number of isolates belonging to the project
* isolates [string] - :ref:`URI to list of URIs of member isolate records<db_projects_project_id_isolates>`. 

.. _db_projects_project_id_isolates:

.. index::
   single: API resources; /db/{database}/projects/{project_id}/isolates

/db/{database}/projects/{project_id}/isolates
=============================================
Provides list of records of isolates that are members of the specified project.

**Supported methods:** GET, POST

**Required query parameter:** 

* {database} - Database configuration name [string]
* {project_id} - Project id number [integer]

**Optional parameters:** 

* page [integer]
* page_size [integer]
* return_all [integer] - Set to non-zero value to disable paging. 

**Example request URI:** http://rest.pubmlst.org/db/pubmlst_neisseria_isolates/projects/3/isolates

**Response:** Object containing:

* isolates [array] - List of URIs to isolate records.  
  Pages are 100 records by default.  Page size can be modified using the 
  page_size parameter.
* paging [object] - Some or all of the following:
   * previous - URI to previous page of results
   * next - URI to next page of results
   * first - URI to first page of results
   * last - URI to last page of results
   * return_all - URI to page containing all results (paging disabled)

**************
Authentication
**************
Protected resources, i.e. those requiring a user to log in, can be accessed via
the API using OAuth (1.0A) authentication (see 
`IETF RFC5849 <http://tools.ietf.org/html/rfc5849>`_ for details).  Third-party
client software has to be registered with the BIGSdb site before they can 
access authenticated resources. The overall three-legged flow works as follows:

#. :ref:`Developer signs up <get_consumer_key>` and gets a consumer key and 
   consumer secret specific to their application.
#. Application :ref:`gets a request token <get_request_token>` and directs user
   to authorization page on BIGSdb.
#. BIGSdb :ref:`asks user for authorization <get_user_authorization>` for 
   application to access specific resource using their credentials.  A verifier
   code is provided.
#. The application exchanges the request token and OAuth verifier code for an 
   :ref:`access token and secret <get_access_token>` (these do not expire but 
   may be revoked by the user or site admin). 
#. Application uses access token/secret to 
   :ref:`request session token <get_session_token>` (this is valid for 12 
   hours).
#. All calls to 
   :ref:`access protected resources <accessing_protected_resources>` are signed
   using the session token/secret and consumer key/secret.
   
It is recommended that application developers use an OAuth library to generate
and sign requests.

.. _get_consumer_key:

.. index::
   single: API authentication; consumer key

Developer sign up to get a consumer key
=======================================
Application developers should apply to the site administrator of the site 
running BIGSdb.  The administrator can 
:ref:`generate a key and secret<create_client_credentials>` using a script - 
both of these will need to be used by the application to sign
requests.

The client id is usually a 24 character alphanumeric string.  The secret is
usually a 42 character alphanumeric (including punctuation) string, e.g.

 * **client_id:** efKXmqp2D0EBlMBkZaGC2lPf
 * **client_secret:** F$M)_+fQ2AFFB2YBDfF9fpHF^qSWJdmmN%L4Fxf5Gur3

.. _get_request_token:

.. index::
   single: API authentication; request token

Getting a request token
=======================

* **Relative URL:** /db/{database}/oauth/get_request_token
* **Supported methods:** GET, POST
 
The application uses the consumer key to obtain a request token.  The request
token is a temporary token used to initiate user authorization for the 
application and will expire in 60 minutes.  The request needs to contain the
following parameters and to be signed using the consumer secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970) - this must be 
   within 600 seconds of the current time.
 * oauth_callback ('oob' for desktop applications)
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the request token.  It is usually a 32 character alphanumeric
      string.
    * e.g. fKFm0WNhCfbEX8zQm6qhDA8K23FOWDGE
 * oauth_token_secret
    * This is the secret associated with the request token.  It is usually a 
      32 character alphanumeric string.
    * e.g. aZ0fncP7i5w5jlebdK5zyQ4vrRRVcdnv
 * oauth_callback_confirmed
    * This parameter is always set to true.

.. _get_user_authorization:

.. index::
   single: API authentication; user authorization
   
Getting user authorization
==========================
Once a request token has been obtained, this can be used by the end user to
grant permission to access a specific resource to the application.  The 
application should direct the user to the client authorization page 
(authorizeClient) specific to a database within BIGSdb, e.g. 
http://pubmlst.org/cgi-bin/bigsdb/bigsdb.pl?db=pubmlst_neisseria_seqdef&page=authorizeClient&oauth_token=fKFm0WNhCfbEX8zQm6qhDA8K23FOWDGE

The user will be asked if they wish to grant access to the application on their
behalf:

.. image:: /images/rest/authorize_client.png

If they authorize the access, they will be presented with a verifier code.  
This should be entered in to the client application which will use this 
together with the request token to request an access token.

.. image:: /images/rest/authorize_client2.png

The verifier code is valid for 60 minutes.

.. _get_access_token:

.. index::
   single: API authentication; access token

Getting an access token
=======================
* **Relative URL:** /db/{database}/oauth/get_access_token
* **Supported methods:** GET, POST
 
The application uses the request token, verifier code and its consumer key to 
obtain an access token.  The access token does not expire but can be revoked
by both the end user or the site admininstrator.  The request needs to contain
the following parameters and to be signed using the consumer secret and request
token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (request token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970) - this must be 
   within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the access token.  It is usually a 32 character alphanumeric
      string.
    * e.g. SDrC74ZVl5SYSqY8lWZqrRxnyDnNGVFO
 * oauth_token_secret
    * This is the secret associated with the access token.  It is usually a 
      32 character alphanumeric string.
    * e.g. tYI2SPzgiO02IRVzW4JR1ez6Vvm4gVyv
    
.. _get_session_token:

.. index::
   single: API authentication; session token

Getting a session token
=======================
* **Relative URL:** /db/{database}/oauth/get_session_token
* **Supported methods:** GET, POST

The application uses the access token and its consumer key to obtain a session
token.  The session token is valid for 12 hours before it expires.  The request
needs to contain the following parameters and to be signed using the consumer
secret and access token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (access token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970) - this must be
   within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the session token.  It is usually a 32 character alphanumeric
      string.
    * e.g. H8CjIS8Ikq6hwCUqUfF1l4pTaCYl8Ljw
 * oauth_token_secret
    * This is the secret associated with the session token.  It is usually a 
      32 character alphanumeric string.
    * e.g. RfponbaNPO7tkZ2miHFISk0pMndePNfJ
    
.. _accessing_protected_resources:

.. index::
   single: API authentication; accessing protected resources
 
Accessing protected resources
=============================
* **Supported methods:** GET, POST

The application uses the session token and its consumer key to access a 
protected resource.  The request needs to contain the following parameters and
to be signed using the consumer secret and session token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (session token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970) - this must be
   within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')
  