##############
Database setup
##############
There are two types of BIGSdb database:

* sequence definition databases, containing
  
  * allele sequences and their identifiers
  * scheme data, e.g. MLST profile definitions

* isolate databases, containing
 
  * isolate provenance metadata
  * genome sequences
  * allele designations for loci defined in sequence definition databases.

These two databases are independent but linked.  A single isolate database can
communicate with multiple sequence definition databases and vice versa.
Different access restrictions can be placed on different databases.

Databases are described in XML files telling BIGSdb everything it needs to know
about them. Isolate databases can have any fields defined for the isolate
table,allowing customisation of metadata - these fields are described in the
XML file (config.xml) and must match the fields defined in the database itself.

******************
Creating databases
******************
There are templates available for the sequence definition and isolate
databases.  These are SQL scripts found in the sql directory.

To create a database, you will need to log in as the postgres user and use
these templates.  For example to create a new sequence definition database
called bigsdb_test_seqdef, navigate to the sql directory and log in as the
postgres user, e.g. ::

 sudo su postgres

then ::

 createdb bigsdb_test_seqdef
 psql -f seqdef.sql bigsdb_test_seqdef

Create an isolate database the same way: ::
 
 createdb bigsdb_test_isolates
 psql -f isolatedb.sql bigsdb_test_isolates

The standard fields in the isolate table are limited to essential fields
required by the system.  To add new fields, you need to log in to the database
and alter this table.  For example, to add fields for country and year, first
log in to the newly created isolate database as the postgres user: ::

 psql bigsdb_test_isolates

and alter the isolate table: ::

 ALTER TABLE isolates ADD country text;
 ALTER TABLE isolates ADD year int;

Remember that any fields added to the table need to be described in the 
config.xml file for this database.

*******************************
Database-specific configuration
*******************************
Each BIGSdb database on a system has its own configuration directory, by
default in /etc/bigsdb/dbases. The database has a short configuration name
used to specify it in a web query and this matches the name of the
configuration sub-directory, e.g. 
http://pubmlst.org/cgi-bin/bigsdb/bigsdb.pl?db=pubmlst_neisseria_isolates
is the URL of the front page of the PubMLST Neisseria isolate database whose
configuration settings are stored in 
/etc/bigsdb/dbases/pubmlst_neisseria_isolates. This database sub-directory
contains a number of files (hyperlinks lead to the files used on the Neisseria
database):

* :download:`config.xml <conf/config.xml>` - the database configuration file.
  Fields defined here correspond to fields in the isolate table of the
  database.
* banner.html - optional file containing text that will appear as a banner
  within the database index pages. HTML markup can be used within this text.
* header.html - HTML markup that is inserted at the top of all pages. This can
  be used to set up site-specific menubars and logos.
* footer.html - HTML markup that is inserted at the bottom of all pages.
* curate_header.html - HTML markup that is inserted at the top of all curator's
  interface pages.
* curate_footer.html - HTML markup that is inserted at the bottom of all
  curator's interface pages.
* profile_submit.html - HTML markup for text that is inserted in to the 
  submission interface prior to profile submission finalization. This can be 
  used to add specific instructions such as the requirement to make an isolate
  submission.
* allele_submit.html - HTML markup for text that is inserted in to the
  submission interface prior to allele submission finalization. This can be
  used to add specific instructions such as the requirement to attach Sanger
  trace files.
  
The header and footer files can alternatively be placed in the root directory 
of the web site for site-wide use.

There are four additional files, site_header.html, site_footer.html, 
curate_site_header.html and curate_site_footer.html which are used when either
bigsdb.pl or bigscurate.pl are called without a database configuration. These
should be placed in the root directory of the web site.

You can also add HTML meta attributes (such as a favicon) by including a file
called meta.html in the database configuration directory. For example to set
a favicon this file can contain something like the following: ::

   <link rel="shortcut icon" href="/favicon.ico" type="image/ico" />
   
These attributes will appear in the <head> section of the HTML page.

.. _xml:

***********************************************
XML configuration attributes used in config.xml
***********************************************
The following lists describes the attributes used in the config.xml file that
is used to describe databases.

.. _isolate_xml:

