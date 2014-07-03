*********************
Administrator's guide
*********************

General
=======

Please note that links displayed within the curation interface will vary depending on database contents and the permissions of the curator.

Types of user
-------------
There are three types of user in BIGSdb:

* User - can view data but never modify it. Users should be created for every submitter of data so that records can be tracked, even if they do not actually use the database. Individual isolate records may not be available to every user if access control lists (ACLs) are configured for the database.
* Curator - can modify data but does not have full control of the database. :ref:`Individual permissions <curator_permissions>` can be set for each curator, so their roles can be controlled. A curator with no specific permissions set has no more power than a standard user.
* Admin - has full control of the database, including setting permissions for curators and setting user passwords if built-in authentication is in use.

.. _curator_permissions:

Curator permissions
-------------------
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
-----------------------------------------------------------
To be allowed to define alleles or scheme profiles, curators must be granted specific permission for each locus and scheme by adding their user id number to the 'locus curator' and 'scheme curator' lists.

The easiest way to modify these lists is to use the batch update link next to 'locus curator control list' and 'scheme curator control list':

.. image:: /images/administration/update_locus_curator_list.png

Select the curator from the list:

.. image:: /images/administration/update_locus_curator_list2.png

Then select loci/schemes that the user is allowed to curate in the left hand 'Available' list, and click the right button to move these to the 'Selected' list:

.. image:: /images/administration/update_locus_curator_list3.png

If you uncheck the 'Hide curator name from public view' checkbox, the curator name and E-mail address will appear alongside loci in the download table on the website. 

Controlling access
------------------

Access control lists
^^^^^^^^^^^^^^^^^^^^
If access control lists are in use (set the read_access attribute to 'acl' in the system tag of the database XML configuration file), viewing and modifying of individual isolates can be restricted to particular users or usergroups.

**Please note that access control lists are likely to be deprecated in future releases.  This is in favour of creating a new class of user that would be allowed to curate their own data only.**

New isolate records are automatically set with the following access control:

* All users: read, not write (all users are members of 'All users' group).
* Curator who added data: read and write.

All access controls can be modified by an admin or curator with appropriate permission. This can be done for individual isolate records or in batch mode following an isolate search in the curation interface.

.. _default_access:

Restricting particular configurations to specific user accounts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Suppose you only wanted specific users to access a database configuration.

In the config.xml, add the following directive: ::

 default_access="deny"

This tells BIGSdb to deny access to anybody unless their account name appears within a file called users.allow within the config directory. The users.allow file should contain one username per line.

Alternatively, you can deny access to specific users, while allowing every other authenticated user. In /etc/bigsdb/dbases/test_private/config.xml, add the following directive: ::

 default_access="allow"

This tells BIGSdb to allow access to anybody unless their account name appears within a file called users.deny within the config directory. The users.deny file should contain one username per line.

Setting user passwords
----------------------
*Please note that these instructions only apply if using the built-in BIGSdb authentication system.*

If you are an administrator or a curator with specific permission to change other users' passwords, you should see a link to 'set user passwords' at the bottom of the curator's index page. Click this.

.. image:: /images/administration/set_passwords.png

Select the appropriate user from the drop-down list box and enter the new password twice where prompted.

.. image:: /images/administration/set_passwords2.png

Click 'Set password' and the password will be updated.

.. _set_first_password:

Setting the first password
^^^^^^^^^^^^^^^^^^^^^^^^^^
To set the first administrator's password for a new database, use the add_user.pl script found in the scripts/maintenance directory: ::

 add_user.pl [-a] -d <dbase> -n <username> -p <password>

The first user account needs to be added to the database :ref:`manually <setup_admin_user>`.

Enabling plugins
----------------

Workflow for setting up a MLST scheme
-------------------------------------

Temporarily disabling database updates
--------------------------------------

Host mapping
------------

Improving performance
---------------------

Dataset partitioning
--------------------

Sequence definition databases
=============================

Adding new loci
---------------

Defining schemes
----------------

Setting up client databases
---------------------------

Rule-based queries
------------------

Isolate databases
=================

Adding new loci
---------------

Genome filtering
----------------

Setting locus genome positions
------------------------------

Defining schemes
----------------

Defining composite fields
-------------------------

Extended provenance attributes (lookup tables)
----------------------------------------------

Checking external database configuration settings
-------------------------------------------------
