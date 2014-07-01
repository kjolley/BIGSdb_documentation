########################################
Installation and configuration of BIGSdb
########################################

Software installation
=====================
BIGSdb consists of two main Perl scripts, bigsdb.pl and bigscurate.pl, that run the query and curator's interfaces respectively. These need to be located somewhere within the web cgi-bin directories. In addition, there are a large number of library files, used by both these scripts, that are installed by default in /usr/local/lib/BIGSdb. Plugin scripts are stored within a 'Plugins' sub-directory of this library directory.

All databases on a system can use the same instance of the scripts, or alternatively any database can specify a particular path for each script, enabling these script directories to be protected by apache htaccess directives.

 * Software requirements
 * Download from `SourceForge.net <http://sourceforge.net/projects/bigsdb/>`_ or `GitHub <https://github.com/kjolley/BIGSdb>`_.

1. Unpack the distribution package in a temporary directory: ::

    gunzip bigsdb_1.x.x.tar.gz
    tar xvf bigsdb_1.x.x.tar

2. Copy the bigsdb.pl and bigscurate.pl scripts to a subdirectory of your web server's cgi-bin directory. Make sure these are readable and executable by the web server daemon.
3. Copy the contents of the lib directory to /usr/local/lib/BIGSdb/. Make sure you include the Plugins and Offline directories which are subdirectories of the main lib directory.
4. Copy the contents of the javascript directory to a javascript directory within the web root tree, i.e. accessible from http://your_website/javascript/.
5. Copy the bigsdb.css stylesheet to the root directory of your website, i.e. accessible from http://your_website/bigsdb.css.
6. Copy the images directory to the root directory of your website, i.e. accessible from http://your_website/images.
7. Copy the contents of the conf directory to /etc/bigsdb/. Check the paths of helper applications and database names in the bigsdb.conf file and modify for your system.
8. Create a PostgreSQL database user called apache - this should not have any special priveleges. Use the createuser command to do this, e.g. ::

    createuser apache

   From the psql command line, set the apache user password: ::

     psql
     ALTER ROLE apache WITH PASSWORD 'remote';

9. Create PostgreSQL databases called bigsdb_auth, bigsdb_prefs and refs using the scripts in the sql directory. Create the database using the createdb command and set up the tables using the psql command, e.g. ::

     createdb bigsdb_auth
     psql -f auth.sql bigsdb_auth

10. Create a writable temporary directory in the root of the web site called tmp, i.e. accessible from http://your_website/tmp.
11. Create a log file, bigsdb.log, in /var/log owned by the web server daemon, e.g. ::

     touch /var/log/bigsdb.log
     chown www-data /var/log/bigsdb.log

 (substitute www-data for the web daemon user).

Site-specific configuration
===========================
Site-specific configuration files are located in /etc/bigsdb by default.

* :download:`bigsdb.conf <conf/bigsdb.conf>` - main configuration file
* :download:`logging.conf <conf/logging.conf>` - error logging settings. See log4perl project website for advanced configuration details.

Database-specific configuration
===============================
Details for creating the databases can be found in the software distribution package.

Each BIGSdb database on a system has its own configuration directory, by default in /etc/bigsdb/dbases. The database has a short configuration name used to specify it in a web query and this matches the name of the configuration sub-directory, e.g. http://pubmlst.org/cgi-bin/bigsdb/bigsdb.pl?db=pubmlst_neisseria_isolates is the URL of the front page of the PubMLST Neisseria isolate database whose configuration settings are stored in /etc/bigsdb/dbases/pubmlst_neisseria_isolates. This database sub-directory contains a number of files (hyperlinks lead to the files used on the Neisseria database):

* :download:`config.xml <conf/config.xml>` - the database configuration file. Fields defined here correspond to fields in the isolate table of the database.
* banner.html - optional file containing text that will appear as a banner within the database index pages. HTML markup can be used within this text.
* header.html - HTML markup that is inserted at the top of all pages. This can be used to set up site-specific menubars and logos.
* footer.html - HTML markup that is inserted at the bottom of all pages.
* curate_header.html - HTML markup that is inserted at the top of all curator's interface pages.
* curate_footer.html - HTML markup that is inserted at the bottom of all curator's interface pages.

User authentication
===================
You can choose whether to allow Apache to handle your authentication or use built-in authentication.

Apache authentication
---------------------
Using apache to provide your authentication allows a flexible range of methods and back-ends (see the Apache authentication HowTo for a start, or any number of tutorials on the web).

