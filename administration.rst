#####################
Administrator's guide
#####################

Please note that links displayed within the curation interface will vary depending on database contents and the permissions of the curator.

.. index::
   single: user types

*************
Types of user
*************
There are three types of user in BIGSdb:

* User - can view data but never modify it. Users should be created for every submitter of data so that records can be tracked, even if they do not actually use the database. Individual isolate records may not be available to every user if access control lists (ACLs) are configured for the database.
* Curator - can modify data but does not have full control of the database. :ref:`Individual permissions <curator_permissions>` can be set for each curator, so their roles can be controlled. A curator with no specific permissions set has no more power than a standard user.
* Admin - has full control of the database, including setting permissions for curators and setting user passwords if built-in authentication is in use.

.. _curator_permissions:

.. index::
   single: permissions

*******************
Curator permissions
*******************
Individual permissions can be set for each curator:

* disable_access - if set to true, this user is completely barred from access.
* modify_users - allowed to add or modify user records. They can change the status of users, but can not revoke admin priveleges from an account. They can also not raise the status of a user to admin level.
* modify_usergroups - allowed to add or modify user groups and add users to these groups.
* set_user_passwords - allowed to modify other users' passwords (if built-in authentication is in use).
* modify_loci - allowed to add or modify loci.
* modify_schemes - allowed to add or modify schemes.
* modify_sequences - allowed to add sequences to the sequence bin (for isolate databases) or new allele definitions (for sequence definition databases).
* modify_isolates - allowed to add or modify isolate records.
* modify_isolates_acl - allowed to control who accesses isolate records (provided they themselves have access to a particular isolate).
* modify_projects - allowed to create projects, modify their descriptions and add or remove isolate records to these.
* modify_composites - allowed to add or modify composite fields (fields made up of other fields, including scheme fields defined in external databases). Composite fields involve defining regular expressions that are evaluated by Perl - this can be dangerous so this permission should be granted with discretion.
* modify_field_attributes - allow user to create or modify secondary field attributes (lookup tables) for isolate record fields.
* modify_value_attributes - allow user to add or modify secondary field values for isolate record fields.
* modify_probes - allow user to define PCR or hybridization reactions to filter tag scanning.
* tag_sequences - allowed to tag sequences with locus information.
* designate_alleles - allowed to manually designate allele numbers for isolate records.
* modify_profiles - allowed to add or modify scheme profiles (only used in a sequence definitions database).

Permissions can be set by clicking the '+' button next to 'user permissions' on the curator's interface: 

.. image:: /images/administration/add_user_permissions.png

Set specific permissions and then click 'Submit'.
   
.. image:: /images/administration/add_user_permissions2.png

If permissions have already been set for a user, click the 'Update or delete' link on the curator's page instead.

.. image:: /images/administration/add_user_permissions3.png

then search for the user by entering specific criteria, or simply press 'Submit' to display all users.  Update a specific user by clicking on the 'Update' link next to their name.

.. image:: /images/administration/add_user_permissions4.png

.. index::
   single: permissions; locus curation
   single: permissions; scheme curation

***********************************************************
Locus and scheme permissions (sequence definition database)
***********************************************************
To be allowed to define alleles or scheme profiles, curators must be granted specific permission for each locus and scheme by adding their user id number to the 'locus curator' and 'scheme curator' lists.

The easiest way to modify these lists is to use the batch update link next to 'locus curator control list' and 'scheme curator control list':

.. image:: /images/administration/update_locus_curator_list.png

Select the curator from the list:

.. image:: /images/administration/update_locus_curator_list2.png

Then select loci/schemes that the user is allowed to curate in the left hand 'Available' list, and click the right button to move these to the 'Selected' list:

.. image:: /images/administration/update_locus_curator_list3.png

If you uncheck the 'Hide curator name from public view' checkbox, the curator name and E-mail address will appear alongside loci in the download table on the website.

.. index::
   single: access; control lists

******************
Controlling access
******************

Access control lists
====================
If access control lists are in use (set the read_access attribute to 'acl' in the system tag of the database XML configuration file), viewing and modifying of individual isolates can be restricted to particular users or usergroups.

.. warning:: Please note that access control lists are likely to be deprecated in future releases.  This is in favour of creating a new class of user that would be allowed to curate their own data only.

New isolate records are automatically set with the following access control:

* All users: read, not write (all users are members of 'All users' group).
* Curator who added data: read and write.

All access controls can be modified by an admin or curator with appropriate permission. This can be done for individual isolate records or in batch mode following an isolate search in the curation interface.

.. _default_access:

.. index::
   single: access; restricting

Restricting particular configurations to specific user accounts
===============================================================
Suppose you only wanted specific users to access a database configuration.

In the config.xml, add the following directive: ::

 default_access="deny"

This tells BIGSdb to deny access to anybody unless their account name appears within a file called users.allow within the config directory. The users.allow file should contain one username per line.

Alternatively, you can deny access to specific users, while allowing every other authenticated user. In config.xml, add the following directive: ::

 default_access="allow"

This tells BIGSdb to allow access to anybody unless their account name appears within a file called users.deny within the config directory. The users.deny file should contain one username per line.

.. index::
   single: passwords; setting

**********************
Setting user passwords
**********************
*Please note that these instructions only apply if using the built-in BIGSdb authentication system.*

