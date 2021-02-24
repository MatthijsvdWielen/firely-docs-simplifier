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
