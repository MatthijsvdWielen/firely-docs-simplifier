Examples
--------

Here are some example rules, that you might consider when writing your
own rules:

Validating resources in a single folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This example validates all resources in a single folder. It also
suppresses all parsing errors

.. code-block:: yaml

   - action: validate
     files: /examples/*.xml
     suppress: https://simplifier.net/qc/errors/evaluation|PARSING
