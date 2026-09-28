.. _publishing:

Publishing a specification
==========================

Most FHIR specifications on Simplifier go through the same steps, from the first profile to a published implementation guide. This page lists them in order, with links to the pages that cover each step.

#. **Profile your resources.** Write your profiles, extensions, value sets and examples with the tool that suits your team:

   - `Forge <https://fire.ly/products/forge/>`_, Firely's visual profiling tool, which :doc:`syncs a local folder <adding_content/forge>` to your project.
   - FHIR Shorthand (FSH). Compile it with SUSHI and sync the generated resources, or add the ``.fsh`` files to your project and let a :ref:`bake pipeline <bake>` run SUSHI when you create a package.
   - :ref:`YamlGen <yamlgen>`, to generate resources from compact YAML.
   - Any other tool that produces FHIR JSON or XML.

#. **Sync them to Simplifier.** Get the resources into a :ref:`project <Project_Page>`, by hand or automatically from GitHub, Forge or Firely Terminal. :ref:`adding_content` helps you choose. If your profiles build on other specifications, add those packages as :doc:`dependencies <dependencies/managing-dependencies>`.

#. **Check the quality.** Run :ref:`Quality Control <QC>` rules on your project to validate your resources and check your own conventions before you release.

#. **Release a package.** :ref:`Create a FHIR package <package_management>` from your project, so implementers can install exactly this version. Read the :ref:`package policy <PackageCreationCheck>` first, as a released package cannot be deleted. Use a :ref:`bake pipeline <bake>` to control what goes into the package, and :ref:`package feeds <package_feeds>` to release it privately.

#. **Publish an implementation guide.** :ref:`Write your guide <implementation_guide>` in the IG editor while you work on your resources, and :ref:`publish <published_guides>` a version when you release.

Releasing a version
-------------------

While you work, your guide renders live from your project. For a release, base the guide on the package you release instead, so the published guide shows exactly the resources in that package:

#. :ref:`Release a package <package_management>` from your project.
#. Open your guide in the IG editor, click ``Settings`` (the gear icon) and set the guide's scope to the package version you just released. Check that the guide renders as expected.
#. :ref:`Publish the guide <published_guides>`. You can also make it the default guide, which is where people land when they open the guide URL without a version number.
#. Set the guide's scope back to your project (``current``) and continue with the next version of both.

A package version is final: you can unlist it, but not change it. A published guide can be overwritable, so you can fix a typo without a new version number. See :ref:`published_guides` for how guide and package versions relate.