If you are an administrator or a curator with specific permission to change other users' passwords, you should see a link to 'set user passwords' at the bottom of the curator's index page. Click this.

.. image:: /images/administration/set_passwords.png

Select the appropriate user from the drop-down list box and enter the new password twice where prompted.

.. image:: /images/administration/set_passwords2.png

Click 'Set password' and the password will be updated.

.. _set_first_password:

.. index::
   single: passwords; setting; first user

*******************************
Setting the first user password
*******************************
To set the first administrator's password for a new database, use the add_user.pl script found in the scripts/maintenance directory: ::

 add_user.pl [-a] -d <dbase> -n <username> -p <password>

The first user account needs to be added to the database :ref:`manually <setup_admin_user>`.

.. index::
   single: plugins; enabling

****************
Enabling plugins
****************
Some plugins can be enabled/disabled for specific databases. If you look in the get_attributes function of the specific plugin file and see a value for system_flag, this value can be used in the system tag of the database configuration XML file to enable the plugin.

For example, the get_attributes function of the BURST plugin looks like: ::

 sub get_attributes {
	my %att = (
		name        => 'BURST',
		author      => 'Keith Jolley',
		affiliation => 'University of Oxford, UK',
		email       => 'keith.jolley@zoo.ox.ac.uk',
		description => 'Perform BURST cluster analysis on query results query results',
		category    => 'Cluster',
		buttontext  => 'BURST',
		menutext    => 'BURST',
		module      => 'BURST',
		version     => '1.0.0',
		dbtype      => 'isolates,sequences',
		section     => 'postquery',
		order       => 10,
		system_flag => 'BURST',
		input       => 'query',
		requires    => 'mogrify',
		min         => 2,
		max         => 1000
	);
	return \%att;
 }

The 'system_flag' attribute is set to 'BURST', so this plugin can be enabled for a database by adding: ::

 BURST="yes"

to the system tag of the database XML file. If the system_flag value is not defined then the plugin is always enabled if it is installed on the system.

.. index::
   single: updates; disabling

**************************************
Temporarily disabling database updates
**************************************
There may be instances where it is necessary to temporarily disable database updates. This may be during periods of server or database maintenance, for instance when running on a backup database server.

Updates can be disabled on a global or database-specific level.

Global
======
In the /etc/bigsdb/bigsdb.conf file, add the following line: ::

  disable_updates=yes

An optional message can also be displayed by adding a disable_update_message value, e.g. ::

  disable_update_message=The server is currently undergoing maintenance.

Database-specific
=================
The same attributes described above for use in the bigsdb.conf file can also be used within the system tag of the database config.xml file, e.g. ::

 <system
   db="bigsdb_neisseria"
   dbtype="isolates"
   ...
   disable_updates="yes"
   disable_update_message="The server is currently undergoing maintenance."

.. index::
   pair: hosts; mapping 

************
Host mapping
************
During periods of server maintenance, it may be necessary to map a database host to an alternative server. This would allow a backup database server to be used while the primary database server is unavailable. In this scenario, you would probably also want to disable updates.

Host mapping can be achieved by editing the /etc/bigsdb/host_mapping.conf file. Each host mapping is placed on a single line, with the current server followed by any amount of whitespace and then the new mapped host, e.g. ::

 #Existing_host      Mapped_host
  server1            server2
  localhost	     server2

[Lines beginning with a hash are comments and are ignored.]

This configuration would use server2 instead of server 1 or localhost wherever they are defined in the database configuration (either host attribute in the database config.xml file, or within the loci or schemes tables).

*********************
Improving performance
*********************

.. index::
   single: performance; mod_perl 

Use mod_perl
============
The single biggest improvement to speed can be obtained by running BIGSdb under mod_perl. There's very little point trying anything else until you have mod_perl set up and running - this can improve start-up performance a hundred-fold since the script isn't compiled on each page access but persists in memory.

.. index::
   single: performance; caching schemes

Cache scheme definitions within an isolate database
===================================================
If you have a large number of allelic profiles defined for a scheme, you can cache these definitions within an isolate database to speed up querying of isolates by scheme criteria (e.g. by ST for a MLST scheme).

To do this use the update_scheme_caches.pl script found in the scripts/maintenance directory, e.g. to cache all schemes in the pubmlst_bigsdb_neisseria_isolates database ::

 update_scheme_caches.pl -d pubmlst_bigsdb_neisseria_isolates

This script creates indexed tables within the isolate database called temp_scheme_X and temp_isolates_scheme_fields_1 (where X is the scheme_id). If these table aren't present, they are created as temporary tables every time a query is performed that requires a join against scheme definition data. This requires importing all profile definitions from the definitions database and determining scheme field values for all isolates. This may sound like it would be slow but caching only has a noticeable effect once you have >5000 profiles.

Note that you will need to run this script periodically as a CRON job to refresh the cache.

If queries are taking longer than 5 seconds to perform and a cache is not in place, you will see a warning message in bigsdb.log suggesting that the caches be set up.  Unless you see this warning regularly, you probably don't need to do this.

.. index::
   single: performance; materialized views

Use materialized views for scheme definitions
=============================================
Because of the way BIGSdb allows any number of profile schemes to be set up, the data are stored in a normalised manner in multiple tables. A database view, e.g. scheme_1, is created that joins these tables so that they can be queried as you would a single table. A view, however, is only a pre-selected query rather than a physical table and you can not index columns on it to optimise query performance.

