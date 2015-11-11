*********************************
Frequently asked questions (FAQs)
*********************************

General
=======
1. **What is the minimum specification of hardware required to run BIGSdb?**

 The software will run on very modest hardware - a number of PubMLST mirrors
 have been set up on virtual machines with 1 processor core and 4 GB RAM.
 This should be considered an absolute minimum specification though.  For an 
 installation with only local users, the following minimum is recommended:
 
  * 4 processor cores
  * 16 GB RAM
  * 50 GB partition for temporary files
  * 100 GB partition for databases
  
 As usual, the more RAM that is available the better.  Ideally you would want
 enough RAM that the whole database(s) can reside in memory (an approximation 
 is roughly twice the total size of your contigs), although this is not
 absolutely required.
 
 Offline jobs, such as :ref:`Genome Comparator <genome_comparator>` will use a
 processor core each, so if you want to run multiple jobs in parallel then you
 may want more cores (and memory).  Tagging of new genomes using the offline
 :ref:`autotagger <autotagger>` can be run in multi-threaded mode so the
 more cores available the faster this will be.
 
 As a comparison, the PubMLST site is run on two machines - separate web 
 and database servers.  All offline jobs and tagging of genomes is performed
 on the database server.  These have the following specification:
 
  * web server: 16 cores, 64GB RAM
  * database server: 64 cores, 1TB RAM, 3TB RAID 10 local storage
  
2. **Why might icons be missing when using Internet Explorer?**

 This can occur if you have Compatibility Mode enabled. BIGSdb generates valid
 HTML5 and Compatibility Mode should not be used. Please ensure this is not
 enabled in the Internet Explorer tools section.

Installation
============

1. **BIGSdb is accumulating files in various temp directories - is this normal 
   and how do I clean them out?**

   See: :ref:`Periodically delete temporary files <delete-temp-files>`.

2. **BIGSdb is complaining of an invalid script path - what does this mean?**

 In your database config.xml file system tag are two attributes - 
 script_path_includes and curate_path_includes. These contain regexes that the 
 web url to your script (bigsdb.pl and bigscurate.pl respectively) must match. 
 This prevents somebody from accessing a private database using an instance of 
 bigsdb.pl that is not in a protected directory if you’re using apache 
 authentication.

 So, if you access the script from http://localhost/cgi-bin/bigsdb/bigsdb.pl 
 then you can set script_path_includes to something like “/bigsdb/” (which is 
 the default), or “/cgi-bin/” or just “/” if you don’t care about this check.

Administration
==============

1. **How can I make some isolates public but not others?**

 The easiest way to do this is to set up two or more separate configuration 
 directories that refer to the database. The URLs to access these will differ 
 by the value of the 'db' attribute, which refers to the name of the 
 configuration directory (in /etc/bigsdb/dbases/). The database view accessed 
 by each of these configurations can be different as can the access 
 restrictions.

 *Example:*

 We have a database 'bigsdb_test' that contains data, only some of which we 
 wish to make publicly available. The isolates to make public are all members 
 of a project. First we can make a view of the isolates table that contains 
 only isolates within this project.

 For isolates in project id 3, create a database view by logging in to psql 
 as the postgresql user. We will name this view 'public'.::

  sudo su postgres
  psql bigsdb_test

  CREATE VIEW public AS SELECT * FROM isolates WHERE id IN (SELECT isolate_id 
    FROM project_members WHERE project_id=3);
  GRANT SELECT ON public TO apache;

 Create a private configuration that can access everything in the database in 
 /etc/bigsdb/dbases/test_private. This will be accessible from 
 http://IP_ADDRESS/cgi-bin/bigsdb/bigsdb.pl?db=test_private.

 The important attributes to set in the system tag of the config.xml file in 
 this directory are:::

  view="isolates"
  read_access="authenticated_users"

 This means that anyone with an account can log in and view all the isolates 
 (because the view is set to the isolates table).

 Now create a public configuration in /etc/bigsdb/dbases/test_public. This will
 be accessible from 
 http://IP_ADDRESS/cgi-bin/bigsdb/bigsdb.pl?db=test_public. 
 It is better to create a symlink to the private config.xml and then override 
 the attributes that are different. So create a symlink to the private config 
 file: ::

  cd /etc/bigsdb/dbases/test_public
  sudo ln -s ../test_private/config.xml .

 You can now override the view and access settings. Within 
 /etc/bigsdb/dbases/test_public, create a file called system.overrides and add 
 the following: ::

  view="public"
  read_access="public"

See also 
:ref:`Restricting particular configurations to 
specific user accounts <default_access>`.
