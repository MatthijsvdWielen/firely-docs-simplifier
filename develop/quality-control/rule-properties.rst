Rule properties
---------------

The following are examples of properties applicable to each rule:

.. code-block:: yaml

   # fields that are applicable to all rules:
   - name: id-mandatory
     status: "Message during processing"
     error: CS100
     error-message: "message when failed. Can contain placeholders"

.. contents::
  :depth: 2
  :local:

Name
~~~~

Every rule has it’s own unique name. It must be a single word, but it may
contain hyphens or underscores. If you do not provide a name, it 
will be generated with a generic tally name: ``rule-1``, ``rule-2``, etc.

See below a hypothetical file ``company.rules.yaml``.

.. code-block:: yaml

   - name: acme-publisher
     predicate: StructureDefinition.publisher = 'ACME'

Within this series, the rule has the name ``acme-publisher``. And in the
Quality Control engine, it will be identified as
``myrules.acme-publisher``, based on the series name ``company`` and the
rule name ``acme-publisher``.

The name and the series where the rule belongs to, together define the
rule identifier by which it can be referred to.

Status
~~~~~~

Provides optional textual feedback in the user interface and the log, while
running the Quality Control. It tells the user/reader what rule
directive is being executed. If no status is provided one will be generated
automatically.

.. code-block:: yaml

   - predicate: id.exists()
     status: "All resources must have an id according to our organization"

Errors
~~~~~~

The ``error`` and ``error-message`` properties allow you to customize
error messages. For every issue encountered by this rule, the error will
be defined by these two properties.

Error-message
=============

The ``error-message`` allows you to define a custom error message. For
some rules, like bulk validation this is not advised, but if you create
your own rules like a predicate, it might help the receiver of the issue
to have a more concrete explanation, other than that the predicate
failed on a resource. For example:

.. code-block:: yaml

   - predicate: id.exists()

The message that this rule would produce will look something like this:
“Predicate failed for rule-3”. You can improve this a lot by providing a
custom message:

.. code-block:: yaml

   - predicate: id.exists()
     error-message: This resource does not have an id

The quality control engine is always able to generate an error message.
If no error message is provided, a standard error is generated.

Error
=====

The ``error`` property allows you to set the error code or system - and
- code, separated with a vertical bar ``|``:

.. code-block:: yaml

   - error: https://mysystem.org/errors|ERROR1
     ..

   - error: ERROR1
     ..

.. _qc_properties_suppress:

Suppress
========

With ``suppress`` you can tell the rule not to see certain error codes as a
failure.

.. code-block:: yaml

   - suppress: https://mysystem.org/errors #Suppress an entire error code system
   - suppress: https://mysystem.org/errors|ERROR1 #Suppress a specific error code
   - suppress: ERROR1 #Suppress an error code, regardless of code system
   - suppress: #Suppress multiple error codes
      - ERROR1
      - ERROR2

Examples of suppressing `errors from the Firely .NET SDK <https://simplifier.net/docs/firely-net-sdk>`_:

.. code-block:: yaml

   - suppress:
      - http://hl7.org/fhir/dotnet-api-operation-outcome|6005 #Or just 6005, since the code system is optional
      - eld-16

Even codes from Simplifier.net Quality Control itself can be suppressed. Their code systems are: 

- Generic errors: https://simplifier.net/qc/errors/generic
- Default user generated errors (unless they specify their own system): https://simplifier.net/qc/errors/custom
- Rule errors (invalid rules): https://simplifier.net/qc/errors/rules
- Evaluation errors (outcomes of rules): https://simplifier.net/qc/errors/evaluation
