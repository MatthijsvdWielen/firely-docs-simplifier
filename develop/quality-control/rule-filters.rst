Rule filters
~~~~~~~~~~~~

There are several filters that you can use to select to which files in
your project a rule should apply. These filter properties are applicable
to most rules, but not all.

.. contents::
  :depth: 2
  :local:

.. _qc_filters_fhirpath:

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

QC supports FHIRPath normative v2.0.0. For more information about FHIRPath, see the `FHIRPath standard`_.

An example true/false expression.

.. code-block:: yaml

   # This will select all files that have an id.
   - filter: id.exists()

An example of a existence match:

.. code-block:: yaml

   # Resources that have a meta.profile field:
   - filter: meta.profile

See :ref:`predicate <qc_filters_fhirpath>` for using the same type of FHIRPath statements
to check if selected resources are correct according to your rules.


Resource filters
================

.. warning::

   This feature will be released around end of feb. 2021

Resource types are a valid FHIRPath expression. So, this wil select all
Patient resources.

.. code-block:: yaml

   - filter: Patient

Filtering on broader categories is planned, but not yet implemented:

.. code-block:: yaml

   - filter: Profile #All StructureDefinitions, except Extensions
   - filter: Extension #Only StructureDefinitions that are of type Extension
   - filter: Resource #Everything that can be parsed by us as a resource
   - filter: Type #All data types
   - filter: Terminology #ValueSet, CodeSystem, NamingSystem, ConceptMap
   - filter: Conformance #Everything that's not an example instance

File filters
============

.. warning::

   This feature will be released around end of feb. 2021

You can filter any file with the ``file`` or ``files`` filter, based on a globbing
pattern as you may now from your own computer file system.

Validating one specific ``file``:

.. code-block:: yaml

   # this rule applies to exactly one file:
   - file: example-patient.json
     action: validate

Checking for all example xml ``files`` that they have a profile field:

.. code-block:: yaml

   - files: example-*.xml
     predicate: meta.profile.exists()

Multiple ``files`` can also be provided as a list:

.. code-block:: yaml

   - files:
      - example-patient-*.xml
      - example-organization-*.xml
     predicate: meta.profile.exists()

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