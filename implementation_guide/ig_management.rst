Implementation Guide management
===============================

IG Storage
----------

Since release 28.0 IG's all files belonging to an IG are saved in the same folder. No longer in the root of the project and not in different folders. The folder name will be the same as the IG name. 

To illustrate how this works, see the screen picture of an example IG containing three topics with one or more pages for each topic. In the project's filemanager you can see the different folder structures for each guide. 

.. image:: ../images/IGEditorStructure.png
.. image:: ../images/IGFileStorage.png

To Save your IG as a Resource, click on the ``Generate IG resource`` button in the left pane of the IG-editor. Note that it is the tree structure that is saved. Textual changes are save automatically.

.. image:: ../images/CreateIGResource.png

Export your IG
--------------

.. important::

    `This feature is available from the Professional plan and up <https://simplifier.net/pricing>`_.

To use your IG outside of Simplifier, click on the Export button next to your IG in the Guides section of your project. 

.. image:: ../images/ExportIG.png

Create a copy of your IG
------------------------

Since the release of Simplifier 28.0 it is possible to create a copy of your Implementation guide. Due to the complexity of the feature it is currently (21-01-2022) a beta release. 

.. image:: ../images/CopyGuide.png

A guide can be copied to the same project or to another project. The ``Target project:`` dropdown provides an list of all of your projects where you can create a copy of your IG. 

.. image:: ../images/TargetProject.png

You can now have multiple version of your Implementation Guide live in the same project (or different projects). You could have one IG use a release package as the scope while the development version uses the live developement version of your project. 

Migrating your legacy Guide
---------------------------

Guides created before Simplifier 28.0 are still stored in the legacy way as separate markdown files. These guides first have to be migrated to the new way of storing guides. 

.. image:: ../images/LegacyGuides.png

This functionality is also a beta release so please follow the warning and migration steps in the Migrate Guide window. In the Migrate Guide window a different target project can also be selected. Migrating a guide **does not** delete the legacy guide. 

After a guide is migrated or copied, please make sure all your internal page links and references are still working. 

Manage your IG using GitHub
---------------------------

The GitHub webhook allows managing your Implementation Guide, without using the editor itself. You can find more information on how to set this up in the :doc:`GitHub integration documentation<simplifierGithub>`.
