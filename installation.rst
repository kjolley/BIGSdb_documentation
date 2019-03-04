########################################
Installation and configuration of BIGSdb
########################################

*********************
Software installation
*********************
BIGSdb consists of two main Perl scripts, bigsdb.pl and bigscurate.pl, that run
the query and curator's interfaces respectively. These need to be located 
somewhere within the web cgi-bin directories. In addition, there are a large 
number of library files, used by both these scripts, that are installed by 
default in /usr/local/lib/BIGSdb. Plugin scripts are stored within a 'Plugins'
sub-directory of this library directory.

All databases on a system can use the same instance of the scripts, or 
alternatively any database can specify a particular path for each script, 
enabling these script directories to be protected by apache htaccess 
directives.

 * :doc:`Software requirements <dependencies>`
 * Download from `SourceForge.net <http://sourceforge.net/projects/bigsdb/>`_ 
   or `GitHub <https://github.com/kjolley/BIGSdb>`_.

1. Unpack the distribution package in a temporary directory: ::

    gunzip bigsdb_1.x.x.tar.gz
    tar xvf bigsdb_1.x.x.tar

2. Copy the bigsdb.pl and bigscurate.pl scripts to a subdirectory of your web
   server's cgi-bin directory. Make sure these are readable and executable by 
   the web server daemon.
3. Copy the contents of the lib directory to /usr/local/lib/BIGSdb/. Make sure
   you include the Plugins and Offline directories which are subdirectories of
   the main lib directory.
4. Copy the javascript directory to the root directory of your website, i.e. 
   accessible from http://your_website/javascript/.
5. Copy the css directory to root directory of your website, i.e. accessible 
   from http://your_website/css/.
6. Copy the webfonts directory to the root directory of your website, i.e. 
   accessible from http://your_website/webfonts/.  
7. Copy the images directory to the root directory of your website, i.e. 
   accessible from http://your_website/images/.
8. Copy the contents of the conf directory to /etc/bigsdb/. Check the paths of
   helper applications and database names in the bigsdb.conf file and modify 
   for your system.
9. Create a PostgreSQL database user called apache - this should not have any
   special priveleges. First you will need to log in as the postgres user: ::

     sudo su postgres

   Then use the createuser command to do this, e.g. ::

     createuser apache

   From the psql command line, set the apache user password: ::

     psql
     ALTER ROLE apache WITH PASSWORD 'remote';

10. Create PostgreSQL databases called bigsdb_auth, bigsdb_prefs and bigsdb_refs
    using the scripts in the sql directory. Create the database using the 
    createdb command and set up the tables using the psql command. ::

     createdb bigsdb_auth
     psql -f auth.sql bigsdb_auth
     createdb bigsdb_prefs
     psql -f prefs.sql bigsdb_prefs
     createdb bigsdb_refs
     psql -f refs.sql bigsdb_refs

11. Create a writable temporary directory in the root of the web site called
    tmp, i.e. accessible from http://your_website/tmp.
12. Create a log file, bigsdb.log, in /var/log owned by the web server daemon,
    e.g. ::

     touch /var/log/bigsdb.log
     chown www-data /var/log/bigsdb.log

    (substitute www-data for the web daemon user).

**********************
Configuring PostgreSQL
**********************
PostgreSQL can be configured in many ways and how you do this will depend on your site requirements.

The following security settings will allow the appropriate users 'apache' and
'bigsdb' to access databases without allowing all logged in users full access.
Only the UNIX users 'postgres' and 'webmaster' can log in to the databases
as the Postgres user 'postgres'.

You will need to edit the pg_hba.conf and pg_ident.conf files.  These are
found somewhere like /etc/postgresql/9.1/main/

pg_hba.conf
===========
::

 # Database administrative login by UNIX sockets
 local   all         postgres                          ident map=mymap

 # TYPE  DATABASE    USER        CIDR-ADDRESS          METHOD

 # "local" is for Unix domain socket connections only
 local   all         all                               ident map=mymap
 # IPv4 local connections:
 host    all         all         127.0.0.1/32          md5
 # IPv6 local connections:
 host    all         all         ::1/128               md5

pg_ident.conf
=============
::

 # MAPNAME     SYSTEM-USERNAME    PG-USERNAME

   mymap       postgres           postgres
   mymap       webmaster          postgres
   mymap       www-data           apache
   mymap       bigsdb             bigsdb
   mymap       bigsdb             apache

