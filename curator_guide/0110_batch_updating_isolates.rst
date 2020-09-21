.. index::
   pair: updating; isolates

***************************************
Batch updating multiple isolate records
***************************************
Select 'batch update' isolates link on the curator's index page.

.. image:: /images/curation/batch_update_isolate.png

Prepare your update data in 3 columns in a spreadsheet:

#. Unique identifier field
#. Field to be updated
#. New value for field

You should also include a header line at the top - this isn't used so can
contain anything but it should be present.

Columns must be tab-delimited which they will be if you copy and paste directly
from the spreadsheet.

So, to update isolate id-100 and id-101 to serogroup B you would prepare the
following: ::

  id     field     value
  100    serogroup B
  101    serogroup B

Select the field you are using as a unique identifier, in this case id, from
the drop-down list box, and paste in the data. If the fields already have
values set, you should also check the 'Update existing values' checkbox. Press
'submit'.

.. image:: /images/curation/batch_update_isolate2.png

A confirmation page will be displayed if there are no problems. If there are
problems, these will be listed.  Press 'Upload' to upload the changes.

.. image:: /images/curation/batch_update_isolate3.png

You can also use a secondary selection field such that a combination of two
fields uniquely defines the isolate, for example using country and isolate
name.

So, for example, to update the serogroups of isolates CN100 and CN103, both
from the UK, select the appropriate primary and secondary fields and prepare
the data as follows: ::

  isolate     country     field      value
  CN100       UK          serogroup  B
  CN103       UK          serogroup  B
