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
-----------------------------------------------

Setting up the admin user
-------------------------
The first admin user needs to be manually added to the users table of the database. Connect to the database using psql and add the following (changing details to suit the user).::

 INSERT INTO users (id,user_name,surname,first_name,email,affiliation,status,date_entered,datestamp,curator) VALUES (1,'keith','Jolley','Keith','keith.jolley@zoo.ox.ac.uk','University of Oxford, UK','admin','today','today',1);

If you are using built-in authentication, set the password for this user using the add_user.pl script. Other users can be added by the admin user from the curation interface accessible from http://your_website/cgi-bin/private/bigscurate.pl?db=test_db (or wherever you have located your bigscurate.pl script).

Setting up the offline job manager
----------------------------------
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
-----------------------------------
There are two temporary directories (one public, one private) which may accumulate temporary files over time. Some of these are deleted automatically when no longer required but some cannot be cleaned automatically since they are used to display results after clicking a link or to pass the database query between pages of results.

The easiest way to clean the temp directories is to run a cleaning script periodically, e.g. create a root-executable script in /etc/cron.hourly containing the following:::

 #!/bin/sh
 #Remove temp BIGSdb files from secure tmp folder older than 1 week.
 find /var/tmp/ -name '*BIGSdb_*' -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null

 #Remove .jnlp files from web tree older than 1 day
 find /var/www/tmp/ -name '*.jnlp' -type f -mmin +1440 -exec rm -f {} \; 2>/dev/null

 #Remove other tmp files from web tree older than 1 week
 find /var/www/tmp/ -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null