You may also need to change some settings in the postgresql.conf file.  As an example, a configuration for a machine with 16GB RAM, allowing connections from a separate web server may have the following configuration changes made: ::

 listen_addresses = '*'
 max_connections = 200
 shared_buffers = 1024Mb
 work_mem = 8Mb
 effective_cache_size = 8192Mb
 stats_temp_directory = '/dev/shm'

Setting stats_temp_directory to /dev/shm makes use of a ramdisk usually available on Debian or Ubuntu systems for frequently updated working files.  This reduces a lot of unneccessary disk access.

See `Tuning Your PostgreSQL Server <https://wiki.postgresql.org/wiki/Tuning_Your_PostgreSQL_Server>`_ for more details.

Restart PostgreSQL after any changes, e.g. ::
 
 /etc/init.d/postgresql restart
 
************************************
Setting global connection parameters
************************************
Global database connection parameters can be entered in /etc/bigsdb/db.conf.
This allows you to set default values for the host, port, user and password.
Default values are as follows:

 * dbhost: localhost
 * dbport: 5432
 * dbuser: apache
 * dbpassword: remote
 
These can all be over-ridden in individual :ref:`database configuration 
config.xml files<xml>` using the terms host, port, user, and password.

***************************
Site-specific configuration
***************************
Site-specific configuration files are located in /etc/bigsdb by default.

* :download:`bigsdb.conf <conf/bigsdb.conf>` - main configuration file
* :download:`logging.conf <conf/logging.conf>` - error logging settings. 
  See log4perl project website for advanced configuration details.

The dropdown menu can be customized by modifying the menu_header.html file 
located in /etc/bigsdb. Any HTML in this file will be inserted at the top of
the menu. The included file displays the BIGSdb logo hyperlinked
to the root of the web site. This file can be edited as you wish, or 
alternatively menu_header.html can be placed in the root directory of the
web site - this will be used in preference to the version in /etc/bigsdb.

**********************************
Setting up the offline job manager
**********************************
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

   If you'd like to run this more frequently, e.g. every 30 seconds, multiple entries can be added to CRON with an appropriate sleep prior to running, e.g.::

     * * * * * bigsdb  xvfb-run -a /usr/local/bin/bigsjobs 
     * * * * * bigsdb  sleep 30;xvfb-run -a /usr/local/bin/bigsjobs 

6. Create a log file, bigsdb_jobs.log, in /var/log owned by 'bigsdb', e.g.::

    sudo touch /var/log/bigsdb_jobs.log
    sudo chown bigsdb /var/log/bigsdb_jobs.log
    
********************************
Setting up the submission system
********************************
The submission system allows users to submit new data to the database for
curation.  Submissions are placed in a queue for a curator to upload.
All communication between submitters and curators can occur via the submission
system.

1.  Create a writable submissions directory in the root of the web site called
    submissions, i.e. accessible from http://your_website/submissions.  This is
    used for file uploads.  The directory should be writable by the Apache web
    daemon (user 'www-data' on Debian/Ubuntu systems). If you are running the
    :ref:`RESTful interface<restful_api>` the directory should also be writable
    by the bigsdb user. To ensure this, make the directory group-writable and 
    add the bigsdb user to the apache group ('www-data' on Debian/Ubuntu 
    systems). If you will be allowing submissions via the RESTful interface, 
    you should also add the apache user ('www-data' on Debian/Ubuntu systems)
    to the bigsdb group, e.g. ::
    
       sudo usermod -a -G www-data bigsdb
       sudo usermod -a -G bigsdb www-data
       
    The actual directory can be outside of the web root 
    and made accessible using a symlink provided your Apache configuration 
    allows this, e.g. the default location is /var/submissions symlinked to 
    /var/www/submissions (assuming your web site is located in /var/www), 
    e.g. ::
   
      sudo touch /var/submissions
      sudo chown www-data:www-data /var/submissions
      sudo chmod 775 /var/submissions
      sudo ln -s /var/submissions /var/www
     
2.  Set the submission_dir location in bigsdb.conf.

3.  Set the smtp_server in bigsdb.conf to the IP or DNS name of your 
    organisation's SMTP relay.  Depending on how your E-mail system is 
    configured, you may be able to use the localhost address (127.0.0.1).
 
4.  Make sure the curate_script and query_script values are set in bigsdb.conf.
    These point to the web-accessible location of the web scripts and are
    required to allow curators to be directed between the web interfaces as
    needed.
    
