.. index::
   pair: retiring; profiles

***********************************
Retiring scheme profile identifiers
***********************************
Sometimes there is a requirement to prevent the automated assignment of a 
particular profile identifier (e.g. ST) - a profile with that identifier may 
have been commonly used and has since been removed. Reassignment of the 
identifier to a new profile may lead to confusion, so in this instance, it 
would be better to prevent this.

You can retire a profile identifier by clicking the 'Add' link in the 'Retired
profiles' box on the sequence database curators' page. This function is 
normally hidden, so you may need to click the 'Show all' toggle to display it.

.. image:: /images/curation/retire_profile1.png

Select the scheme from the dropdown list box and enter the profile id. Click
'Submit'.

.. image:: /images/curation/retire_profile2.png

You cannot retire a profile identifier that already exists, so you must delete 
it before retiring it.  Once an identifier is retired, you will not be able to 
create a new profile with that name.  

You can also retire a profile definition when you 
:ref:`delete a profile<update_delete_profile>`. 

.. index::
   pair: un-retiring; profiles

**************************************
Un-retiring scheme profile identifiers
**************************************
If a profile identifier, e.g. ST, has been retired, it is possible to un-retire
it so that it can be re-assigned. To do this, you need to remove the identifier
from the retired_profiles table.

First, find the profile identifier in the retired_profiles table by clicking the 
'Update/delete' retired profiles link on the sequence database curators' page. 
This function is normally hidden, so you may need to click the 'Show all' 
toggle to display it.

.. image:: /images/curation/unretire_profiles.png

Search by any criteria to find the profile identifier.

.. image:: /images/curation/unretire_profiles2.png

Click the delete link on the identifer to be un-retired.

.. image:: /images/curation/unretire_profiles3.png

A confirmation page will be displayed. Click 'Delete' to remove the identifier
from the retired profiles table.

.. image:: /images/curation/unretire_profiles4.png

The identifier can now be re-assigned when adding a new profile.
