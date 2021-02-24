Generic properties
------------------

There is a set of properties that are applicable to each rule. , like
``name``, ``status``, ``error`` and ``error-message``.

.. code-block:: yaml

   # fields that are applicable to all rules:
   - name: id-mandatory
     status: "Message during processing"
     error: CS100
     error-message: "message when failed. Can contain placeholders"

Some rules apply to most but not all rules, like ``filter``.

**Properties**

See the index below for an elaboration about each property:

.. toctree::
    :maxdepth: 1

    generic-properties/name.rst
    generic-properties/status.rst
    generic-properties/errors.rst
    generic-properties/filters.rst