5.  Set submissions="yes" in the system tag of the 
    :ref:`database config.xml file<xml>` of each database for which submissions
    should be enabled. 
    
.. _site-wide-db: 
    
************************************
Setting up a site-wide user database
************************************
A site-wide user database allows users to register themselves for accounts and
associate these with specific databases. It means that a single set of log-in
credentials can be used across databases, rather than each database maintaining
its own.

Users can access/update their account details by calling the bigsdb.pl script
without any additional attributes, e.g. http://website/cgi-bin/bigsdb.pl.

Site admins can access administration features by calling the bigscurate.pl
script without any additional attributes.

1.  Create a user database, e.g. pubmlst_bigsdb_users::

      createdb pubmlst_bigsdb_users
      psql -f users.sql pubmlst_bigsdb_users
      
    Set up sync_user_dbase_users.pl to run every hour as a CRON JOB, e.g. in 
    /etc/crontab, add the following to run this at 5 minutes past each hour :: 
    
      05  *  *  *  *  bigsdb   /usr/local/bin/sync_user_dbase_users.pl --user_database pubmlst_bigsdb_users
    
    Add the user database details to each database that you want to allow to 
    use it.
    
    You need to :ref:`add the users database details<setting_site_users_db>` 
    to each client database that will use it.
    
2.  If you want to allow users to register themselves you need to modify 
    bigsdb.conf.

    You can define multiple user databases (as a comma-separated list) but 
    usually you would have just one. Define this using the site_user_dbs 
    attribute. Use a short domain (site) name separated by a pipe (|) and the
    name of the database, e.g. add the following to /etc/bigsdb.conf:: 

      site_user_dbs=PubMLST|pubmlst_bigsdb_users

    Make sure default database connection parameters are set in 
    /etc/bigsdb/db.conf.
    
3.  Set up site admin user in new user database. This has to be done manually -
    other users will either be able to register themselves or be created by 
    curators from other databases.:: 
    
      psql pubmlst_bigsdb_users
      INSERT INTO USERS (user_name,surname,first_name,email,affiliation,
        date_entered,datestamp,status) VALUES ('kjolley','Jolley','Keith',
        'keith.jolley@zoo.ox.ac.uk','University of Oxford, UK','now','now',
        'validated');
        
    Set the password for this user using the add_user.pl script (change 
    XXXXXXXX to the password value):: 
    
      add_user.pl -a -d pubmlst_bigsdb_users -n kjolley -p XXXXXXXX
      
    Add specific permissions that this admin user can have by directly adding
    the following terms to the permissions table: 
    
    * set_site_user_passwords: 
      
      * Allow admin to set user passwords.
      
    * import_dbase_configs: 
    
      * Allow admin to define which database configurations are made available
        for registration.
      
    * merge_users
    
      * Allow admin to merge user accounts.
      
    * modify_users
    
      * Allow admin to edit user details.
      
    e.g. ::
    
      psql pubmlst_bigsdb_users
      INSERT INTO permissions (user_name,permission,curator,datestamp) VALUES 
        ('kjolley','import_dbase_configs','kjolley','now');
      
4.  Specific :ref:`permissions can be set for curators<curator_permissions>` in
    individual databases:

    * import_site_users
      
      * This allows the curator to import site users in to the database.
        
    * modify_site_users
      
      * You may not wish to do this! - It allows the curator of any database 
        with this permission to change the details of a user that may be used
        on other databases on the site.
        
5.  HTML header files can be defined for use when bigsdb.pl or bigscurate.pl 
    are called withouth a database configuration, such as when a user is 
    registering or modifying their user details. These files, site_header.html,
    site_footer.html, site_curate_header.html and site_curate_footer.html 
    should be placed in the root directory of the web site. 
   
.. _delete-temp-files: 

***********************************
Periodically delete temporary files
***********************************
There are two temporary directories (one public, one private) which may
accumulate temporary files over time. Some of these are deleted automatically
when no longer required but some cannot be cleaned automatically since they are
used to display results after clicking a link or to pass the database query
between pages of results.

The easiest way to clean the temp directories is to run a cleaning script
periodically, e.g. create a root-executable script in /etc/cron.hourly
containing the following:::

 #!/bin/sh
 #Remove temp BIGSdb files from secure tmp folder older than 1 week.
 find /var/tmp/ -name '*BIGSdb_*' -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null

 #Remove .jnlp files from web tree older than 1 day
 find /var/www/tmp/ -name '*.jnlp' -type f -mmin +1440 -exec rm -f {} \; 2>/dev/null

 #Remove other tmp files from web tree older than 1 week
 find /var/www/tmp/ -type f -mmin +10080 -exec rm -f {} \; 2>/dev/null
 
