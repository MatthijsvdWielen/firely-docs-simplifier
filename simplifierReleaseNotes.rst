.. _release_notes:

Release Notes
=============

This page contains the release notes of the current major version of simplifier.net (29.5.0), as well as release notes from previous releases.

Current release
~~~~~~~~~~~~~~~

Release 29.5.0, December 15th, 2022
-----------------------------------

Features
^^^^^^^^

#. FHIRPath: A FHIRPath playground is now available at https://simplifier.net/fhirpath
#. Validator: A validator playground is now available at https://simplifier.net/validator
#. IG editor: You can now reference resources in your IG using resourceType/ID of the resource. This is helpful for e.g. linking to specific examples.
#. Github: It is now possible to link multiple projects to one Github repository branch.
#. Reporting issues: The process for submitting issues has been made easier by allowing users that are not yet logged in to see the issue button. Upon clicking the issue button they will be guided to log in.
#. Packages: Unlisted packages have been made more easily distinguishable.
#. Beta: The package graph visualisation page is now available for beta users.

Bugfixes
^^^^^^^^

#. Firely server: In the previous version of simplifier.net users with MAC OS experienced that after trying to download and run the project as a FHIR server in Docker, the CapabilityStatement of Firely server was not loading correctly on first try. This issue was caused by the Windows OS specific seperators in the Powershell scripts that are downloaded when pressing the yellow download button. This issue is now fixed and users should be able to succesfully try out Firely server via this route on MAC OS, with the CapabilityStatement loeding correctly on first try.
#. IG: the use of multiple pagelinks within one sentence in the IG previously led to rendering issues. This has been fixed and it is now possible to use multiple pagelinks within one sentence without breakage or error.

Known issues
^^^^^^^^^^^^

As of this moment no issues are listed for this version of simplifier yet. If you come across an issue and it is not listed here, please contact us at
simplifier@fire.ly or (for customers) `our premium support desk <https://firely.atlassian.net/servicedesk/customer/portals>`_. 

If you experience service lags in Simplifier.net, it could be that services are offline. You can check if this is the case on `Simplifier.net's status website <https://status.simplifier.net/>`_.
It is also possible to raise an issue from here.

All our tooling is built on top of the official Firely .NET SDK developed and managed by Firely. The `SDK is open source
and maintained on Github <https://github.com/FirelyTeam/firely-net-sdk/>`_ and `issues are publicly tracked there <https://github.com/FirelyTeam/firely-net-sdk/issues>`_.

HL7 is maintaining a `known issue list for the FHIR specifications on
their Confluence <https://confluence.hl7.org/display/FHIR/Known+Issues+with+the+published+FHIR+Specifications>`_.

Previous releases
~~~~~~~~~~~~~~~~~

Release 29.4.0, October 5th, 2022
---------------------------------

Features
^^^^^^^^

#. IG editor: You can now switch between pages and files. The layout of the IG editor has been cleaned up and users now have more control over metadata and the configuration files behind the rendering. It is also possible to use PlantUML in the IG now.
#. Captcha: We added captcha to Simplifier.net.
#. Index management: We continously work on improving our search, but that often requires re-indexing. Simplifier now has an Index management page, to manage and switch indexes.
#. Cloud upgrade: Simplifier's cloud storage has been upgraded to assure quick rendering and improved user experience.
#. Zullip: Simplifier now has a bot on `Zulip <https://chat.fhir.org/#narrow/stream/328836-tooling.2FPackage-Crawlers>`_ where we publish the logs of the Package metafeed burner. It is possible to find here if and why a package was not imported.


Bugfixes
^^^^^^^^

#. IG: after duplicating an IG, sometimes the pages were out of order. This has been fixed.
#. Bake: When trying to upload a a zip file in Bake manage settings, the user is given the option to open project settings. Clicking on the project settings to navigate to the project settings page gave an error. This is now fixed.
#. Filepaths: Filepaths in packages are now constrained to be unique.
#. Deleting guides: Users experienced they were getting stuck in the console when trying to delete guides. This is no longer the case.
#. IG: If you have similar names in the IG Editor subfolders, double clicking on the other subfolder having similar name would reset the name to the older name automatically. This is no longer the case.
#. Uploading zips: Error messaging upon uploading a ZIP file where two resources have the same ID, but with different capitalization has been improved for clarity.

Release 29.3.0, July 13th, 2022
-------------------------------

In this released we worked on improvements and feedback of our new search engine.

Features
^^^^^^^^