At its simplest, use a .htaccess file in the directory containing the bigscurate.pl (and bigsdb.pl for restriction of read-access) script or by equivalent protection of the directory in the main Apache server configuration. It is important to note however that, by default, any BIGSdb database can be accessed by any instance of the BIGSdb script (including one which may not be protected by a .htaccess file, allowing public access). To ensure that only a particular instance (protected by a specific htaccess directive) can access the database, the following attributes can be set in the system tag of the database XML description file:

* script_path_includes: the BIGSdb script path must contain the value set.
* curate_path_includes: the BIGSdb curation script path must contain the value set.

For public databases, the 'script_path_includes' attribute need not be set.

To use apache authentication you need to set the authentication attribute in the system tag of the database XML configuration to 'apache'.

Built-in authentication
-----------------------
BIGSdb has its own built-in authentication, using a separate database to store password and session hashes. The advantages of using this over many forms of apache authentication are:

* Users are able to update their own passwords.
* Passwords are not transmitted over the Internet in plain text.

When a user logs in, the server provides a random one-time session variable and the user is prompted to enter their username and password. The password is encrypted within the browser using a Javscript one-way hash algorithm, and this is combined with the session variable and hashed again. This hash is passed to the server. The server compares this hash with its own calculated hash of the stored encrypted password and session variable that it originally sent to the browser. Implementation is based on `perl-md5-login <http://perl-md5-login.sourceforge.net/>`_.

To use built-in authentication you need to set the authentication attribute in the system tag of the database XML configuration to 'builtin'.

XML configuration attributes used in config.xml
===============================================
The following lists describes the attributes used in the config.xml file that is used to describe databases.

Isolate database XML attributes
-------------------------------
Please note that database structure described by the field and sample elements must match the physical structure of the database isolate and sample tables respectively.::
 
    <db>

Top level element. Contains child elements: system, field and sample.::
 
    <system>
    
* db	

  * name of database on system	
  * required

* dbtype	

  * type of database: either 'isolates' or 'sequences'
  * required

* description	

  * Description of database used throughout interface
  * required

* authentication	

  * method of authentication: either 'builtin' or 'apache'. See user authentication. 	
  * required

* webroot	

  * URL of web root, which can be relative or absolute. The bigsdb.css stylesheet file should be located in this directory. Default '/'.
  * optional

* view

  * database view containing isolate data, default 'isolates'
  * optional

* script_path_includes	

  * partial path of the bigsdb.pl script used to access the database. See user authentication.	
  * optional

* curate_path_includes	

  * partial path of the bigscurate.pl script used to curate the database. See user authentication.	
  * optional

* noshow	

  * comma-separated list of fields not to use in breakdown statistic plugins	
  * optional

* fieldgroup1 - fieldgroup10	

  * allows multiple fields to be queried as a group. Value should be the name of the group followed by a colon (:) followed by a comma-separated list of fields to group, e.g. identifiers:id,strain,other_name	
  * optional

* maindisplay_aliases	

  * default setting for whether isolates aliases are displayed in main results tables: either 'yes' or 'no', default 'no'. This setting can be overridden by individual user preferences.	
  * optional

* read_access	

  * describes who can view data: either 'public' for everybody, 'authenticated_users' for anybody who has been able to log in, or 'acl' (access control list) for fine-grained access control to individual isolate records. Default 'public'.	
  * optional

* write_access	

  * describes who can curate isolate records: either 'acl' (access control list) for fine-grained access control to individual isolate records, or leave empty for anybody with curator permission to alter isolate records.	
  * optional

* locus_superscript_prefix	

  * superscript the first letter of a locus name if it is immediately following by an underscore, e.g. f_abcZ would be displayed as fabcZ within the interface: must be either 'yes' or 'no', default 'no'. This can be used to designate gene fragments (or any other meaning you like).	
  * optional

* hide_unused_schemes	

  * sets whether a scheme is shown in a main results table if none of the isolates on that page have any data for the specific scheme: either 'yes' or 'no', default 'no'.
  * optional

* use_temp_scheme_table	

  * sets whether entire schemes are imported in to the isolate database in to an indexed table rather than querying the seqdef scheme view for isolate results tables. Under some circumstances this can be considerably quicker than querying the seqdef scheme view (a few ms compared to >10s if the seqdef database contains multiple schemes with an uneven distribution of a large number of profiles so that the Postgres query planner picks a sequential rather than index scan). This scheme table can also be generated periodically using the update_scheme_cache.pl script to create a persistent cache. This is particularly useful for large schemes (>10000 profiles) but data will only be as fresh as the cache so ensure that the update script is run periodically. 	
  * optional

* labelfield	

  * field that is used to describe record in isolate info page, default 'isolate'	
  * optional