*********************************************
Prevent preference database getting too large
*********************************************
The preferences database stores user preferences for BIGSdb databases running
on the site.  Every user will have a globally unique identifier (guid) stored
in this database along with a datestamp indicating the last access time. On
public databases that do not require logging in, this guid is stored as a 
cookie on the user's computer.  Databases that require logging in use a 
combination of database and username as the identifier.  Over time, the 
preferences database can get quite large since every unique user will result 
in an entry in the database.  Since many of these entries represent casual
users, or even web indexing bots, they can be periodically cleaned out based
on their last access time.  A weekly CRON job can be set up to remove any 
entries older than a defined period.  For example, the following line entered
in /etc/crontab will remove the preferences for any user that has not accessed
any database in the past 6 months (the script will run at 6pm every Sunday). ::

 #Prevent prefs database getting too large
 00   18 *  *  0  postgres    psql -c "DELETE FROM guid WHERE last_accessed < NOW() - INTERVAL '6 months'" bigsdb_prefs
 
*****************
Log file rotation
*****************
Set the log file to auto rotate by adding a file called 'bigsdb' with the 
following contents to /etc/logrotate.d: ::

 /var/log/bigsdb.log {
   weekly
   rotate 4
   compress
   copytruncate
   missingok
   notifempty
   create 640 root adm
 }

 /var/log/bigsdb_jobs.log {
   weekly
   rotate 4
   compress
   copytruncate
   missingok
   notifempty
   create 640 root adm
 }

****************
Upgrading BIGSdb
****************
Major version changes, e.g. 1.7 -> 1.8, indicate that there has been a change
to the underlying database structure for one or more of the database types.
Scripts to upgrade the database are provided in sql/upgrade and are named by
the database type and version number.  For example, to upgrade an isolate
database (bigsdb_isolates) from version 1.7 to 1.8, log in as the postgres user
and type: ::

 psql -f isolatedb_v1.8.sql bigsdb_isolates

Upgrades are sequential, so to upgrade from a version earlier than the last
major version you would need to upgrade to the intermediate version first, e.g.
to go from 1.6 -> 1.8, requires upgrading to 1.7 first.

Minor version changes, e.g. 1.8.0 -> 1.8.1, have no modifications to the
database structures.  There will be changes to the Perl library modules and
possibly to the contents of the Javascript directory, images directory and CSS
files.

.. _restful_api:

************************************
Running the BIGSdb RESTful interface
************************************
BIGSdb has an Application Programming Interface (API) that allows third-party
applications to access the data within the databases.  The script that runs
this is called bigsrest.pl.  This is a Dancer2 application that can be run 
using a wide range of options, e.g. as a stand-alone script, using Perl 
webservers with plackup, or from apache.  Full documentation for 
`deploying Dancer2 applications <http://search.cpan.org/~xsawyerx/Dancer2-0.200002/lib/Dancer2/Manual/Deployment.pod>`_
can be found online.

The script requires a new database that describes the resources to make
available.  This is specified in the bigsdb.conf file as the value of the
'rest_db' attribute.  By default, the database is named bigsdb_rest.

A SQL file to create this database can be found in the sql directory of the
download archive.  It is called rest.sql.  To create the database, as the
postgres user, navigate to the sql directory and type ::

  createdb bigsdb_rest
  psql -f rest.sql bigsdb_rest
 
This database will need to be populated using psql or any tool that can be used
to edit PostgreSQL databases.  The database contains three tables that together
describe and group the databases resources that will be made available through
the API. The tables are:

* resources
   * this contains two fields (both compulsory):
      * **dbase_config** - the name of the database configuration used with
        the database.  This is the same as the name of the directory that 
        contains the config.xml file in the /etc/bigsdb/dbases directory.
      * **description** - short description of the database.

* groups (used to group related resources together)
   * this contains two fields (compulsory fields shown in bold):
      * **name** - short name of group.  This is usually a single word and is also
        the key that links resources to groups.
      * **description** - short description of group.
      * long_description - fuller description of group.

* group_resources (used to add resources to groups)
   * this contains two fields (both compulsory)
      * **group_name** - name of group.  This must already exist in the groups
        table.
      * **dbase_config** - the name of database resource.  This must already
        exist in the resources table.
  
