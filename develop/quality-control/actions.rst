Actions
-------

**Explicit**

Each rule directive has an action. You can specify this explicitly:

.. code-block:: yaml

   - action: validate

**Implicit**

With many rules it’s implicit which rule is applied. IN the following
example, the action is implied by the ‘predicate’ property,

.. code-block:: yaml

   - action: predicate
   - predicate: id.exists()

So the line with ``action: predicate`` provides no new information and
can be left out:

.. code-block:: yaml

   - predicate: id.exists()

In the sub pages you can find the full list of all actions:

.. toctree::
    :maxdepth: 1
    
    actions/include
    actions/validate
    actions/predicate
    actions/unique
    actions/unit-testing
    actions/same
