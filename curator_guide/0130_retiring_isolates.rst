.. index::
   pair: retiring; isolates

****************************
Retiring isolate identifiers
****************************
Sometimes there is a requirement to prevent the automated assignment of a 
particular isolate identifier number - an isolate with that identifier may 
have been commonly referred to and has since been removed. Reassignment of the 
identifier to a new isolate record may lead to confusion, so in this instance,
it would be better to prevent this.

You can retire an isolate identifier by clicking the 'Add' retired isolates
link on the isolates database curators' page. This function is normally hidden,
so you may need to click the 'Show all' toggle to display it.

.. image:: /images/curation/retire_isolate1.png

Enter the isolate id to retire and click 'Submit'.

.. image:: /images/curation/retire_isolate2.png

You cannot retire an isolate identifier that already exists, so you must delete 
it before retiring it.  Once an identifier is retired, you will not be able to 
create a new isolate record using that identifier.  

You can also retire an isolate identifier when you 
:ref:`delete an isolate record<update_delete_isolate>`. 

.. index::
   pair: un-retiring; isolates

*******************************
Un-retiring isolate identifiers
*******************************
If an isolate identifier has been retired, it is possible to un-retire
it so that it can be re-assigned. To do this, you need to remove the identifier
from the retired_isolates table.

First, find the isolate identifier in the retired_isolates table by clicking the 
'Update/delete' retired isolates link on the isolate database curators' page. 
This function is normally hidden, so you may need to click the 'Show all' 
toggle to display it.

.. image:: /images/curation/unretire_isolates.png

Search by any criteria to find the isolate identifier.

.. image:: /images/curation/unretire_isolates2.png

Click the delete link on the identifer to be un-retired.

.. image:: /images/curation/unretire_isolates3.png

A confirmation page will be displayed. Click 'Delete' to remove the identifier
from the retired isolates table.

.. image:: /images/curation/unretire_isolates4.png

The identifier can now be re-assigned when adding a new isolate record.