For example, to describe the PubMLST resources for Neisseria, connect to the
bigsdb_rest database using psql, ::

   psql bigsdb_rest
   
Then enter the following SQL commands.  First add the database resources: ::

   INSERT INTO resources (dbase_config,description) VALUES
   ('pubmlst_neisseria_seqdef','Neisseria sequence/profile definitions');
   INSERT INTO resources (dbase_config,description) VALUES
   ('pubmlst_neisseria_isolates','Neisseria isolates');
   
Then create a 'neisseria' group that will contain these resources: ::

   INSERT INTO groups (name,description) VALUES 
   ('neisseria','Neisseria spp.');
   
Finally, add the database resources to the group: ::

   INSERT INTO group_resources (group_name,dbase_config) VALUES 
   ('neisseria','pubmlst_neisseria_seqdef');
   INSERT INTO group_resources (group_name,dbase_config) VALUES 
   ('neisseria','pubmlst_neisseria_isolates');
      
The REST API will need to run on its own network port.  By default this is port 
3000.  To run as a stand-alone script, from the script directory, as the bigsdb 
user, simply type: ::

   ./bigsrest.pl
   
This will start the API on port 3000.  You will be able to check 
that this is running using a web browser by navigating to http://localhost:3000
on the local machine, or using the server IP address from a remote machine.
You may need to modify your server firewall rules to allow connection to this
port.

Running as a stand-alone script is useful for testing, but you can achieve much
better performance using a Perl webserver with plackup.  There are various
options to choose.  PubMLST uses 
`Starman <http://search.cpan.org/dist/Starman/>`_.

To run the API using Starman, type the following as the bigsdb user: ::

   plackup -a /var/rest/bigsrest.pl -s Starman -E deployment
   
where the value of -a refers to the location of the bigsrest.pl script.  
Starman defaults to using port 5000.  

Different Linux distributions use different means to control services/daemons.
To start the REST interface on system boot on systems using upstart, create a 
file called bigsdb-rest.conf in /etc/init.  The contents of this file should
be something like (modify file paths as appropriate): ::

  description "Start BIGSdb REST interface"
  version "1.0"
  author "Keith Jolley"

  start on runlevel [12345]

  ## tell upstart we're creating a daemon
  expect fork
  
  script
  
  exec su -s /bin/sh -c 'exec "$0" "$@"' bigsdb -- /usr/local/bin/plackup -a /var/rest/bigsrest.pl -s Starman -E deployment
  
  end script
  
The service will then start automatically on boot or can be manually started 
by calling: ::

  sudo service bigsdb-rest start 
  
For systems using systemd, create a file in /etc/systemd/system called 
bigsdb-rest.service with the following contents (again, modify file paths
as appropriate): ::

  [Unit]
  Description=BIGSdb REST interface
  After=network.target
  
  [Service]
  User=bigsdb
  ExecStart=/usr/bin/plackup -a /var/rest/bigsrest.pl -s Starman -E deployment
  Restart=always

  [Install]
  WantedBy=multi-user.target
  
To start the service automatically on boot you need to enable it: ::

  sudo systemctl enable bigsdb-rest.service

It can also be manually started by calling: ::

  sudo systemctl start bigsdb-rest.service


Proxying the API to use a standard web port
===========================================
Usually you will want your API to be available on the standard web port 80.
To do this you will need to set up a virtual host using a different domain
name from your web site to proxy the API port.  For example, PubMLST has a
separate domain 'http://rest.pubmlst.org' for its API.  This is set up as a
virtual host directive in apache with the following configuration file: ::

   <VirtualHost *>
     ServerName rest.pubmlst.org
     DocumentRoot /var/rest
     ServerAdmin keith.jolley@zoo.ox.ac.uk
      <Directory /var/rest>
       AllowOverride None
       Require all granted
     </Directory>
   
     ProxyPass / http://rest.pubmlst.org:5000/
     ProxyPassReverse / http://rest.pubmlst.org:5000/
   
     <Proxy *>
         Order allow,deny
         Allow from all
     </Proxy>
   
     ErrorLog  /var/log/apache2/rest.pubmlst.org-error.log
     CustomLog /var/log/apache2/rest.pubmlst.org-access.log common
   
   </VirtualHost>

You should also set 'rest_behind_proxy=1' in bigsdb.conf. 