Isolate database XML attributes
===============================
Please note that database structure described by the field and sample elements
must match the physical structure of the database isolate and sample tables
respectively.  Required attributes are in **bold**::
 
    <db>

Top level element. Contains child elements: system, field and sample.::
 
    <system>
    
Any value set here can be overridden in a 
:ref:`system.overrides file<system_overrides>`.
    
* **authentication**  

  * Method of authentication: either 'builtin' or 'apache'. 
    See :ref:`user authentication <user_authentication>`.   

* **db**	

  * Name of database on system.	

* **dbtype**	

  * Type of database: either 'isolates' or 'sequences'.

* **description**	

  * Description of database used throughout interface.
  
* align_limit

  * Overrides the sequence export record alignment limit in the Sequence
    Export plugin.  Default: '200'.
  
* all_plugins  

  * Enable all appropriate plugins for database: either 'yes' or 'no', default
    'no'.   
  
* annotation   

  * Semi-colon separated list of accession numbers with descriptions (separated
    by a \|), eg. 
    'AL157959|Z2491;AM421808|FAM18;NC_002946|FA 1090;NC_011035|NCCP11945;NC_014752|020-06'.
    Currently used only by Genome Comparator plugin.
    
* cache_schemes

  * Enable automatic refreshing of scheme field caches when batch adding new
    isolates: either 'yes' or 'no', default 'no'.
  * See :ref:`scheme caching<scheme_caching>`.
    
* codon_usage_limit

  * Overrides the record limit for the Codon Usage plugin.  Default: '500'.
  
* contig_analysis_limit

  * Overrides the isolate number limit for the Contig Export plugin.  Default: '1000'.
    
* curate_config

  * The database configuration that should be used for curation if different
    from the current configuration. This is used when the submission system is
    being used so that curation links in the 'Manage submissions' pages for
    curators load the correct database configuration.
    
* curate_link

  * URL to curator's interface, which can be relative or absolute. This will 
    be used to create a link in the public interface dropdown menu.
    
* curate_path_includes 

  * Partial path of the bigscurate.pl script used to curate the database.
    See user authentication.
    
* curate_script

  * Relative web path to curation script. Default ‘bigscurate.pl’
    (version 1.11+).
  * This is only needed if automated submissions are enabled. If bigscurate.pl
    is in a different directory from bigsdb.pl, you need to include the whole 
    web path, e.g. /cgi-bin/private/bigsdb/bigscurate.pl.
    
* curator_home

  * URL of curator's index page, which can be relative or absolute. This will
    be used to add a link in the dropdown menu.
    
* curators_only

  * Set to 'yes' to prevent ordinary authenticated users having access to
    database configuration. This is only effective if read_access is set to
    'authenticated_users'. This may be useful if you have different 
    configurations for curation and querying with some data hidden in the
    configuration used by standard users. Default 'no'.
    
* daily_pending_submissions

  * Overrides the daily limit on pending submissions that a user can submit
    via the web submission system. Default: '15'.

* daily_rest_submissions_limit

  * Overrides the limit on number of submissions that can be made to the 
    database via the RESTful interface. This is useful to prevent flooding of
    the submission system by aberrant scripts. Default: '100'. 
    
* default_access  

  * The default access to the database configuration, either 'allow' or 'deny'.
    If 'allow', then specific users can be denied access by creating a file
    called 'users.deny' containing usernames (one per line) in the
    configuration directory. If 'deny' then specific users can be allowed by
    creating a file called 'users.allow' containing usernames (one per line)
    in the configuration directory.  See
    :ref:`default access <default_access>`.
    
* default_private_records

  * The default number of private isolate records that a user can upload. The
    user account must have a status of either 'submitter', 'curator', or 
    'admin'. This value is used to set the private_quota field when creating a 
    new user record (which can be overridden for individual users). Changing it
    will not affect the quotas of existing users. Default: '0'.
    
* default_seqdef_config 

  * Isolate databases only: Name of the default seqdef database configuration
    used with this database. Used to automatically fill in details when adding
    new loci.
    
* default_seqdef_dbase  

  * Isolate databases only: Name of the default seqdef database used with this
    database. Used to automatically fill in details when adding new loci. 

