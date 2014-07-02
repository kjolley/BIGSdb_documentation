*********************************
Frequently asked questions (FAQs)
*********************************

Installation
============

1. **BIGSdb is accumulating files in various temp directories - is this normal and how do I clean them out?**

   See: :ref:`Periodically delete temporary files <delete-temp-files>`.

2. **BIGSdb is complaining of an invalid script path - what does this mean?**

 In your database config.xml file system tag are two attributes - script_path_includes and curate_path_includes. These contain regexes that the web url to your script (bigsdb.pl and bigscurate.pl respectively) must match. This prevents somebody from accessing a private database using an instance of bigsdb.pl that is not in a protected directory if you’re using apache authentication.

 So, if you access the script from http://localhost/cgi-bin/bigsdb/bigsdb.pl then you can set script_path_includes to something like “/bigsdb/” (which is the default), or “/cgi-bin/” or just “/” if you don’t care about this check.

Administration
==============

1. **How can I make some isolates public but not others?**

 The easiest way to do this is to set up two or more separate configuration directories that refer to the database. The URLs to access these will differ by the value of the 'db' attribute, which refers to the name of the configuration directory (in /etc/bigsdb/dbases/). The database view accessed by each of these configurations can be different as can the access restrictions.

 *Example:*

 We have a database 'bigsdb_test' that contains data, only some of which we wish to make publicly available. The isolates to make public are all members of a project. First we can make a view of the isolates table that contains only isolates within this project.

 For isolates in project id 3, create a database view by logging in to psql as the postgresql user. We will name this view 'public'.::

  sudo su postgres
  psql bigsdb_test

  CREATE VIEW public AS SELECT * FROM isolates WHERE id IN (SELECT isolate_id FROM project_members WHERE project_id=3);
  GRANT SELECT ON public TO apache;

 Create a private configuration that can access everything in the database in /etc/bigsdb/dbases/test_private. This will be accessible from http://IP_ADDRESS/cgi-bin/bigsdb/bigsdb.pl?db=test_private.

 The important attributes to set in the system tag of the config.xml file in this directory are:::

  view="isolates"
  read_access="authenticated_users"

 This means that anyone with an account can log in and view all the isolates (because the view is set to the isolates table).

 Now create a public configuration in /etc/bigsdb/dbases/test_public. This will be accessible from http://IP_ADDRESS/cgi-bin/bigsdb/bigsdb.pl?db=test_public. It is better to create a symlink to the private config.xml and then override the attributes that are different. So create a symlink to the private config file: ::

  cd /etc/bigsdb/dbases/test_public
  sudo ln -s ../test_private/config.xml .

 You can now override the view and access settings. Within /etc/bigsdb/dbases/test_public, create a file called system.overrides and add the following: ::

  view="public"
  read_access="public"

 *Restricting particular configurations to specific user accounts*

 Suppose you only wanted specific users to access the private configuration (or indeed, any specific configuration).

 In /etc/bigsdb/dbases/test_private/config.xml, add the following directive: ::

  default_access="deny"

 This tells BIGSdb to deny access to anybody unless their account name appears within a file called users.allow within the config directory. The users.allow file should contain one username per line.

 Alternatively, you can deny access to specific users, while allowing every other authenticated user. In /etc/bigsdb/dbases/test_private/config.xml, add the following directive: ::

  default_access="allow"

 This tells BIGSdb to allow access to anybody unless their account name appears within a file called users.deny within the config directory. The users.deny file should contain one username per line.