A materialized view is a real table that is created from the view and refreshed every time the data in the underlying view changes. Because it is a real table, the database doesn't need to perform these joins every time it is queried and indexes can be set up on it, both of which greatly speeds up querying.

To use materialized views within a seqdef database set the following attribute in the system tag of the XML description file: ::

 materialized_views="yes"

You will then need to run the 'configuration repair' function at the bottom of the administrator's main curation page for each scheme. This rebuilds the view and creates a materialized view called mv_scheme_X. This materialized view is updated automatically whenever profile data are added or altered via the web interface.

If you want an isolate database to benefit from this materialized view, make sure you put 'mv_scheme_X' (where X is the scheme id) in the dbase_table field (rather than 'scheme_X') when setting up the scheme in the isolate database configuration.

Please note that if you make changes to your profile data by means other than the web interface then the materialized view will not be updated. You can update it by running the following SQL command: ::

 SELECT refresh_matview('mv_scheme_X');

The materialized view is used, for example, for looking up a ST from a profile and vice-versa. Significant speed improvements will only be realised if you have lots of profiles (>5000) and you are doing lots of lookups, e.g. displaying more than the default 25 records per page.

.. index::
   pair: partitioning; sets

********************
Dataset partitioning
********************

Sets
====
Along with loci, schemes and groups of schemes, BIGSdb also has the concept of a 'set'. Sets provide a means to take a large database with multiple loci and/or schemes and present a subset of these as though it was a complete database. The loci and schemes chosen to belong to a set can be renamed when used with this set. The rationale for this is that in a database with disparate isolates and a large number of loci, the naming of these loci may have to be long to specify a species name. For example, you may have a database that contains multiple MLST schemes for different species, but since these schemes may use different fragments of the same genes they may have to be named something like 'Streptococcus_pneumoniae_MLST_aroE' to uniquely specify them. If we define a set for 'Streptococcus pneumoniae' we can then choose to only include S. pneumoniae loci and therefore shorten their names, e.g. to 'aroE'.

Additional metadata fields can also be associated with each set so it is possible to have a database containing genomes from multiple species and a generic set of metadata, then have additional specific metadata fields for particular species or genera. These additional fields only become visible and searchable when the specific set that they belong to has been selected.

Configuration of sets
=====================
First sets need to be enabled in the XML configuration file (config.xml) of the database. Add the following attribute to the system tag: ::

 sets="yes"

With this attribute, the curation interface now has options to add sets, and then add loci or schemes to these sets.

.. image:: /images/administration/dataset_partitioning.png

The name of a locus or scheme to use within a set can be defined in the set_name field when adding loci or schemes to a set. Common names can also be set for loci - equivalent to the common name used within the loci table.

Now when a user goes to the contents page of the database they will be presented with a dropdown menu of datasets and can choose either the 'whole database' or a specific set. This selection is remembered between sessions.

.. image:: /images/administration/dataset_partitioning2.png

Alternatively, a specific set can be selected within the XML config file so that only a specific set is available when accessed via that configuration. In that case, the user would be unaware that the database contains anything other than the loci and schemes available within the set.

To specify this, add the following attributute to the system tag: ::

 set_id="1"

where the value is the name of the set.

Set metadata
============
Additional metadata fields can be set within the XML configuration file. They are specified as belonging to a metaset by prefixing the field name with 'meta_NAME:' where NAME is the name of the metaset, e.g. ::

 <field type="text" required="no" length="30" maindisplay="no" 
     optlist="yes">meta_1:clinical_outcome
   <optlist>
     <option>no sequeleae</option>
     <option>hearing loss</option>
     <option>amputation</option>
     <option>death</option>
   </optlist>
 </field>

Metaset fields can be defined just like any other :ref:`provenance field <isolate_xml>` and their position in the output is determined by their position in the XML file.

Metaset fields can then be added to a set using the 'Add set metadata' link on the curator's page.

.. image:: /images/administration/dataset_partitioning3.png

A new database table needs to be added for each metaset. This should contain all the fields defined for a metaset. The table should also contain an isolate_id field to act as the foreign key linking to the isolate table, e.g. the SQL would look something like the following: ::

 CREATE TABLE meta_1 (
 isolate_id integer NOT NULL,
 town text,
 clinical_outcome text,
 PRIMARY KEY (isolate_id),
 CONSTRAINT m1_isolate_id FOREIGN KEY (isolate_id) REFERENCES isolates
 ON DELETE CASCADE
 ON UPDATE CASCADE
 );

 GRANT SELECT,UPDATE,INSERT,DELETE ON meta_1 TO apache;

The above creates the database table for a metaset called '1', defining new text fields for 'town' and 'clinical_outcome'.

Set views
=========
Finally the isolate record table can be partitoned using database views and these views associated with a set. Create views using something like the following: ::

 CREATE VIEW spneumoniae AS SELECT * FROM isolates WHERE species = 'Streptococcus pneumoniae';
 GRANT SELECT ON spneumoniae TO apache;

Add the available views to the XML file as a comma separated list in the system tag 'views' attribute: ::

  <system
   .....
   sets="yes"
   views="spneumoniae,saureus"
  >
  </system>

