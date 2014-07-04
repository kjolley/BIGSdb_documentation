#####################
Administrator's guide
#####################

*******
General
*******
Please note that links displayed within the curation interface will vary depending on database contents and the permissions of the curator.

Types of user
=============
There are three types of user in BIGSdb:

* User - can view data but never modify it. Users should be created for every submitter of data so that records can be tracked, even if they do not actually use the database. Individual isolate records may not be available to every user if access control lists (ACLs) are configured for the database.
* Curator - can modify data but does not have full control of the database. :ref:`Individual permissions <curator_permissions>` can be set for each curator, so their roles can be controlled. A curator with no specific permissions set has no more power than a standard user.
* Admin - has full control of the database, including setting permissions for curators and setting user passwords if built-in authentication is in use.

.. _curator_permissions:

Curator permissions
===================
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

Locus and scheme permissions (sequence definition database)
===========================================================
To be allowed to define alleles or scheme profiles, curators must be granted specific permission for each locus and scheme by adding their user id number to the 'locus curator' and 'scheme curator' lists.

The easiest way to modify these lists is to use the batch update link next to 'locus curator control list' and 'scheme curator control list':

.. image:: /images/administration/update_locus_curator_list.png

Select the curator from the list:

.. image:: /images/administration/update_locus_curator_list2.png

Then select loci/schemes that the user is allowed to curate in the left hand 'Available' list, and click the right button to move these to the 'Selected' list:

.. image:: /images/administration/update_locus_curator_list3.png

If you uncheck the 'Hide curator name from public view' checkbox, the curator name and E-mail address will appear alongside loci in the download table on the website. 

Controlling access
==================

Access control lists
--------------------
If access control lists are in use (set the read_access attribute to 'acl' in the system tag of the database XML configuration file), viewing and modifying of individual isolates can be restricted to particular users or usergroups.

**Please note that access control lists are likely to be deprecated in future releases.  This is in favour of creating a new class of user that would be allowed to curate their own data only.**

New isolate records are automatically set with the following access control:

* All users: read, not write (all users are members of 'All users' group).
* Curator who added data: read and write.

All access controls can be modified by an admin or curator with appropriate permission. This can be done for individual isolate records or in batch mode following an isolate search in the curation interface.

.. _default_access:

Restricting particular configurations to specific user accounts
---------------------------------------------------------------
Suppose you only wanted specific users to access a database configuration.

In the config.xml, add the following directive: ::

 default_access="deny"

This tells BIGSdb to deny access to anybody unless their account name appears within a file called users.allow within the config directory. The users.allow file should contain one username per line.

Alternatively, you can deny access to specific users, while allowing every other authenticated user. In config.xml, add the following directive: ::

 default_access="allow"

This tells BIGSdb to allow access to anybody unless their account name appears within a file called users.deny within the config directory. The users.deny file should contain one username per line.

Setting user passwords
======================
*Please note that these instructions only apply if using the built-in BIGSdb authentication system.*

If you are an administrator or a curator with specific permission to change other users' passwords, you should see a link to 'set user passwords' at the bottom of the curator's index page. Click this.

.. image:: /images/administration/set_passwords.png

Select the appropriate user from the drop-down list box and enter the new password twice where prompted.

.. image:: /images/administration/set_passwords2.png

Click 'Set password' and the password will be updated.

.. _set_first_password:

Setting the first password
--------------------------
To set the first administrator's password for a new database, use the add_user.pl script found in the scripts/maintenance directory: ::

 add_user.pl [-a] -d <dbase> -n <username> -p <password>

The first user account needs to be added to the database :ref:`manually <setup_admin_user>`.

Enabling plugins
================
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

Temporarily disabling database updates
======================================
There may be instances where it is necessary to temporarily disable database updates. This may be during periods of server or database maintenance, for instance when running on a backup database server.

Updates can be disabled on a global or database-specific level.

Global
------
In the /etc/bigsdb/bigsdb.conf file, add the following line: ::

  disable_updates=yes

An optional message can also be displayed by adding a disable_update_message value, e.g. ::

  disable_update_message=The server is currently undergoing maintenance.

