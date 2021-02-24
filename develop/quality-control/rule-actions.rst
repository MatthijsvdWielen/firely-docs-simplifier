Rule actions
------------

Each rule directive has an action. You can specify this **explicitly**:

.. code-block:: yaml

   - action: validate

With many rules it’s **implicit** which rule is applied. In the following
example, the action is implied by the ‘predicate’ property,

.. code-block:: yaml

   - action: predicate
   - predicate: id.exists()

So, the line with ``action: predicate`` provides no new information and
can be left out:

.. code-block:: yaml

   - predicate: id.exists()

In the sub pages you can find the full list of all actions:

.. toctree::
   :maxdepth: 1
    
   rule-actions/validate
   rule-actions/predicate
   rule-actions/unique
   rule-actions/same
   rule-actions/include
   rule-actions/unit-testing
   