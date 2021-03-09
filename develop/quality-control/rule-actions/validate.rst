.. _qc_actions_validate:

Validate
~~~~~~~~

.. figure:: /images/Simplifier-validate-results.png
    :alt: The results of bulk validation

    The results of bulk validation in a Simplifier.net project

The validate action, validates all resources against the base profiles
and their stated base claims, set in ``meta.profile``.

.. code-block:: yaml

   - action: validate # Since validate has no parameters the action parameter is always needed
