.. _update_delete_allele:

*************************************************
Updating and deleting allele sequence definitions
*************************************************
.. note::

   You cannot update the sequence of an allele definition. This is for reasons 
   of data integrity since an allele may form part of a scheme profile and be 
   referred to in multiple databases. If you really need to change a sequence, 
   you will have to remove the allele definition and then re-add it.  If the
   allele is a member of a scheme profile, you will also have to remove that
   profile first, then re-create it after deleting and re-adding the allele.

In order to update or delete an allele, first you must select it. Click the 
update/delete sequences link.

.. image:: /images/curation/update_alleles.png

Either search for specific attributes in the search form, or leave it blank and
click 'Submit' to return all alleles. For a specific allele, select the locus 
in the filter (click the small arrow next to 'Filter query by' to expand the 
filter) and enter the allele number in the allele_id field.

.. image:: /images/curation/update_alleles2.png

Click the appropriate link to either update the allele attributes or to delete
it. If you have appropriate permissions, there may also be a link to 'Delete 
ALL'. This allows you to quickly delete all alleles returned from a search.

.. image:: /images/curation/update_alleles3.png

If you choose to delete, you will be presented with a final confirmation 
screen. To go ahead, click 'Delete'. Deletion will not be possible if the 
allele is part of a scheme profile - if it is you will need to delete any 
profiles that it is a member of first. You can also choose to delete and
retire the allele identifier. If you do this, the allele identifier will not
be re-used. It is possible to set the configuration so that you only have
the option to delete and retire.

.. image:: /images/curation/delete_allele.png

If instead you clicked 'Update', you will be able to modify attributes of the 
sequence, or link PubMed, ENA or Genbank records to it. You will not be able 
to modify the sequence itself.

.. note::

   Adding flags and comments to an allele record requires that this feature is
   enabled in the :ref:`database configuration <seqdef_xml>`.

.. image:: /images/curation/update_alleles4.png
