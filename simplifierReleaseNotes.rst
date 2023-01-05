Release Notes
=============

This page contains the release notes of the current major version of simplifier.net (v29).

Release 29.5.0, December 15th, 2022
-----------------------------------

Features
^^^^^^^^

#. FHIRPath: A FHIRPath playground is now available at https://simplifier.net/fhirpath
#. Validator: A validator playground is now available at https://simplifier.net/validator
#. IG: You can now reference resources in your IG using resourceType/ID of the resource. This is helpful for e.g. linking to specific examples.
#. Github: It is now possible to link multiple projects to one Github repository branch.
#. Reporting issues: The process for submitting issues has been made easier by allowing users that are not yet logged in to see the issue button. Upon clicking the issue button they will be guided to log in.
#. Packages: Unlisted packages have been made more easily distinguishable.
#. Beta: The package graph visualisation page is now available for beta users.

Bugfixes
^^^^^^^^

#. Firely server: In the previous version of simplifier.net users with MAC OS experienced that after trying to download and run the project as a FHIR server in Docker, the CapabilityStatement of Firely server was not loading correctly on first try. This issue was caused by the Windows OS specific seperators in the Powershell scripts that are downloaded when pressing the yellow download button. This issue is now fixed and users should be able to succesfully try out Firely server via this route on MAC OS, with the CapabilityStatement loeding correctly on first try.
#. IG: the use of multiple pagelinks within one sentence in the IG previously led to rendering issues. This has been fixed and it is now possible to use multiple pagelinks within one sentence without breakage or error.