Database-specific
-----------------
The same attributes described above for use in the bigsdb.conf file can also be used within the system tag of the database config.xml file, e.g. ::

 <system
   db="bigsdb_neisseria"
   dbtype="isolates"
   ...
   disable_updates="yes"
   disable_update_message="The server is currently undergoing maintenance."

Host mapping
============
During periods of server maintenance, it may be necessary to map a database host to an alternative server. This would allow a backup database server to be used while the primary database server is unavailable. In this scenario, you would probably also want to disable updates.

Host mapping can be achieved by editing the /etc/bigsdb/host_mapping.conf file. Each host mapping is placed on a single line, with the current server followed by any amount of whitespace and then the new mapped host, e.g. ::

 #Existing_host      Mapped_host
  server1            server2
  localhost	     server2

[Lines beginning with a hash are comments and are ignored.]

This configuration would use server2 instead of server 1 or localhost wherever they are defined in the database configuration (either host attribute in the database config.xml file, or within the loci or schemes tables).

Improving performance
=====================

Use mod_perl
------------
The single biggest improvement to speed can be obtained by running BIGSdb under mod_perl. There's very little point trying anything else until you have mod_perl set up and running - this can improve start-up performance a hundred-fold since the script isn't compiled on each page access but persists in memory.

Cache scheme definitions within an isolate database
---------------------------------------------------
If you have a large number of allelic profiles defined for a scheme, you can cache these definitions within an isolate database to speed up querying of isolates by scheme criteria (e.g. by ST for a MLST scheme).

To do this use the update_scheme_caches.pl script found in the scripts/maintenance directory, e.g. to cache all schemes in the pubmlst_bigsdb_neisseria_isolates database ::

 update_scheme_caches.pl -d pubmlst_bigsdb_neisseria_isolates

This script creates indexed tables within the isolate database called temp_scheme_X and temp_isolates_scheme_fields_1 (where X is the scheme_id). If these table aren't present, they are created as temporary tables every time a query is performed that requires a join against scheme definition data. This requires importing all profile definitions from the definitions database and determining scheme field values for all isolates. This may sound like it would be slow but caching only has a noticeable effect once you have >5000 profiles.

Note that you will need to run this script periodically as a CRON job to refresh the cache.

If queries are taking longer than 5 seconds to perform and a cache is not in place, you will see a warning message in bigsdb.log suggesting that the caches be set up.  Unless you see this warning, you probably don't need to do this.

Use materialized views for scheme definitions
---------------------------------------------
Because of the way BIGSdb allows any number of profile schemes to be set up, the data are stored in a normalised manner in multiple tables. A database view, e.g. scheme_1, is created that joins these tables so that they can be queried as you would a single table. A view, however, is only a pre-selected query rather than a physical table and you can not index columns on it to optimise query performance.

A materialized view is a real table that is created from the view and refreshed every time the data in the underlying view changes. Because it is a real table, the database doesn't need to perform these joins every time it is queried and indexes can be set up on it, both of which greatly speeds up querying.

To use materialized views within a seqdef database set the following attribute in the system tag of the XML description file: ::

 materialized_views="yes"

You will then need to run the 'configuration repair' function at the bottom of the administrator's main curation page for each scheme. This rebuilds the view and creates a materialized view called mv_scheme_X. This materialized view is updated automatically whenever profile data are added or altered via the web interface.

If you want an isolate database to benefit from this materialized view, make sure you put 'mv_scheme_X' (where X is the scheme id) in the dbase_table field (rather than 'scheme_X') when setting up the scheme in the isolate database configuration.

Please note that if you make changes to your profile data by means other than the web interface then the materialized view will not be updated. You can update it by running the following SQL command: ::

 SELECT refresh_matview('mv_scheme_X');

The materialized view is used, for example, for looking up a ST from a profile and vice-versa. Significant speed improvements will only be realised if you have lots of profiles (>5000) and you are doing lots of lookups, e.g. displaying more than the default 25 records per page.

Dataset partitioning
====================