* default_seqdef_script 

  * Isolate databases only: URL of BIGSdb script running the seqdef database
    (default: '/cgi-bin/bigsdb/bigsdb.pl').
    
* export_limit

  * Overrides the default allowed number of data points (isolates x columns) to
    export. Default: '25000000'. 
    
* fast_scan

  * Sets whether fast mode scanning is enabled via the web interface. This will
    scan all loci together, using exemplar sequences. In cases where multiple
    loci are being scanned this should be significantly faster than the 
    standard locus-by-locus scan, but it will take longer for the first results
    to appear. :ref:`Allele exemplars<defining_exemplars>` should be defined 
    if you enable this option. Set to 'yes' to enable.
    Default: 'no'.
  
* fieldgroup1 - fieldgroup10  

  * Allows multiple fields to be queried as a group. Value should be the name
    of the group followed by a colon (:) followed by a comma-separated list of
    fields to group, e.g. identifiers:id,strain,other_name.
    
* genome_comparator_limit

  * Overrides the isolate number limit for the Genome Comparator plugin.
    Default: '1000'.
    
* genome_comparator_max_ref_loci

  * Overrides the limit on number of loci allowed in a reference genome.
    Default: '10000'.
    
* genome_comparator_recommended_schemes

  * Comma-separated list of recommended schemes to suggest to Genome Comparator
    users. If lots of schemes are defined, a user may be tempted to click 'All
    loci' and this may not be the best option. Populating this attribute, 
    results in an additional list of preferred schemes that can be chosen.
    
* genome_comparator_threads

  * The number of threads to use for data gathering (BLAST, database
    queries) to populate data structure for Genome Comparator analysis. You
    should not set this to less than 2 as this will prevent job cancelling due
    to the way isolates are queued.
    Default: '2'.
    
* hide_unused_schemes   

  * Sets whether a scheme is shown in a main results table if none of the
    isolates on that page have any data for the specific scheme: either 'yes'
    or 'no', default 'no'.
    
* host   

  * Host name/IP address of machine hosting isolate database, default
    'localhost'. 
    
* job_priority 

  * Integer with default job priority for offline jobs (default:5).  

* job_quota 

  * Integer with number of offline jobs that can be queued or currently running
    for this database.
    
* labelfield   

  * Field that is used to describe record in isolate info page, default
    'isolate'.
    
* locus_aliases

  * Display locus aliases and use them in dropdown lists by default: must be
    either 'yes' or 'no', default 'no'. This option can be overridden by a user
    preference.   
    
* locus_superscript_prefix 

  * Superscript the first letter of a locus name if it is immediately following
    by an underscore, e.g. f_abcZ would be displayed as fabcZ within the
    interface: must be either 'yes' or 'no', default 'no'. This can be used to
    designate gene fragments (or any other meaning you like). 
  
* maindisplay_aliases   

  * Default setting for whether isolates aliases are displayed in main results
    tables: either 'yes' or 'no', default 'no'. This setting can be overridden
    by individual user preferences. 

* noshow 

  * Comma-separated list of fields not to use in breakdown statistic plugins.
  
* no_publication_filter  

  * Isolate databases only: Switches off display of publication filter in
    isolate query form by default: either 'yes' or 'no', default 'no'.
  
* only_sets

  * Don't allow option to view the 'whole database' - only list sets that have
    been defined: either 'yes' or 'no', default 'no'.  
  
* password  

  * Password for access to isolates database, default 'remote'. 
   
* port   

  * Port number that the isolate host is listening on, default '5432'.
  
* privacy   

  * Displays E-mail address for sender in isolate information page if set to
    'no'. Default 'yes'.
    
* public_login

  * Optionally allow users to log in to a public database - this is useful as
    any jobs will be associated with the user and their preferences will also
    be linked to the account. Set to 'no' to disable. Default 'yes'.
    
* query_script

  * Relative web path to bigsdb script. Default ‘bigsdb.pl’ (version 1.11+).
  * This is only needed if automated submissions are enabled. If bigsdb.pl is
    in a different directory from bigscurate.pl, you need to include the whole
    web path, e.g. /cgi-bin/bigsdb/bigsdb.pl.
  
