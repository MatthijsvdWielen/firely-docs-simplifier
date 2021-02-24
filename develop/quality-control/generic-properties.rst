Generic properties
------------------

There is a set of properties that are applicable to each rule. , like
``name`` and ``status``, ``error`` and ``error-message``.

.. code-block:: yaml

   # fields that are applicable to all rules:
   - name: id-mandatory
     code: CS100 # not sure, maybe we should have one naming system where the names are the codes.
     status: "Message during processing"
     error: "message when failed. Can contain placeholders"

Some rules apply to most but not all rules, like ``filter``.

**Properties**

See the index below for an elaboration about each property:

.. toctree::
    :maxdepth: 1

    generic-properties/filters.rst
    generic-properties/errors.rst
    generic-properties/name.rst
    generic-properties/status.rst