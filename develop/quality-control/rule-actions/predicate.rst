.. _qc_actions_predicate:

Predicate
---------

The predicate is a FHIRPath rule that is tested against every resource. 
The predicate rule, gives an error for each resource where the predicate
evaluates to false.

For example, the following rule gives an error for each resource without the ``id`` element:

.. code-block:: yaml

   - # action: predicate # Can be added for consistency, but not necessary
     predicate: id.exists()
     error: This resource does not have an id

There is a large similarity between ``predicate`` and the :ref:`FHIRPath based filters <qc_filters_fhirpath>`.
Where the outcome (True or False) of a FHIRPath based ``filter`` determines if the resource will be checked or ignored,
the outcome of the ``predicate`` determines if the check is succesfull or a failure.