* read_access  

  * Describes who can view data: either 'public' for everybody or 
    'authenticated_users' for anybody who has been able to log in. 
    Default 'public'.  
    
* related_databases

  * Semi-colon separated list of links to related BIGSdb databases on the
    system. This should be in the form of database configuration name followed
    by a '|' and the description, e.g. 
    'pubmlst_neisseria_seqdef|Sequence and profile definitions'.
    This is used to populate the dropdown menu.
    
* remote_contigs

  * Optionally allow the use of remote contigs. These are stored in a remote
    BIGSdb database, accessible via the RESTful API. Set to 'yes' to enable.

* script_path_includes  

  * Partial path of the bigsdb.pl script used to access the database.
    See :ref:`user authentication <user_authentication>`.
    
* seqbin_size_threshold

  * Sets the size values in Mbp to enable for the 
    :ref:`seqbin filter <seqbin_filter>`.
  * Example: seqbin_size_threshold="0.5,1,2,4".
  
* seq_export_limit

  * Overrides the sequence export limit (records x loci) in the Sequence
    Export plugin.  Default: '1000000'.
    
* sets   

  * Use :ref:`sets <sets>`: either 'yes' or 'no', default 'no'.  
  
* set_id 

  * Force the use of a specific set when accessing database via this XML
    configuration: Value is the name of the set. 
    
* start_id

  * Defines the minimum record id to be used when uploading new isolate 
    records. This can be useful when it is anticipated that two databases may
    be merged and it would be easier to do so if the id numbers in the two
    databases were different.  Default: '1'.
    
* submissions

  * Enable automated submission system: either 'yes' or 'no', default 'no'
    (version 1.11+).
  * The curate_script and query_script paths should also be set, either in
    the bigsdb.conf file (for site-wide configuration) or within the system
    attribute of config.xml.
    
* submissions_deleted_days

  * Overrides the default number of days before closed submissions are deleted
    from the system. Default: '90'. 
    
* tblastx_tagging 

  * Sets whether tagging can be performed using TBLASTX: either 'yes' or 'no',
    default 'no'.
    
* total_pending_submissions

  * Overrides the total limit on pending submissions that a user can submit
    via the web submission system. Default: '20'.
    
* user   

  * Username for access to isolates database, default 'apache'.
  
* user_job_quota 

  * Integer with number of offline jobs that can be queued or currently running
    for this database by any specific user - this parameter is only effective
    if users have to log in.
    
* user_projects

  * Sets whether authenticated users can create their own projects in order
    to group isolates: either 'yes' or 'no', default 'no'.
      
* view

  * Database view containing isolate data, default 'isolates'.
  
* views   

  * Comma-separated list of views of the isolate table defined in the database.
    This is used to set a view for a set.   
 
* webroot	

  * URL of web root, which can be relative or absolute. This is used to provide
    a hyperlinked item in the dropdown menu. Default '/'.

.. _isolate_xml_field:

::

 <field>

Element content: Field name + optional list <optlist> of allowed values, e.g.::

  <field type="text" required="no" length="40" maindisplay="no"
     web="http://somewebsite.com/cgi-bin/script.pl?id=[?]" optlist="yes">epidemiology
    <optlist>
     <option>carrier</option>
     <option>healthy contact</option>
     <option>sporadic case</option>
     <option>endemic</option>
     <option>epidemic</option>
     <option>pandemic</option>
    </optlist>
  </field>

* **type**	

  * Data type: int, text, float, bool, or date.
  
* comments  
  * optional

  * Comments about the field.  These will be displayed in the field description
    plugin and as tooltips within the curation interface.
    
* curate_only

  * Set to 'yes' to hide field on an isolate information page in the standard
    interface.  The field will be visible if the page is accessed via the 
    curator's interface (version 1.10.0+).
    
* default

  * Default value.  This will be entered automatically in the web form but can
    be overridden.
  
* dropdown  

  * Select if you want this field to have its own dropdown filter box on the
    query page. If the field has an option list it will use the values in it,
    otherwise all values defined in the database will be included: 'yes' or
    'no', default 'no'. This setting can be overridden by individual user
    preferences. 
  
