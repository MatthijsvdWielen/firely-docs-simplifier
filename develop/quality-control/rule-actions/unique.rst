Unique
~~~~~~

The unique constraint takes all resources (within the filter if
provided) together and checks if each of them has some value that is
unique compared to the same value of all the other resources.

.. code-block:: yaml

   - # action: unique # Can be added for consistency, but not necessary
     status: Testing if all canonicals are unique
     filter: StructureDefinition
     unique: url 

The action here is optional because it’s implicitly given by the
``unique`` property. So the minimal set of the above example would be:

.. code-block:: yaml

   - filter: StructureDefinition
     unique: urlUnique
