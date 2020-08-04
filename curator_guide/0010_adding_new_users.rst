.. index::
   single: users; adding

*************************
Adding new sender details
*************************
All records within the databases are associated with a sender.  Whenever
somebody new submits data, they should be added to the users table so that 
their name appears in the dropdown lists on the data upload forms.

To add a user, click the add users (+) link on the curator's contents page.

.. image:: /images/curation/add_users.png 

Enter the user's details in to the form.

.. image:: /images/curation/add_users2.png 

Normally the status should be set as 'user'.  Only admins and curators with
special permissions can create users with a status of curator or admin.

If the submission system is in operation there will be an option at the bottom
called 'submission_emails'.  This is to enable users with a status of 'curator'
or 'admin' to receive E-mails on receipt of new submissions.  It is not 
relevant for users with a status of 'user' or 'submitter'.