* length 

  * Length of field, default 12.  
  
* maindisplay  

  * Sets if field is displayed in the main table after a database search, 'yes'
    or 'no', default 'yes'. This setting can be overridden by individual user
    preferences. 
  
* max 

  * Maximum value for integer and date types. Special values such as 
    CURRENT_YEAR and CURRENT_DATE can be used.

* min	

  * Minimum value for integer and date types.
  
* no_curate

  * Setting this will hide the field in the curator interface and prevent it
    from being manually modified. This is useful for fields that are populated
    by automated scripts or database triggers. Can be 'yes' or 'no', default
    'no'.
  
* optlist   

  * Sets if this field has a list of allowed values, default 'no'. Surround
    each option with an <option> tag. 
    
* regex  

  * Regular expression used to constrain field values, e.g. regex="^[A-Z].*$"
    forces the first letter of the value to be capitalized.  

* required	

  * Sets if data is required for this field, 'yes' or 'no', default 'yes'.	
  
* userfield

  * Select if you want this field to have its own dropdown filter box of users
    (populated from the users table): 'yes' or 'no', default 'no'.
 
* web	

  * URL that will be used to hyperlink field values. If [?] is included in the
    URL, this will be substituted for the actual field value.	
 
Special values
--------------
The following special variables can be used in place of an actual value:

* CURRENT_DATE: current date in yyyy-mm-dd format
* CURRENT_YEAR: the 4 digit value of the current year

::

 <sample>

Element content: Sample field name + optional list <optlist> of allowed values.
Attributes are essentially the same as isolate field attributes, but refer to
the samples table rather than the isolates table.

The sample table, if defined, must include isolate_id and sample_id fields,
which must also be described in the XML file. These must be set as integer
fields.

.. _seqdef_xml:

Sequence definition database XML attributes
===========================================

Required attributes are in **bold**.

::

 <db>

Top level element. Contains child elements: system, field and sample.

::

 <system>
 
Any value set here can be overridden in a 
:ref:`system.overrides file<system_overrides>`.

* **authentication**  

  * Method of authentication: either 'builtin' or 'apache'. See 
    :ref:`user authentication <user_authentication>`.   

* **db**

  * Name of database on system.	

* **dbtype**	

  * Type of database: either 'isolates' or 'sequences'.	

* **description**	

  * Description of database used throughout interface.
  
* align_limit

  * Overrides the sequence export record alignment limit in the Sequence
    Export plugin.  Default: '200'.

* allele_comments

  * Enable comments on allele sequences: either 'yes' or 'no', default 'no'.
  * This is not enabled by default to discourage the practice of adding isolate
    information to allele definitions (this sort of information belongs in an
    isolate database).
  
* allele_flags

  * Enable flags to be set for alleles: either 'yes' or 'no', default 'no'.
  
* curate_config

  * The database configuration that should be used for curation if different
    from the current configuration. This is used when the submission system is
    being used so that curation links in the 'Manage submissions' pages for
    curators load the correct database configuration.
  
* curate_path_includes  

  * Partial path of the bigscurate.pl script used to curate the database. See
    :ref:`user authentication <user_authentication>`.
    
* curate_script

  * Relative web path to curation script.  Default 'bigscurate.pl' (version 
    1.11+).
  * This is only needed if automated submissions are enabled.  If bigscurate.pl
    is in a different directory from bigsdb.pl, you need to include the whole 
    web path, e.g. /cgi-bin/private/bigsdb/bigscurate.pl.
    
* curator_home

  * URL of curator's index page, which can be relative or absolute. This will
    be used to add a link in the dropdown menu.
    
* curators_only

  * Set to 'yes' to prevent ordinary authenticated users having access to
    database configuration. This is only effective if read_access is set to
    'authenticated_users'. This may be useful if you have different 
    configurations for curation and querying with some data hidden in the
    configuration used by standard users. Default 'no'.
    
* daily_pending_submissions

  * Overrides the daily limit on pending submissions that a user can submit
    via the web submission system. Default: '15'.
    
