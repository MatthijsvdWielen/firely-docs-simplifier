Filters
=======

There are several filters that you can use to select to which files in
your project a rule should apply. These filter properties are applicable
to most rules, but not all.

File(s)
-------

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

Filter
------

This filter allows you to filter a resource on a FhirPath predicate.
That means that only files for which the FhirPath statement is true,
remain in your selection.

The filter property understands several types of values:

- Any Resource Category (Resource, Example Profile, etc) [NOT IMPLEMENTED YET]
- Any Resource Type (Patient, Organization)
- Any FhirPath statement that results in an unambiguous true or false
- Any FhirPath statement that results in a single value (if the value is there, it’s a match)

For more information about FhirPath, see the `FhirPath standard`_.


An example true/false expression.

.. code-block:: yaml

   This will select all files that have an id.
   - filter: id.exists()

An example of a existence match:

.. code-block:: yaml

   # Resources that have a meta.profile field:
   - meta.profile

Resource types are a valid FhirPath expression. So This wil select all
Patient resources.

.. code-block:: yaml

   - filter: Patient

Category
--------

This is not yet implemented. But planned.

.. code-block:: yaml

   - filter: Profile 
   - filter: Extension

Multiple filters
----------------

You can specify more than one filter, per rule. Only files (resources)
that fall in both filters will be part of the rule evaluation.

This example will filter in all examples that have a profile:

.. code-block:: yaml

   - action: validate
     files: examples/*-example.xml
     filter: meta.profile

.. _FhirPath standard: http://hl7.org/fhirpath/