* tblastx_tagging	

  * sets whether tagging can be performed using TBLASTX: either 'yes' or 'no', default 'no'.	
  * optional

* host	

  * host name/IP address of machine hosting isolate database, default 'localhost'	
  * optional

* port	

  * port number that the isolate host is listening on, default '5432'	
  * optional

* user	

  * username for access to isolates database, default 'apache'	
  * optional

* password	

  * password for access to isolates database, default 'remote'	
  * optional

* privacy	

  * displays E-mail address for sender in isolate information page if set to 'no'. Default 'yes'.	
  * optional

* annotation	

  * semi-colon separated list of accession numbers with descriptions (separated by a |), eg. 'AL157959|Z2491;AM421808|FAM18;NC_002946|FA 1090;NC_011035|NCCP11945;NC_014752|020-06'. Currently used only by Genome Comparator plugin	
  * optional

* sets	

  * use sets: either 'yes' or 'no', default 'no'.	
  * optional

* set_id	

  * Force the use of a specific set when accessing database via this XML configuration: Value is the name of the set.	
  * optional

* only_sets

  * when defined, don't allow option to view the 'whole database' - only list sets that have been defined: either 'yes' or 'no', default 'no'.	
  * optional

* views	

  * comma-separated list of views of the isolate table defined in the database. This is used to set a view for a set.	
  * optional

* all_plugins	

  * enable all appropriate plugins for database: either 'yes' or 'no', default 'no'.	
  * optional

* job_priority	

  * Isolate databases only: Integer with default job priority for offline jobs (default:5) (Version v1.7+)	
  * optional

* dbase_job_quota	

  * isolate databases only:Integer with number of offline jobs that can be queued or currently running for this database (Version 1.7+)	
  * optional

* default_seqdef_config	

  * isolate databases only: Name of the default seqdef database configuration used with this database. Used to automatically fill in details when adding new loci. (Version 1.7+)	
  * optional

* default_seqdef_dbase	

  * isolate databases only: Name of the default seqdef database used with this database. Used to automatically fill in details when adding new loci. (Version 1.7+)	
  * optional

* default_seqdef_script	

  * isolate databases only: URL of BIGSdb script running the seqdef database (default: '/cgi-bin/bigsdb/bigsdb.pl'). (Version 1.7+)	
  * optional

* default_access	

  * the default access to the database configuration, either 'allow' or 'deny'. If 'allow', then specific users can be denied access by creating a file called 'users.deny' containing usernames (one per line) in the configuration directory. If 'deny' then specific users can be allowed by creating a file called 'users.allow' containing usernames (one per line) in the configuration directory. (Version 1.7+)	
  * optional

* no_publication_filter	
  * isolate databases only: Switches off display of publication filter in isolate query form by default: either 'yes' or 'no', default 'no'. (Version 1.8+)	
  * optional

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

* type	

  * data type: int, text, float or date	
  * required

* min	

  * minimum value for integer types.(introduced in v1.7)	
  * optional

* max	

  * maximum value for integer types. Special values such as CURRENT_YEAR can be used. (introduced in v1.7)	
  * optional

* required	

  * is data required for this field? 'yes' or 'no', default 'yes'	
  * optional

* maindisplay	

  * is field displayed in main table after database search? 'yes' or 'no', default 'yes'. This setting can be * overridden by individual user preferences.	
  * optional

* length	

  * length of field, default 12	
  * optional

* optlist	

  * does this field have a list of allowed values? default 'no'. Surround each option with an <option> tag	
  * optional

* dropdown	

  * select if you want this field to have its own dropdown box on the query page. If the field has an option list it will use the values in it, otherwise all values defined in the database will be included: 'yes' or 'no', default 'no'. This setting can be overridden by individual user preferences.	
  * optional

* comments	

  * comments about the field	
  * optional

* web	

  * URL that will be used to hyperlink field values. If [?] is included in the URL, this will be substituted for the actual field value.	
  * optional

* regex	

  * regular expression used to constrain field values, e.g. regex="^[A-Z].*$" forces the first letter of the value to be capitalized.	
  * optional

Special values
--------------
The following special variables can be used in place of an actual value:

* CURRENT_YEAR: the 4 digit value of the current year
::

 <sample>

Element content: Sample field name + optional list <optlist> of allowed values. Attributes are essentially the same as isolate field attributes, but refer to the samples table rather than the isolates table.

The sample table, if defined, must include isolate_id and sample_id fields, which must also be described in the XML file. These must be set as integer fields.

Sequence definition database XML attributes
-------------------------------------------
::

 <db>

Top level element. Contains child elements: system, field and sample.
::

 <system>
* db

  * name of database on system	
  * required