* daily_rest_submissions_limit

  * Overrides the limit on number of submissions that can be made to the 
    database via the RESTful interface. This is useful to prevent flooding of
    the submission system by aberrant scripts. Default: '100'. 
    
* diploid

  * Allow IUPAC 2-nuclotide ambiguity codes in allele definitions for use with
    diploid typing schemes: either 'yes' or 'no', default 'no'.
    
* disable_seq_downloads
   
  * Prevent users or curators from downloading all alleles for a locus (admins
    always can). 'yes' or 'no', default 'no'.
    
* exemplars

  * Use exemplar sequences in the BLAST caches used for the sequence query
    pages. This is useful on larger databases as it speeds up the query 
    significantly. :ref:`Exemplar alleles<defining_exemplars>` *MUST* be 
    defined otherwise sequence queries will fail. 'yes' or 'no', default 'no'.
    
* isolate_database

  * The config name of the isolate database. This is used to provide a link to
    isolate submissions. You also need to set isolate_submissions="yes".
    
* isolate_submissions

  * Set to yes to provide a link to isolate submissions. The isolate_database
    attribute also needs to be set. Default: 'no'.
    
* job_priority 

  * Integer with default job priority for offline jobs (default:5).   

* job_quota 

  * Integer with number of offline jobs that can be queued or currently running
    for this database.
    
* profile_submissions

  * Enable profile submissions (automated submission system): either 'yes' 
    or 'no', default 'no' (version 1.11+).
  * To enable, you will also need to set submissions="yes".  By default, 
    profile submissions are disabled since generally new profiles should be
    accompanied by representative isolate data, and the profile can be 
    extracted from that. 
    
* public_login

  * Optionally allow users to log in to a public database - this is useful as
    any jobs will be associated with the user and their preferences will also
    be linked to the account. Set to 'no' to disable. Default 'yes'.
  
* query_script

  * Relative web path to bigsdb script.  Default 'bigsdb.pl' (version 1.11+).
  * This is only needed if automated submissions are enabled.  If bigsdb.pl is
    in a different directory from bigscurate.pl, you need to include the whole 
    web path, e.g. /cgi-bin/bigsdb/bigsdb.pl.  
     
* read_access  

  * Describes who can view data: either 'public' for everybody, or
    'authenticated_users' for anybody who has been able to log in. Default
    'public'.   
    
* related_databases

  * Semi-colon separated list of links to related BIGSdb databases on the
    system. This should be in the form of database configuration name followed
    by a '|' and the description, e.g. 
    'pubmlst_neisseria_isolates|Isolates'.
    This is used to populate the dropdown menu.
 
* script_path_includes  

  * Partial path of the bigsdb.pl script used to access the database. See
    :ref:`user authentication <user_authentication>`.
    
* seq_export_limit

  * Overrides the sequence export limit (records x loci) in the Sequence
    Export plugin.  Default: '1000000'.
    
* sets

  * Use :ref:`sets <sets>`: either 'yes' or 'no', default 'no'.
  
* set_id

  * Force the use of a specific set when accessing database via this XML
    configuration: Value is the name of the set.
    
* submissions

  * Enable automated submission system: either 'yes' or 'no', default 'no' 
    (version 1.11+).
  * The curate_script and query_script paths should also be set, either in
    the bigsdb.conf file (for site-wide configuration) or within the system
    attribute of config.xml.
    
* submissions_deleted_days

  * Overrides the default number of days before closed submissions are deleted
    from the system. Default: '90'. 
    
* total_pending_submissions

  * Overrides the total limit on pending submissions that a user can submit
    via the web submission system. Default: '20'.
    
* user_job_quota 

  * Integer with number of offline jobs that can be queued or currently running
    for this database by any specific user - this parameter is only effective 
    if users have to log in.

* webroot	

  * URL of web root, which can be relative or absolute. This is used to provide
    a hyperlinked item in the dropdown menu. Default '/'.

