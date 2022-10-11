
Quality Control: Validating FHIR Projects
=========================================

.. important::

    `This feature is available from the Professional plan and up <https://simplifier.net/pricing>`_.

This specification describes how to write (and read) rules for the
Simplifier Quality Control Engine.

.. figure:: /images/simplifier-quality-control.gif
    :alt: Simplifier.net Quality Control progress bar

    Example of Quality Control being executed on a project

**Simplifier.net** and :doc:`Firely Terminal<firely_terminal_docs:index>` come with a Quality Control
engine, helping you to improve the quality of your FHIR projects. The QC
engine performs a series of rule checks on selected files in your
Simplifier.net projects, on your local computer or at every change of your
source code repository.

There are **two default rulesets** available, which run FHIR validation on all FHIR
resources and a set of rules we at Firely recommend. Additionally, you can define
any number of **custom business rules** to enforce your own custom profiling standards.

.. figure:: /images/Simplifier-rules-results.png
    :alt: The results of running a ruleset

    The results of running a ruleset in a Simplifier.net project

.. toctree::
    :maxdepth: 2
    :caption: Get started with Quality Control

    quality-control/structure
    quality-control/rule-properties
    quality-control/rule-filters
    quality-control/rule-actions
    quality-control/examples