Set the view to the set by using the 'Add set view' link on the curator's page.

Using only defined sets
=======================
The only_sets attribute can be set to 'yes' to disable the option for 'Whole database' so that only sets can be viewed, e.g. ::

  <system
   .....
   sets="yes"
   only_sets="yes"
  >
  </system>

.. _add_new_loci:

***************
Adding new loci
***************

.. index::
   pair: locus; adding

Sequence definition databases
=============================

Single locus
------------
Click the add (+) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_seqdef.png

Fill in the web form with appropriate values. Required fields have an exclamation mark (!) next to them:

.. _seqdef_locus_fields:

* id - The name of the locus.

  * Allowed: any value starting with a letter or underscore.

* data_type - Describes whether the locus is defined by nucleotide or peptide sequence.

  * Allowed: DNA/peptide.

* allele_id_format - The format for allele identifiers.

  * Allowed: integer/text.

* length_varies	- Sets whether alleles can vary in length.	

  * Allowed: true/false.

* coding_sequence - Sets whether the locus codes for a protein.

  * Allowed: true/false.

* formatted_name - Name with HTML formatting (optional).

  * This allows you to add formatting such as bold, italic, underline and superscripting to locus names as they appear in the web interface.
  * Allowed: valid HTML.

* common_name - The common name for the locus (optional).

  * Allowed: any value.

* formatted_common_name - Common name with HTML formatting (optional).

  * Allowed: valid HTML.

* allele_id_regex - `Regular expression <http://en.wikipedia.org/wiki/Regular_expression>`_ to enforce allele id naming (optional).

  * ^: the beginning of the string
  * $:the end of the string
  * \d: digit
  * \D: non-digit
  * \s: white space character
  * \S: non white space character
  * \w: alpha-numeric plus '_'
  * .: any character
  * \*: 0 or more of previous character
  * +: 1 or more of previous character
  * e.g. ^F\d-\d+$ states that an allele name must begin with a F followed by a single digit, then a dash, then one or more digits, e.g. F1-12 