#. Search: You can now search within content, such as IG's.
#. Search: Search ranking has now been improved.
#. Search: The interface of the search bar has been improved.
#. Search: Search drill-down options have been added.
#. Search: It is now possible to search within an Organization.
#. Snippets: It is possible to add Snippets to the IG.

Bugfixes
^^^^^^^^

#.  Search: Searching on a resource name would not give a result. This is now fixed.
#.  IG: Renaming folders in the IG would lead to child pages missing. This has been fixed.
#.  Search: Previously, when users searched within a token and type a value that is not available or without a search result, they did not receive any feedback. Users now get a message that no search results are available.
#.  Search: When searching within a project and a result is given with just 2 results, “load more results“ was displayed. This can be misleading since there is no more entries to be displayed. This has been fixed to only show when there are more than 10 entries in the search results.
#.  Search: Previously, guides sometimes were not indexed and therefore not discoverable by the search engine. The indexing on guides has been improved, allowing users to find guides more quickly.
#.  Logs: When the import log LogLevel is set on 'Debug' it would only show Debug messages. This is now set to be more verbose.
#.  Search: Searching from home/top search bar would lead to a 404 error and searching on just a filter would lead to "You have not selected any filters. Please provide a search term." This is now been fixed.
#.  Search: Keyboard navigation for searching has been fixed.
#.  Search: Filter token behaviour has been improved.
#.  Search: Selecting filters only would lead to search results, this has been fixed to only include results when a search term is added.


Release 29.2.0, June 17th, 2022
-------------------------------

Features
^^^^^^^^

#. Bake: The first true beta release of Bake. When you have package.bake.yaml in your project, it will be used to create your package. If you don't have it, simplifier uses the existing configuration system. This is as of yet a Beta release.
#. YAML gen: We have made our example generator agnostic, by moving it into the generator engine that we build for YamlGen. You can now define examples that are fully defined by you, or partially or completely generated. Some parts of the extended syntax are still in beta. You can use YamlGen in Bake. You can try out YamlGen here: https://simplifier.net/yamlgen
#. Plant UML: We now have a solid and stable Plant UML (micro) service in Simplifier, that you can run in our playground: https://simplifier.net/plantuml.
#. FSH: Our FSH service now has a stable implementation. It is in beta and still has some configuration limitations, but it's usage is stable. You can use FSH in Bake to generate resources for your package. You can try out the FSH service here: https://simplifier.net/fsh.

Release 29.1.0, May 31st, 2022
-------------------------------
This release focussed on improving the search function in Simplifier.net.

Features
^^^^^^^^

#. Search: ability to search guides, guide pages, packages and package files in addition to projects and organizations.
#. Search: Improved indexing for better search performance.
#. Search: Rendering of search results for Organizations has been improved.

Bugfixes
^^^^^^^^

#. License: Site admins were no longer able to change license features on Simplifier. This has been fixed.
#. Search: Search pages were not always showing options for other FHIR versions, this has been fixed.
#. Package: Error messaging upon trying to publish a package which already exists has been improved.
 

Release 28.6.0, April 29th, 2022
--------------------------------

Features
^^^^^^^^

#. .NET 6: Simplifier.net was upgraded to .NET 6.
#. Rendering: Simplifier's rendering machine has been improved and the rendering library has been made fully asynchronous for better performance.
#. New placeholders: For a long time we've had a ``{{render}}`` placeholder in the guide editor, that chooses the most typical style of rendering given a resource. 
   This used to be a tree for StructureDefinitions, and a narrative for examples. We have now added two more placeholders:
      - The ``{{tree}}``` placeholder now also renders instance tree for examples.
      - The  ``{{narrative}}`` placeholder now always renders the narrative, even if it's empty.
#. FSH playground: We have added a FSH playground. This was live before as an alfa release, but it's now generally available as a beta release. You can find the FSH playground here: simplifier.net/fsh
#. Plant-UML Playground: Plant UML is now available as a playground, you can find it here: simplifier.net/plantuml
#. YAMLGen Playground: With YAML gen you can write standard YAML to generate FHIR resources. Our YAMLgen playground is the first (alfa) release in our effort to enable our users in writing examples. You can try it out here: https://simplifier.net/yamlgen.

Bugfixes
^^^^^^^^

#. JSON rendering: Simplifier rendered JSON did not escape newlines/special characters correctly. This has been fixed.
#. IG export: Users experienced several issues when exporting an IG, this is now fixed.




