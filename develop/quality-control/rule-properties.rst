Rule properties
---------------

There is a set of properties that are applicable to each rule. , like
``name``, ``status``, ``error`` and ``error-message``.

.. code-block:: yaml

   # fields that are applicable to all rules:
   - name: id-mandatory
     status: "Message during processing"
     error: CS100
     error-message: "message when failed. Can contain placeholders"

Some rules apply to most but not all rules, like ``filter``.

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

Error
=====

The ``error`` property allows you to set the error code or system - and
- code, separated with a vertical bar ``|``:

.. code-block:: yaml

   - error: https://mysystem.org/errors|ERROR1
     ..

   - error: ERROR1
     ..

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

Filters
~~~~~~~

There are several filters that you can use to select to which files in
your project a rule should apply. These filter properties are applicable
to most rules, but not all.

File filters
============

.. warning::

   This feature will be released around end of feb. 2021

You can filter any file bassed on a globbing pattern as you may now from
your own computer file system.

A specific file:

.. code-block:: yaml

   # this rule applies to exactly one file:
   - action: validate
   - file: example-patient.json

All xml files; make sure that all xml examples have a profile field:

.. code-block:: yaml

   - predicate: meta.profile.exists()
     files: example-*.xml

FHIRPath Filters
================

This filter allows you to filter a resource on a FHIRPath predicate.
That means that only files for which the FHIRPath statement is true,
remain in your selection.

The filter property understands several types of values:

- Any Resource Category (Resource, Example Profile, etc) [NOT IMPLEMENTED YET]
- Any Resource Type (Patient, Organization)
- Any FHIRPath statement that results in an unambiguous true or false
- Any FHIRPath statement that results in a single value (if the value is there, it’s a match)

For more information about FHIRPath, see the `FHIRPath standard`_.

An example true/false expression.

.. code-block:: yaml

   # This will select all files that have an id.
   - filter: id.exists()

An example of a existence match:

.. code-block:: yaml

   # Resources that have a meta.profile field:
   - filter: meta.profile

Resource types are a valid FHIRPath expression. So This wil select all
Patient resources.

.. code-block:: yaml

   - filter: Patient

Filtering on broader categories is planned, but not yet implemented:

.. code-block:: yaml

   - filter: Profile 
   - filter: Extension

Applying multiple filters
=========================

You can specify more than one filter, per rule. Only files (resources)
that fall in both filters will be part of the rule evaluation.

This example will filter in all examples that have a profile:

.. code-block:: yaml

   - action: validate
     files: examples/*-example.xml
     filter: meta.profile

.. _FHIRPath standard: http://hl7.org/FHIRPath/