**********************************************
Over-riding global defaults set in bigsdb.conf
**********************************************
Certain values set in bigsdb.conf can be over-ridden by corresponding values
set in a database-specific config.xml file. These can be set within the system
tag like other attributes:

 * query_script
 
   * Relative web path to bigsdb script.
 
 * curate_script
 
   * Relative web path to curation script.
   
 * prefs_db
 
   * The name of the preferences database.
   
 * auth_db
 
   * The name of the authentication database.
   
 * tmp_dir
 
   * Path to the web-accessible temporary directory.
   
 * secure_tmp_dir
 
   * Path to the web-inaccessible (secure) temporary directory.
   
 * ref_db
 
   * The name of the references database.

.. _system_overrides:
    
************************************
Over-riding values set in config.xml
************************************
Any attribute used in the system tag of the database config.xml file can be
over-ridden using a file called system.overrides, placed in the same directory
as config.xml. This is very useful as it allows you to set up multiple configs
for a database, with the config.xml files symlinked so that any changes to one
will be seen in each database configuration. An example of why you may wish to
do this would be if you create separate public and private views of the 
isolate table that filters on some attribute. The system.overrides file uses
key value pairs separated by = with the values quoted, e.g. :: 

   view="private"
   read_access="authenticated_users"
   description="Private view of database"
  
.. _user_authentication:

*******************
User authentication
*******************
You can choose whether to allow Apache to handle your authentication or use
built-in authentication.

Apache authentication
=====================
Using apache to provide your authentication allows a flexible range of methods
and back-ends (see the 
`Apache authentication HowTo <http://httpd.apache.org/docs/2.2/howto/auth.html>`_ 
for a start, or any number of tutorials on the web).

At its simplest, use a .htaccess file in the directory containing the
bigscurate.pl (and bigsdb.pl for restriction of read-access) script or by
equivalent protection of the directory in the main Apache server configuration.
It is important to note however that, by default, any BIGSdb database can be
accessed by any instance of the BIGSdb script (including one which may not be
protected by a .htaccess file, allowing public access). To ensure that only a
particular instance (protected by a specific htaccess directive) can access
the database, the following attributes can be set in the system tag of the
database XML description file:

* script_path_includes: the BIGSdb script path must contain the value set.
* curate_path_includes: the BIGSdb curation script path must contain the value
  set.

For public databases, the 'script_path_includes' attribute need not be set.

To use apache authentication you need to set the authentication attribute in
the system tag of the database XML configuration to 'apache'.

Built-in authentication
=======================
BIGSdb has its own built-in authentication, using a separate database to store
password and session hashes. The advantages of using this over many forms of
apache authentication are:

* Users are able to update their own passwords.
* Passwords are not transmitted over the Internet in plain text.

When a user logs in, the server provides a random one-time session variable
and the user is prompted to enter their username and password. The password
is encrypted within the browser using a Javscript one-way hash algorithm, and
this is combined with the session variable and hashed again. This hash is
passed to the server. The server compares this hash with its own calculated
hash of the stored encrypted password and session variable that it originally
sent to the browser. Implementation is based on
`perl-md5-login <http://perl-md5-login.sourceforge.net/>`_.

To use built-in authentication you need to set the authentication attribute in
the system tag of the database XML configuration to 'builtin'.

.. _setup_admin_user:

*************************
Setting up the admin user
*************************
The first admin user needs to be manually added to the users table of the
database. Connect to the database using psql and add the following (changing
details to suit the user).::

 INSERT INTO users (id, user_name, surname, first_name, email, affiliation, status, date_entered,
 datestamp, curator) VALUES (1, 'keith', 'Jolley', 'Keith', 'keith.jolley@zoo.ox.ac.uk', 
 'University of Oxford, UK', 'admin', 'now', 'now', 1);

If you are using built-in authentication, set the password for this user using
the :ref:`add_user.pl <set_first_password>` script. This hashes the password
and stores this within the authentication database.  Other users can
be added by the admin user from the curation interface accessible from
http://your_website/cgi-bin/private/bigscurate.pl?db=test_db (or wherever you
have located your bigscurate.pl script).

.. _updating_citations:

*************************
Updating PubMed citations
*************************
Publications listed in PubMed can be associated with individual isolate
records, profiles, loci and sequences.  Full citations for these are stored
within a local reference database, enabling these to be displayed within
isolate records and searching by publication and author.  This local database
is populated by a script that looks in BIGSdb databases for PubMed records not
locally stored and then requests the full citation record from the PubMed
database.

