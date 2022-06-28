.. _gp_lookups:

.. index::
   single: geographic coordinates

**********************************************
Populating geographic coordinate lookup values
**********************************************
If a field has the geographic_point_lookup attribute set to 'yes' in the
:ref:`config.xml file<isolate_xml_field>`, field values can be mapped to GPS 
coordinates to facilitate mapping.

If the user has curator privileges with the 'modify_geopoints' permission set,
or is an admin, a curator link to modify 'Geopoint field lookup' will be 
available in the curator interface. This link is normally hidden but can be
shown by selecting the 'Show all' toggle.

To add a value, click the 'Add' link:

.. image:: /images/curation/geopoint_lookup.png

Select the 2 letter ISO country code and the linked field from the dropdown
lists. Enter the town or city in the value field, and the GPS coordinates 
in LATITUDE, LONGITUDE format.

.. image:: /images/curation/geopoint_lookup2.png

Now, whenever that specified field value is used, a map will appear in the
isolate information page showing the location. In addition, these values will
be used in mapping in the Field Breakdown and Microreact plugins.

GPS coordinates can be mapped in bulk using the gp_town_lookups.pl script.