* dbtype	

  * type of database: either 'isolates' or 'sequences'	
  * required

* description	

  * description of database used throughout interface	
  * required

* authentication	

  * method of authentication: either 'builtin' or 'apache'. See user authentication. 	
  * required

* webroot	

  * URL of web root, which can be relative or absolute. The bigsdb.css stylesheet file should be located in this directory. Default '/'	
  * optional

* script_path_includes	

  * partial path of the bigsdb.pl script used to access the database. See user authentication.	
  * optional

* curate_path_includes	

  * partial path of the bigscurate.pl script used to curate the database. See user authentication.	
  * optional

* read_access	

  * describes who can view data: either 'public' for everybody, or 'authenticated_users' for anybody who has been able to log in. Default 'public'.	
  * optional

* disable_seq_downloads
	
  * prevent users or curators from downloading all alleles for a locus (admins always can). 'yes' or 'no', default 'no'.	  * optional
	
Setting up the admin user
=========================
The first admin user needs to be manually added to the users table of the database. Connect to the database using psql and add the following (changing details to suit the user).::

 INSERT INTO users (id,user_name,surname,first_name,email,affiliation,status,date_entered,datestamp,curator) VALUES (1,'keith','Jolley','Keith','keith.jolley@zoo.ox.ac.uk','University of Oxford, UK','admin','today','today',1);

If you are using built-in authentication, set the password for this user using the add_user.pl script. Other users can be added by the admin user from the curation interface accessible from http://your_website/cgi-bin/private/bigscurate.pl?db=test_db (or wherever you have located your bigscurate.pl script).

Setting up the offline job manager
==================================
To run plugins that require a long time to complete their analyses, an offline job manager has been developed. The plugin will save the parameters of a job to a job database and then provide a link to the job status page. An offline script, run frequently from CRON, will then process the job queue and update status and outputs via the job status page.

1. Create a 'bigsdb' UNIX user, e.g.::

    sudo useradd -s /bin/sh bigsdb

2. As the postgres user, create a 'bigsdb' user and create a bigsdb_jobs database using the jobs.sql SQL file, e.g.::

    createuser bigsdb [no need for special priveleges]
    createdb bigsdb_jobs
    psql -f jobs.sql bigsdb_jobs

   From the psql command line, set the bigsdb user password:::

    psql
    ALTER ROLE bigsdb WITH PASSWORD 'bigsdb';

3. Set up the jobs parameters in the /etc/bigsdb/bigsdb.conf file, e.g.::

    jobs_db=bigsdb_jobs
    max_load=8

   The jobs script will not process a job if the server's load average (over the last minute) is higher than the max_load parameter. This should be set higher than the number of processor cores or you may find that jobs never run on a busy server. Setting it to double the number of cores is probably a good starting point.

4. Copy the job_logging.conf file to the /etc/bigsdb directory.

5. Set the script to run frequently (preferably every minute) from CRON. Note that CRON does not like '.' in executable filenames, so either rename the script to 'bigsjobs' or create a symlink and call that from CRON, e.g.::

    copy bigsjobs.pl to /usr/local/bin
    sudo ln -s /usr/local/bin/bigsjobs.pl /usr/local/bin/bigsjobs

   You should install xvfb, which is a virtual X server that may be required for third party applications called from plugins. This is required, for example, for calling splitstree4 from the Genome Comparator plugin.

   Add the following to /etc/crontab:::

     * * * * * bigsdb xvfb-run -a /usr/local/bin/bigsjobs

   (set to run every minute from the 'bigsdb' user account).

6. Create a log file, bigsdb_jobs.log, in /var/log owned by 'bigsdb', e.g.::

    sudo touch /var/log/bigsdb_jobs.log
    sudo chown bigsdb /var/log/bigsdb_jobs.log

Periodically delete temporary files
===================================
There are two temporary directories (one public, one private) which may accumulate temporary files over time. Some of these are deleted automatically when no longer required but some cannot be cleaned automatically since they are used to display results after clicking a link or to pass the database query between pages of results.

The easiest way to clean the temp directories is to run a cleaning script periodically, e.g. create a root-executable script in /etc/cron.hourly containing the following:::

 #!/bin/sh
 #Remove temp BIGSdb files from secure tmp folder older than 1 week.
 find /var/tmp/ -name '*BIGSdb_*' -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null

 #Remove .jnlp files from web tree older than 1 day
 find /var/www/tmp/ -name '*.jnlp' -type f -mmin +1440 -exec rm -f {} \; 2>/dev/null

 #Remove other tmp files from web tree older than 1 week
 find /var/www/tmp/ -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null