The script is called get_refs.pl and can be found in the scripts/maintenance
directory.  This script needs to know which BIGSdb databases and tables it
needs to search for PubMed ids.  These are listed in a configuration file
(usually called getrefs.conf) which contains two columns - the first is the
name of the database, the second is a comma-separated list of tables to search,
e.g. ::

  pubmlst_bigsdb_neisseria_isolates          refs
  pubmlst_bigsdb_neisseria_seqdef            profile_refs,sequence_refs,locus_refs

The script can be called as follows: ::

 get_refs.pl getrefs.conf
 
Run either as the 'postgres' user or an account that is allowed to connect as
the postgres user.

This should be run periodically from a CRON job, e.g. every hour.

.. _accessing_remote_contigs:

************************************
Configuring access to remote contigs
************************************
It is possible for isolate records to have contigs in an external BIGSdb 
database. These must be accessible via the :ref:`RESTful API<restful_api>`. 
The advantage of this is that it enables multiple isolate databases to use the
same genome assemblies without having to duplicate the storage of those 
assemblies. If access to the external database requires authenticated access,
OAuth settings can be set to enable contig retrieval.

To enable remote contigs, set the remote_contigs attribute in the 
:ref:`<system><isolate_xml>` tag of config.xml, i.e. ::

 remote_contigs = "yes"
 
.. _oauth_remote_contigs:
  
Setting up authentication
=========================
A client key for the BIGSdb remote contig manager needs to be generated. This
can be done using the 
:ref:`create_client_credentials.pl<create_client_credentials>` script, e.g. ::

 create_client_credentials.pl --a 'BIGSdb remote contig manager' --insert
 
This will generate a client id (key) and a client secret and add them to the
authentication database. 

You will then need to obtain an access token and access secret using the client
key and secret with the get_oauth_access_token.pl script. You will need to
enter the API database URI (e.g. 
http://rest.pubmlst.org/db/pubmlst_rmlst_isolates) and the web database URL 
(e.g. https://pubmlst.org/bigsdb?db=pubmlst_rmlst_isolates). You will then be
prompted to follow a link and log in to the database with your user 
credentials. A verification code will be generated. You need to enter this in
to the script when prompted. An access token and secret will be returned to 
you.

From the curators' page, click the oauth credentials add link in the 
administrator settings. This function is normally hidden, so you may need to 
click the 'Show all' toggle to display it.

.. image:: /images/dbase_setup/oauth.png

Populate the OAuth_credentials table with the client key/secret and access
token/secret. You should also enter the root REST URI for the database 
(e.g. http://rest.pubmlst.org/db/pubmlst_rmlst_isolates). 

.. image:: /images/dbase_setup/oauth2.png

.. _processing_remote_contigs:

Processing remote contigs
=========================
When remote contigs are first linked to a record, the sequences are downloaded
in bulk (without their metadata). This allows the sequence lengths to be 
recorded as this is needed for various queries and outputs. The curator is then
given an option to process the contigs, which involves downloading each contig 
individually to record metadata including the original designation and the 
sequence platform used. This may take a while so it may be preferable to
perform this task offline. This can be done using the process_remote_contigs.pl
script found in the scripts/automation directory. Options for using this script
are shown below: ::

   remote_contigs.pl --help
   NAME
       process_remote_contigs.pl
       Download, check length and create checksum contigs stored as URIs
   
   SYNOPSIS
       process_remote_contigs.pl --database NAME [options]
   
   OPTIONS
              
   --database NAME
       Database configuration name.
       
   --exclude_isolates LIST
       Comma-separated list of isolate ids to ignore.
       
   --exclude_projects LIST
       Comma-separated list of projects whose isolates will be excluded.
       
   --help
       This help page.
       
   --isolates LIST  
       Comma-separated list of isolate ids to scan (ignored if -p used).
       
   --isolate_list_file FILE  
       File containing list of isolate ids (ignored if -i or -p used).
       
   --min ID
       Minimum isolate id.
   
   --max ID
       Maximum isolate id.
              
   --projects LIST
       Comma-separated list of project isolates to scan.
       
   --quiet
       Only display errors.


 