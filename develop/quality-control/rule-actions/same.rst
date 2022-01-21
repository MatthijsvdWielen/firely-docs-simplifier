Same
====


The ``same`` rule makes sure all values at a specific location in a
resource are the same. You can provide any FhirPath expression, as long
as it produces a single value.

In many cases, the actual value of a mandatory field is known, like the
publisher of a project. But in some scenario’s that field is not known.
For example: it’s it’s a good practice to have the same version for all
Resources in a project. But that value changes over time, so the
specific value is not known to the Quality Control Engine of Simplifier.

Example
-------

.. code-block:: yaml

   - files: /resources/*.xml
     # action: same # Can be added for consistency, but not necessary
     same: id