Sets
----
Along with loci, schemes and groups of schemes, BIGSdb also has the concept of a 'set'. Sets provide a means to take a large database with multiple loci and/or schemes and present a subset of these as though it was a complete database. The loci and schemes chosen to belong to a set can be renamed when used with this set. The rationale for this is that in a database with disparate isolates and a large number of loci, the naming of these loci may have to be long to specify a species name. For example, you may have a database that contains multiple MLST schemes for different species, but since these schemes may use different fragments of the same genes they may have to be named something like 'Streptococcus_pneumoniae_MLST_aroE' to uniquely specify them. If we define a set for 'Streptococcus pneumoniae' we can then choose to only include S. pneumoniae loci and therefore shorten their names, e.g. to 'aroE'.

Additional metadata fields can also be associated with each set so it is possible to have a database containing genomes from multiple species and a generic set of metadata, then have additional specific metadata fields for particular species or genera. These additional fields only become visible and searchable when the specific set that they belong to has been selected.

Configuration of sets
---------------------
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
------------
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
---------
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
-----------------------
The only_sets attribute can be set to 'yes' to disable the option for 'Whole database' so that only sets can be viewed, e.g. ::

  <system
   .....
   sets="yes"
   only_sets="yes"
  >
  </system>

*****************************
Sequence definition databases
*****************************

Adding new loci
===============

Single locus
------------
Click the add (+) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_seqdef.png

Fill in the web form with appropriate values. Required fields have an exclamation mark (!) next to them:

.. _seqdef_locus_fields:

* id - The name of the locus.

  * Allowed: Any value starting with a letter or underscore.

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

  * Allowed: Any value.

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
  * e.g. ^F\d-\d+$ states that an allele name must begin with a F followed by a single digit, then a dash, then one or more digits, e.g. F1-12 	Any valid Perl regex

* length - Standard length of locus (required if length_varies is set to false.

  * Allowed: Any integer.

* min_length - Minimum length of locus (optional).

  * Allowed: Any integer.

* max_length - Maximum length of locus (optional).

  * Allowed: Any integer (larger than the minimum length).

* orf - Open reading frame of locus (optional). 

  * 1-3 are the forward reading frame, 4-6 are the reverse reading frames.
  * Allowed: 1-6.

* genome_position - The start position of the locus on a reference genome (optional).

  * Allowed: Any integer.

* match_longest - Specifies whether in a sequence query to only return the longest match (optional).

  * This is useful for some loci that can have some sequences shorter than others, e.g. peptide loci defining antigenic loops.  This can lead to instances of one sequence being longer than another but otherwise being identical.  In these cases, usually the longer sequence is the one that should be matched.
  * Allowed: true/false. 

* full_name - Full name of the locus (optional).

  * Allowed: Any value.

* product - Name of gene product (optional).

  * Allowed: Any value.

* description - Description of the locus (optional).

  * Allowed: Any value.

* aliases - Alternative names for the locus (optional).

  * Enter each alias on a separate line in the text box.
  * Allowed: Any value.

* pubmed_ids - PubMed ids of publications describing the locus (optional).

  * Enter each PubMed id on a separate line in the text box.
  * Allowed: Any integer.

* links - Hyperlinks pointing to additional resources to display in the locus description (optional).

  * Enter each link on a separate line in the format with the URL first, followed by a | then the description (URL|description).

Batch adding multiple loci
--------------------------
Click the batch add (++) loci link on the curator's interface contents page.

.. image:: /images/administration/add_new_loci_seqdef2.png

Click the link to download a header line for an Excel spreadsheet:

.. image:: /images/administration/add_new_loci_seqdef3.png

Fill in the spreadsheet using the fields described for :ref:`adding single loci <seqdef_locus_fields>`.

Fill in the spreadsheet fields using the table above as a guide, then paste the completed table into the web form and press 'Submit query'.
   
Defining schemes
================

Setting up client databases
===========================

Rule-based queries
==================

Workflow for setting up a MLST scheme
=====================================

*****************
Isolate databases
*****************

Adding new loci
===============

Genome filtering
================

Setting locus genome positions
==============================

Defining schemes
================

Defining composite fields
=========================

Extended provenance attributes (lookup tables)
==============================================

Checking external database configuration settings
=================================================
