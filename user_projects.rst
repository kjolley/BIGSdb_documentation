.. index::
   single: user projects
   
.. _user_projects:

#############
User projects
#############
If user projects are enabled, authenticated users are able to set up their own
projects in order to group isolates for analysis. If private data and user 
quotas are enabled, these projects can include private records that can then be
shared with other user accounts.

.. note::
   User projects can be enabled by an administrator by setting 
   'user_projects="yes"' in the :ref:`config.xml<isolate_xml>` file for the
   database.

To create a new project, go to the isolate database contents page and click
'Your projects'.

.. image:: /images/user_projects/user_projects1.png

Enter the name of your project (this must be unique on the system - you will be
told if the name is already used). You can optionally include a description - 
if you do this, this will appear within :ref:`isolate records<isolate_records>`
when accessed from your account. Click 'Create'.

.. image:: /images/user_projects/user_projects2.png

You can either add isolates to your project directly following a query or by 
manually editing a list of ids.

***************************************************
Adding isolates to a user project following a query
***************************************************
Perform an isolate database query. If you have set up a project, there will be
a link in the results header box. Select your project and click 'Add these 
records'.

.. image:: /images/user_projects/user_projects3.png

The records will be added to the project. Please note that it doesn't matter
whether any of the records have been previously added.

*************************************************************************
Adding or removing isolates belonging to a user project by editing a list
*************************************************************************
From the user projects page, click the 'Add/remove records' link for the 
project that you wish to modify.

.. image:: /images/user_projects/user_projects4.png

Edit the list of ids of records belonging to the list. You can copy and paste
this list if you wish to prepare it in a spreadsheet or text editor. Click
'Update' when finished.

.. image:: /images/user_projects/user_projects5.png

**************************
Accessing project isolates
**************************
To browse isolate records belonging to a project, go to the user projects page
and click the 'Browse' link for the project.

.. image:: /images/user_projects/user_projects6.png

Alternatively, you can select the project from the 
:ref:`projects filter<query_filters>` on the isolate query page. This would
enable you to combine the project with additional search criteria

.. image:: /images/user_projects/user_projects7.png

Please note that you will only see your project in the filter list if you are
logged in. As a private project, only you will see it.

******************************************
Allowing other users to share your project
******************************************
You can share a project that you own with any other user. In order to do this,
you must know the username that they use to log in with. They will see the
project in their own list of private projects and in the query interface 
projects filter.

From the user projects page, click the 'Modify users' link for the specified
project:

.. image:: /images/user_projects/user_projects8.png

Enter the username of the person you wish to share with and click 'Add user':

.. image:: /images/user_projects/user_projects9.png

If user groups are in use, you can also share your project with all members of
a user group (provided you are also a member of this group) from the same page.

Once a user has been added, you can give them permission to administer (add 
other users, modify the description or delete) or add/remove records to the 
project:

.. image:: /images/user_projects/user_projects10.png

***********************
Deleting a user project
***********************
You can delete a project from the user projects page by clicking the 'Delete'
link next to the project in question.

.. image:: /images/user_projects/user_projects11.png

If the project contains any isolates you will be asked for confirmation. Click
the 'Delete project' button.

.. image:: /images/user_projects/user_projects12.png

If the project contains no isolates, the confirmation page is skipped and the
project is removed immediately.

.. note::
   Removing a project does not delete the isolate records belonging to it. A
   project is simply a means of grouping records.