* length - Standard length of locus (required if length_varies is set to false.

  * Allowed: any integer.

* min_length - Minimum length of locus (optional).

  * Allowed: any integer.

* max_length - Maximum length of locus (optional).

  * Allowed: any integer (larger than the minimum length).

* orf - Open reading frame of locus (optional). 

  * 1-3 are the forward reading frame, 4-6 are the reverse reading frames.
  * Allowed: 1-6.

* genome_position - The start position of the locus on a reference genome (optional).

  * Allowed: any integer.

* match_longest - Specifies whether in a sequence query to only return the longest match (optional).

  * This is useful for some loci that can have some sequences shorter than others, e.g. peptide loci defining antigenic loops.  This can lead to instances of one sequence being longer than another but otherwise being identical.  In these cases, usually the longer sequence is the one that should be matched.
  * Allowed: true/false. 

* full_name - Full name of the locus (optional).

  * Allowed: any value.

* product - Name of gene product (optional).

  * Allowed: Any value.

* description - Description of the locus (optional).

  * Allowed: any value.

* aliases - Alternative names for the locus (optional).

  * Enter each alias on a separate line in the text box.
  * Allowed: any value.

* pubmed_ids - PubMed ids of publications describing the locus (optional).

  * Enter each PubMed id on a separate line in the text box.
  * Allowed: any integer.

* links - Hyperlinks pointing to additional resources to display in the locus description (optional).

  * Enter each link on a separate line in the format with the URL first, followed by a | then the description (URL|description).

.. index::
   pair: locus; adding

Batch adding
------------
Click the batch add (++) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_seqdef2.png

Click the link to download a header line for an Excel spreadsheet:

.. image:: /images/administration/add_new_loci_seqdef3.png

Fill in the spreadsheet using the fields described for :ref:`adding single loci <seqdef_locus_fields>`.

Fill in the spreadsheet fields using the table above as a guide, then paste the completed table into the web form and press 'Submit query'.

Isolate databases
=================

.. index::
   pair: locus; adding

Single locus
------------

.. index::
   pair: locus; adding

Click the add (+) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_isolates.png

Fill in the web form with appropriate values. Required fields have an exclamation mark (!) next to them:

.. _isolate_locus_fields:

* id - The name of the locus

  * Allowed: any value starting with a letter or underscore.

* data_type - Describes whether the locus is defined by nucleotide or peptide sequence.

  * Allowed: DNA/peptide.

* allele_id_format - The format for allele identifiers.

  * Allowed: integer/text.

* length_varies	- Sets whether alleles can vary in length.

  * Allowed: true/false.

* coding_sequence - Sets whether the locus codes for a protein.

  * Allowed: true/false.

* flag_table - Set to true to specify that the sequence definition database contains an allele flag table (which is the case for BIGSdb version 1.4 onwards).

  * Allowed: true/false.

* isolate_display - Sets how alleles for this locus are displayed in a detailed isolate record - this can be overridden by user preference.

  * Allowed: allele only/sequence/hide.

* main_display - Sets whether or not alleles for this locus are displayed in a main results table by default - this can be overridden by user preference.

  * Allowed: true/false.

* query_field - Sets whether or not alleles for this locus can be used in queries by default - this can be overridden by user preference.

  * Allowed: true/false.

* analysis - Sets whether or not alleles for this locus can be used in analysis functions by default - this can be overridden by user preference.

  * Allowed: true/false.

* formatted_name - Name with HTML formatting (optional).

  * This allows you to add formatting such as bold, italic, underline and superscripting to locus names as they appear in the web interface.
  * Allowed: valid HTML.

* common_name - The common name for the locus (optional).

  * Allowed: any value.

* formatted_common_name - Common name with HTML formatting (optional).

  * Allowed: valid HTML.

* allele_id_regex - `Regular expression <http://en.wikipedia.org/wiki/Regular_expression>`_ to enforce allele id naming.

  * ^: the beginning of the string
  * $:the end of the string
  * \d: digit
  * \D: non-digit
  * \s: white space character
  * \S: non white space character
  * \w: alpha-numeric plus '_'
  * .: any character
  * \*: 0 or more of previous character
  * +: 1 or more of previous character
  * e.g. ^F\d-\d+$ states that an allele name must begin with a F followed by a single digit, then a dash, then one or more digits, e.g. F1-12 	
   
* length - Standard length of locus (required if length_varies is set to false).

  * Allowed: any integer.

* orf - Open reading frame of locus (optional). 1-3 are the forward reading frame, 4-6 are the reverse reading frames.

  * Allowed: 1-6.

* genome_position - The start position of the locus on a reference genome.

  * Allowed: any integer.

* match_longest - Only select the longest exact match when tagging/querying.  

  * This is useful for some loci that can have some sequences shorter than others, e.g. peptide loci defining antigenic loops.  This can lead to instances of one sequence being longer than another but otherwise being identical.  In these cases, usually the longer sequence is the one that should be matched.
  * Allowed: true/false.

* reference_sequence - Sequence used by the automated sequence comparison algorithms to identify sequences matching this locus.  **This is only used if a sequence definition database has not been set up for this locus.**

* pcr_filter - Set to true if this locus is further defined by genome filtering using in silico PCR.

  * Allowed: true/false.

* probe_filter - Set to true if this locus is further defined by genome filtering using in silico hybdridization.

  * Allowed: true/false.

* dbase_name - Name of database (system name).

  * Allowed: any text.

* dbase_host - Resolved name of IP address of database host - leave blank if running on the same machine as the isolate database.

  * Allowed: network address, e.g. 129.67.26.52 or zoo-oban.zoo.ox.ac.uk

* dbase_port - Network port on which the sequence definition database server is listening - leave blank unless using a non-standard port (5432).

  * Allowed: integer.

* dbase_user - Name of user with permission to access the sequence definition database - depending on the database configuration you may be able to leave this blank.

  * Allowed: any text (no spaces).

* dbase_password - Password of database user - again depending on the database configuration you may be able to leave this blank.

  * Allowed: any text (no spaces).

* dbase_table - Table in the sequence definition database that contains allele sequences for this locus. If the definition database uses BIGSdb this will be 'sequences'.

  * Allowed: any text (no spaces).

* dbase_id_field - Primary field in sequence database that defines allele. If the definition database uses BIGSdb this will be 'allele_id'.

  * Allowed: any text (no spaces).

* dbase_id2_field - Secondary field in sequence database that defines alleles. If dbase_id_field uniquely defines alleles for this locus then this should be left blank. If the definition database uses BIGSdb this will be 'locus'.

  * Allowed: any text (no spaces).

* dbase_id2_value - Secondary field value in sequence database that defines alleles. If dbase_id_field uniquely defines alleles for this locus then this should be left blank. If the definition database uses BIGSdb this will be the name of the locus used in the id field

  * Allowed: any text (no spaces).

* dbase_seq_field - Field in sequence database containing allele sequence. If the definition database uses BIGSdb this will be 'sequence'.

  * Allowed: any text (no spaces).

* description_url - The URL used to hyperlink to locus information in the isolate information page. This can either be a relative (e.g. /cgi-bin/...) or an absolute (containing http://) URL.	

  * Allowed: any valid URL.

* url - The URL used to hyperlink to information about the allele. This can either be a relative or absolute URL. If [?] (including the square brackets) is included then this will be substituted for the allele value in the resultant URL. To link to the appropiate allele info page on a corresponding seqdef database you would need something like /cgi-bin/bigsdb/bigsdb.pl?db=pubmlst_neisseria_seqdef&page=alleleInfo&locus=abcZ&allele_id=[?].

  * Allowed: any valid URL.

.. index::
   single: locus; adding; copying existing record

Using existing locus definition as a template
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. todo:: Add description.

.. index::
   pair: locus; adding

Batch adding
------------
Click the batch add (++) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_isolates2.png

Click the link to download an Excel template:

.. image:: /images/administration/add_new_loci_isolates3.png

Fill in the spreadsheet fields using the :ref:`table above as a guide <isolate_locus_fields>`, then paste the completed table into the web form and press 'Submit query'.

**********************************
Defining locus extended attributes
**********************************

.. todo:: Add description.

.. index::
   pair: scheme; adding
   
****************
Defining schemes
****************
Schemes are collections of loci that may be associated with particular fields - one of these fields can be a primary key, i.e. a field that uniquely defines a particular combination of alleles at the associated loci.

A specific example of a scheme is MLST - :ref:`see workflow for setting up a MLST scheme <mlst_workflow>`.

To set up a new scheme, you need to:

#. Add a new scheme description.
#. Define loci as 'scheme members'.
#. Add 'scheme fields' associated with the scheme.

Sequence definition databases
=============================
As with all configuration, tables can be populated using the batch interface (++) or one at a time (+). Details for the latter are described below:

Click the add (+) scheme link on the curator's interface contents page.

.. image:: /images/administration/add_new_scheme_seqdef.png

Fill in the scheme description in the web form. The next available scheme id number will be filled in already.

The display_order field accepts an integer that can be used to order the display of schemes in the interface - this can be left blank if you wish.

.. image:: /images/administration/add_new_scheme_seqdef2.png

To add loci to the scheme, click the add (+) scheme members link on the curator's interface contents page.

.. image:: /images/administration/add_new_scheme_seqdef3.png

Select the scheme name and a locus that you wish to add to the scheme from the appropriate drop-down boxes. :ref:`Loci need to have already been defined <add_new_loci>`. The field_order field allows you to set the display order of the locus within a profile - if these are left blank that alphabetical ordering is used.

.. image:: /images/administration/add_new_scheme_seqdef4.png

To add scheme fields, click the add (+) scheme fields link on the curator's interface contents page.

.. image:: /images/administration/add_new_scheme_seqdef5.png

Fill in the web form with appropriate values. Required fields have an exclamation mark (!) next to them:

.. image:: /images/administration/add_new_scheme_seqdef6.png

* scheme_id - Dropdown box of scheme names.

  * Allowed: selection from list.

* field	- Field name.

  * Allowed: any value.

* type - Format for values.

  * Allowed: text/integer/date.

* primary_key -	Set to true if field is the primary key. There can only be one primary key for a scheme.

  * Allowed: true/false.

* dropdown - Set to true if a dropdown box is displayed in the query interface, by default, for values of this field to be quickly selected. This option can be overridden by user preferences.

  * Allowed: true/false.

* description - This field isn't currently used.

* field_order - Integer that sets the position of the field within scheme values in any results.

  * Allowed: any integer.

* value_regex - `Regular expression <http://en.wikipedia.org/wiki/Regular_expression>`_ to enforce field values.
  
  * ^: the beginning of the string
  * $:the end of the string
  * \d: digit
  * \D: non-digit
  * \s: white space character
  * \S: non white space character
  * \w: alpha-numeric plus '_'
  * .: any character
  * \*: 0 or more of previous character
  * +: 1 or more of previous character

Isolate databases
=================
As with all configuration, tables can be populated using the batch interface (++) or one at a time (+). Details for the latter are described below:

Click the add (+) scheme link on the curator's interface contents page.

.. image:: /images/administration/add_new_scheme_isolates.png

Fill in the scheme description in the web form. Required fields have an exclamation mark (!) next to them:

.. image:: /images/administration/add_new_scheme_isolates2.png

* id - Index number of scheme - the next available number will be entered automatically.	
  
  * Allowed: any positive integer.

* description - Short description - this is used in tables so make sure it's not too long.

  * Allowed: any text.

* isolate_display - Sets whether or not fields for this scheme are displayed in a detailed isolate record - this can be overridden by user preference.

  * Allowed: allele only/sequence/hide.

* main_display - Sets whether or not fields for this scheme are displayed in a main results table by default - this can be overridden by user preference.

  * Allowed: true/false.

* query_field - Sets whether or not fields for this scheme can be used in queries by default - this can be overridden by user preference.

  * Allowed: true/false.

* query_status - Sets whether a dropdown list box should be displayed in the query interface to filter results based on profile completion for this scheme - this can be overridden by user preference.

  * Allowed: true/false.

* analysis - Sets whether or not alleles for this locus can be used in analysis functions by default - this can be overridden by user preference.
  
  * Allowed: true/false.

* dbase_name - Name of seqdef database (system name) containing scheme profiles (optional).

  * Allowed: any text.

* dbase_host - Resolved name of IP address of database host - leave blank if running on the same machine as the isolate database (optional).

  * Allowed: network address, e.g. 129.67.26.52 or zoo-oban.zoo.ox.ac.uk

* dbase_port - Network port on which the sequence definition database server is listening - leave blank unless using a non-standard port, 5432 (optional).

  * Allowed: integer.

* dbase_user - Name of user with permission to access the sequence definition database - depending on the database configuration you may be able to leave this blank (optional).

  * Allowed: any text (no spaces).

* dbase_password - Password of database user - again depending on the database configuration you may be able to leave this blank (optional).

  * Allowed: any text (no spaces).

* dbase_table - Table in the sequence definition database that contains profiles for this scheme. If the definition database uses BIGSdb this will be 'scheme_X' where X is the scheme id number in the seqdef database.

  * Allowed: any text (no spaces).

* display_order - Integer reflecting the display position for this scheme within the interface (optional).

  * Allowed: any integer.

* allow_missing_loci - Allow profile definitions to contain '0' (locus missing) or 'N' (any allele).

.. index::
   single: client databases

***************************
Setting up client databases
***************************
Sequence definition databases can have any number of isolate databases that connect as clients. Registering these databases allows the software to perform isolate data searches relevant to results returned by the sequence definition database, for example:

* Determine the number of isolates that a given allele is found in and link to these.
* Determine the number of isolates that a given scheme field, e.g. a sequence type, is found in and link to these.
* Retrieve specific attributes of isolates that have a given allele, e.g. species that have a particular 16S allele, or penicillin resistance given a particular penA allele.

Multiple client databases can be queried simultaneously.

To register a client isolate database for a sequence definition database, click the add (+) client database link on the curator's interface contents page.

.. image:: /images/administration/add_client_databases.png

Fill in the web form with appropriate values. Required fields have an exclamation mark (!) next to them:

.. image:: /images/administration/add_client_databases2.png

* id - Index number of client database. The next available number is entered automatically but can be overridden.

  * Allowed: any positive integer.

* name - Short description of database. This is used within the interface result tables so it is better to make it as short as possible.

  * Allowed: any text.

* description -	Longer description of database.

  * Allowed: any text.

* dbase_name - Name of database (system name).

  * Allowed: any text.

* dbase_config_name - Name of database configuration - this is the text string that appears after the db= part of script URLs.

  * Allowed: any text (no spaces)

* dbase_host - Resolved name of IP address of database host (optional).

  * Allowed: Network address, e.g. 129.67.26.52 or zoo-oban.zoo.ox.ac.uk
  * Leave blank if running on the same machine as the seqdef database.

* dbase_port - Network port on which the client database server is listening (optional)

  * Allowed: integer.
  * Leave blank unless using a non-standard port (5432).

* dbase_user - Name of user with permission to access the client database

  * Allowed: any text (no spaces).
  * Depending on the database configuration you may be able to leave this blank.	
* dbase_password - Password of database user
  
  * Allowed: any text (no spaces).
  * Depending on the database configuration you may be able to leave this blank.

* url -	URL of client database bigsdb.pl script

  * Allowed: valid script path.
  * This can be relative (e.g. /cgi-bin/bigsdb/bigsdb.pl) if running on the same machine as the seqdef database or absolute (including http://) if on a different machine.

Look up isolates with given allele
==================================
To link a locus, click the add (+) client database loci link on the curator's interface contents page.	

.. image:: /images/administration/add_client_databases3.png

Link the locus to the appropriate client database using the dropdown list boxes. If the locus is named differently in the client database, fill this name in the locus_alias.

.. image:: /images/administration/add_client_databases4.png

Now when information on a given allele is shown following a query, the software will list the number of isolates with that allele and link to a search on the database to retrieve these.

.. image:: /images/administration/add_client_databases5.png

Look up isolates with a given scheme primary key
================================================
Setting this up is identical to setting up for alleles (see above) except you click on the add (+) client database schemes link and choose the scheme and client databases in the dropdown list boxes.

Now when information on a given scheme profile (e.g. MLST sequence type) is shown following a query, the software will list the number of isolates with that profile and link to a search on the database to retrieve these.

.. image:: /images/administration/add_client_databases6.png

Look up specific isolate database fields linked to a given allele
=================================================================
To link an allele to an isolate field, click the add (+) 'client database fields linked to loci' link on the curator's interface contents page.

.. image:: /images/administration/add_client_databases7.png

Select the client database and locus from the dropdown lists and enter the isolate database field that you'd like to link. The 'allele_query' field should be set to true.

.. image:: /images/administration/add_client_databases8.png

Now, in the allele record or following a sequence query that identifies an allele, all values for the chosen field from isolates with the corresponding allele are shown.

.. image:: /images/administration/add_client_databases9.png


.. index::
   single: rule-based queries

***************************
Rule-based sequence queries
***************************
The RuleQuery plugin has been designed to extract information from a pasted-in genome sequence, look up scheme fields and client database fields, and then format the output in a specified manner.

Rules are written in Perl, allowing the full power of this scripting language to be utilised. Helper functions that perform specific actions are available to the script (see example).

Please note that direct access to the database is prevented as are system calls.

Example rule code
=================
An example can be found on the `Neisseria sequence database <http://pubmlst.org/perl/bigsdb/bigsdb.pl?db=pubmlst_neisseria_seqdef&page=plugin&name=RuleQuery&ruleset=Clinical_identification>`_ that takes a genome sequence and determines a fine type and antibiotic resistance.

The code for this rule is as follows: ::

  #Clinical identification rule

  #Update job viewer status
  update_status({stage=>'Scanning MLST loci'});

  #Scan genome against all scheme 1 (MLST) loci
  scan_scheme(1);

  #Update job viewer status
  update_status({percent_complete=>30, stage=>'Scanning PorA and FetA VRs'});

  #Scan genome against the PorA VR and FetA VR loci
  scan_locus($_) foreach qw(PorA_VR1 PorA_VR2 FetA_VR);

  Add text to main output
  append_html("<h1>Strain type</h1>");

  #Set variables for the scanned results.  These can be found in the
  #$results->{'locus'} hashref
  my %alleles;
  $alleles{$_} = $results->{'locus'}->{$_} // 'ND' foreach qw(PorA_VR1 PorA_VR2);
  $alleles{'FetA_VR'} = $results->{'locus'}->{'FetA_VR'} // 'F-ND';

  #Scheme field values are automatically determined if a complete
  #profile is available.  These are stored in the $results->{'scheme'} hashref
  my $st = $results->{'scheme'}->{1}->{'ST'} // 'ND';
  append_html("<ul><li>P1.$alleles{'PorA_VR1'}, $alleles{'PorA_VR2'}; $alleles{'FetA_VR'}; ST-$st ");

  #Reformat clonal complex using a regular expression, e.g.
  #'ST-11 clonal complex/ET-37 complex' gets rewritten to 'cc11'
  my $cc =  $results->{'scheme'}->{1}->{'clonal_complex'} // '-';
  $cc =~ s/ST-(\S+) complex.*/cc$1/;

  append_html("($cc)</li></ul>");
  if ($st eq 'ND'){
    append_html("<p>ST not defined.  If individual MLST loci have been found "
    . "they will be displayed below:</p>");

    #The get_scheme_html function automatically formats output for a scheme.
    #Select whether to display in a table rather than a list, list all loci, and/or list fields.
    append_html(get_scheme_html(1, {table=>1, loci=>1, fields=>0}));
  }

  #Antibiotic resistance
  update_status({percent_complete=>80, stage=>'Scanning penA and rpoB'});
  scan_locus($_) foreach qw(penA rpoB);
  if (defined $results->{'locus'}->{'penA'} || defined $results->{'locus'}->{'rpoB'} ){
    append_html("<h1>Antibiotic resistance</h1><ul>");
    if (defined $results->{'locus'}->{'penA'}){
      append_html("<li><i>penA</i> allele: $results->{'locus'}->{'penA'}");

      #If a client isolate database has been defined and values have been defined in
      #the client_dbase_loci_fields table, the values for a field in the isolate database can be
      #retrieved based on isolates that have a particular allele designated.
      #The min_percentage attribute states that only values that are represented by at least that 
      #proportion of all isolates that had a value set are returned (null values are ignored).
      my $range = get_client_field(1,'penA','penicillin_range',{min_percentage => 75});
      append_html(" (penicillin MIC: $range->[0]->{'penicillin_range'})") if @$range;
      append_html("</li>");
    }  
    if (defined $results->{'locus'}->{'rpoB'}){
      append_html("<li><i>rpoB</i> allele: $results->{'locus'}->{'rpoB'}");
      my $range = get_client_field(1,'rpoB','rifampicin_range',{min_percentage => 75});
      append_html(" (rifampicin MIC: $range->[0]->{'rifampicin_range'})") if @$range;
      append_html("</li>");
    }      
    append_html("</ul>");
  }

Rule files
----------
The rule file is placed in a rules directory within the database configuration directory, e.g. /etc/bigsdb/dbase/pubmlst_neisseri_seqdef/rules. Rule files are suffixed with '.rule' and their name should be descriptive since it is used within the interface, i.e. the above rule file is named Clinical_identification.rule (underscores are converted to spaces in the web interface).

Linking to the rule query
-------------------------
Links to the rule query are not automatically placed within the web interface. The above rule query can be called using the following URL:

`<http://pubmlst.org/perl/bigsdb/bigsdb.pl?db=pubmlst_neisseria_seqdef&page=plugin&name=RuleQuery&ruleset=Clinical_identification>`_

To place a link to this within the database contents page an HTML file called job_query.html can be placed in a contents directory within the database configuration directory, e.g. in /etc/bigsdb/dbases/pubmlst_neisseria_seqdef/contents/job_query.html. This file should contain a list entry (i.e. surrounded with <li> and </li> tags) that will appear in the 'Query database' section of the contents page.

Adding descriptive text
-----------------------
Descriptive text for the rule, which will appear on the rule query page, can be placed in a file called description.html in a directory with the same name as the rule within the rule directory, e.g. in /etc/bigsdb/dbases/pubmlst_neisseria_seqdef/rules/Clinical_identification/description.html.

.. _mlst_workflow:

.. index::
   pair: adding; MLST scheme

*************************************
Workflow for setting up a MLST scheme
*************************************
The workflow for setting up a MLST scheme is as follows (the example seqdef database is called seqdef_db):

**Seqdef database**

1. Create appropriate loci
2.   Create new scheme 'MLST'
3.   Add scheme_field 'ST' with primary_key=TRUE (add clonal_complex if you want; set this with primary_key=FALSE)
4.   Add each locus as a scheme_member
5.   You'll then be able to add profiles

**Isolate database**

1. Create the same loci with the following additional parameters (example locus 'atpD')

  * dbase_name: seqdef_db
  * dbase_table: sequences
  * dbase_id_field: allele_id
  * dbase_id2_field: locus
  * dbase_id_value: atpD
  * dbase_seq_field: sequence
  * url: something like /cgi-bin/bigsdb/bigsdb.pl?db=seqdef_db&page=alleleInfo&locus=atpD&allele_id=[?]

2. Create scheme 'MLST' with:
  
  * dbase_name: seqdef_db
  * dbase_table: scheme_1 (or whatever the id of your seqdef scheme is)

3. Add scheme_field ST as before
4. Add loci as scheme_members

*****************************************************
Defining new loci based on annotated reference genome
*****************************************************

.. index::
   pair: locus; adding

.. todo:: Add description.

****************
Genome filtering
****************

.. todo:: Add description.

******************************
Setting locus genome positions
******************************

.. todo:: Add description.

*************************
Defining composite fields
*************************

.. todo:: Add description.

**********************************************
Extended provenance attributes (lookup tables)
**********************************************

.. todo:: Add description.

*************************************************
Checking external database configuration settings
*************************************************

.. todo:: Add description.

