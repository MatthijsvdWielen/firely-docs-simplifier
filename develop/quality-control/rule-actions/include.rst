Include
-------

If you run a ruleset file (a ``*.rules.yaml``), by default, no other
rules will be run. This is done to give you maximum control, and allow
you to run individual rulesets.

But, there are situations where you would like to run an aditional set
of rules, that you have defined elsewhere (in another file). Imagine you
have a ruleset to ‘check broken links’, but want to run all the default
rules as a first step. You can achieve this by using the ‘include’
action.

Include action
~~~~~~~~~~~~~~

You include the default ruleset or any other ruleset in a , you can
speficy this in a single directive.

.. code-block:: yaml

   - include: <name>

For example, this will include the default ruleset:

.. code-block:: yaml

   - include: default

And this will include the custom ruleset file ``myrules.rules.yaml``

.. code-block:: yaml

   - include: myrules

Alternatively these will do the same:

.. code-block:: yaml

   - include: myrules.rules.yaml

   - include: some-directory/myrules.rules.yaml

It is not an issue to have multiple references to the same file, because
rules will be indexed by their name.