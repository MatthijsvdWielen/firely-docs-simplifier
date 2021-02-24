Predicate
---------

The predicate rule, gives an error for each resource where the predicate
evaluates to false.

Example:
~~~~~~~~

.. code-block:: yaml

   - action: predicate
     predicate: id.exists()
     error: This resource does not have an id
