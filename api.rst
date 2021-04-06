.. _simpl_endpoint:

API Endpoint
^^^^^^^^^^^^

Simplifier.net has multiple APIs available for interacting with the platform and your content on it:

.. contents::
  :depth: 2
  :local:

To test these APIs you can see `our Postman API documentation <https://documenter.getpostman.com/view/8381182/TW6xo8Yv>`_ 
or directly run the following Postman collection:

|Run in Postman|

.. |Run in Postman| image:: https://run.pstmn.io/button.svg
   :target: https://app.getpostman.com/run-collection/da066eb30fb57e2c9865

Authentication
""""""""""""""

JWT authentication
==================

The Simplifier API endpoints are available for Simplifier users based on JWT authentication. 

First retrieve a JWT token from Simplifier. This works with a POST at 
https://api.simplifier.net/token with your account details in the message body 
in JSON format. Header should be ``Content-Type: application/json``. 
A ``token`` and ``refreshToken`` will be returned.

::
  
  POST https://api.simplifier.net/token 
  
  Header:
  Content-Type: application/json

  Body:
    {
      "Email": "youremail@example.com",
      "Password": "your password"
    }
    
Next, you can use this token with an authorization header that includes 
your retrieved token as shown below. The token is valid for a limited time.

::
  
  GET https://api.simplifier.net/<yourproject>/zip
  
  Header:
  Authorization: Bearer <access_token> 

Once your token is expired you can use the ``refreshToken`` to retrieve new
token and refreshToken pair. The refreshToken has a much longer expiry time.

::
  
  POST https://api.simplifier.net/token/refresh
  
  Header:
  Content-Type: application/json

  Body:
    {
      "Token": <token>,
      "RefreshToken": <refreshToken>
    }

Your outstanding refreshTokens are visible at https://simplifier.net/myrefreshtokens,
where you can choose to revoke them if you no longer wish them to be valid.

Basic Auth
==========

The ZIP and FHIR API endpoints alternatively also support authentication with 
Basic Auth directly. However, going forward we recommend the JWT authentication instead.

Features API
""""""""""""

The Simplifier Features API allows you to retrieve feautures for your account on the
platform, like the feautures your plan gives you access to, the projects you have 
accesss to and the files within them.

The currently supported calls include:

* GET https://api.simplifier.net/myfeatures
  
  Return the features that this user has a right to use in their current plan.

* GET https://api.simplifier.net/api/v2/myprojects
  
  Return the Simplifier.net projects for the user.
  
* GET https://api.simplifier.net/api/v3/projects/{{project_urlkey}}/Files
  
  Return a list of files contained in the Simplifier.net project.


Package Server API
""""""""""""""""""

Simplifier has an package server API, that is compliant to the FHIR NPM package standard. It serves all FHIR packages created in Simplifier. 

API Endpoint
============

The api endpoint of the Simplifier FHIR package Server is:

https://packages.simplifier.net/

HL7 FHIR Package Server
=======================

Simplifier also hosts the same package API for the FHIR package server. The root URL for this server is:

https://packages.fhir.org/

Available API Endpoints
"""""""""""""""""""""""

Download Packages
=================
The Simplifier FHIR Package server allows you to download a specific version of a package. You can download any FHIR package by directly accessing this URL in your browser:

::

https://packages.simplifier.net/<package-name>/<package-version>

For example:

::

https://packages.simplifier.net/hl7.fhir.r3.core/3.0.2

NPM compatible endpoint:

There is also an NPM compatible endpoint, which allows sligtly less trivial, but allows you to install FHIR package using any NPM client.

::

https://packages.simplifier.net/<name>/-/<package-name>-<package-version>.tgz

The above example, then becomes:

::

https://packages.simplifier.net/hl7.fhir.r3.core/-/hl7.fhir.r3.core-3.0.2.tgz

Version Listing
===============
In order to discover the available versions of a package, you can do a GET on this endpoint.

https://packages.simplifier.net/<package-name>

The payload is compliant with the NPM package version listing.

The dist-tags element will provide tags on certain versions, like the label of which version is the latest. Note: In calculating latest the highest stable semver version is used, not the most recently published version.
Example payload

Here is an example output when requesting https://packages.simplifier.net/simplifier.core.stu3

::

{
    "_id":"Simplifier.Core.STU3",
    "name":"Simplifier.Core.STU3",
    "description":"This is a meta package that contains the FHIR Core STU3 Spec...",
    "dist-tags": {"latest":"3.0.3"},
    "versions": { 
        "3.0.1": {
            "name": "Simplifier.Core.STU3",
            "version": "3.0.1",
            "description":"None.",
            "url":"https://packages.simplifier.net/Simplifier.Core.STU3/3.0.1"},
        "3.0.2": {
            "name": "Simplifier.Core.STU3",
            "version": "3.0.2", 
            "description": "Contains a fix for invariant sdf-20 (no slici...",        
            "url": "https://packages.simplifier.net/Simplifier.Core.STU3/3.0.2"},
        "3.0.3": {
            "name":"Simplifier.Core.STU3", 
            "version":"3.0.3",
            "description": "None.",
            "url": "https://packages.simplifier.net/Simplifier.Core.STU3/3.0.3"
        }
    }
}
..

Package Search
==============
Because we want to make package search as useful as possible for the FHIR usecase, we are not following the NPM standard, but we implement a lean endpoint that can be used for intellisense (dropdown) and a search that can deal with the most important FHIR relevant search queries: canonicals and FHIR versions.

Query
-----
The implementation is this:

https://packages.simplifier.net/catalog?<parameters>

We currently support these four parameters:
Name

With the name= parameter, you can search for any package where the name contains the given value. The match is anywhere in the string, so searching for name=r3 will match hl7.fhir.r3.core.
Canonical

With the canonical= parameter, you can search for any package that contains a resource that has the canonical url of the given value. The canonical needs to be an exact match. The search does not support partial matching.
Fhir Version

The fhirversion= parameter, filters your search results for the given FHIR version. This value can be of format strict Rx format: R3, R4, but also understands common monikers like stu3, dstu2.
Prerelease

The prerelease= parameter allows you to include non-official package releases in your search results. The parameter allows two values: true and false. The default value is false.

Response
--------
The response of this API call is a JSON array that contains the following values:

    package name,
    package description
    FHIR version.

Example output for the search https://simplifier.net/catalog?name=core:

[
    {
        "Name": "Simplifier.Core.STU3.Resources",
        "Description": "These are the STU3 Core Profile StructureDefini...",
        "FhirVersion": "STU3"
    },
    {
        "Name": "simplifier.core.r4.resources",
        "Description": "The HL7 FHIR core R4 Specification Base Resources",
        "FhirVersion": "R4"
    },
    {
        "Name": "hl7.fhir.r2.core",
        "Description": "Definitions (API, structures and terminologies ...",
        "FhirVersion": "DSTU2" 
    },
    ...
]

Package version Response
------------------------
**PROPOSAL - Not implemented yet**

A version= parameter that accepts a boolean true or false. The default is false.

When set to true, the search will return all versions of packages that match the criteria.

Example output:

https://simplifier.net/catalog?name=core:

[
    {
        "Name": "hl7.fhir.r3.core",
        "Description": "These are the STU3 Core Profile StructureDefini...",
        "FhirVersion": "STU3"
        "Version": "3.0.1"
    },
    {
        "Name": "hl7.fhir.r3.core",
        "Description": "These are the STU3 Core Profile StructureDefini...",
        "FhirVersion": "STU3"
        "Version": "3.0.2"
    },
    {
        "Name": "hl7.fhir.r4.core",
        "Description": "These are the R4 Core Profile StructureDefini...",
        "FhirVersion": "STU3"
        "Version": "4.0.1"
    },
    ...
]


Open API / Swagger documentation
================================

Try the Simplifier.net FHIR Package API `live from the SwaggerHub documentation. <https://app.swaggerhub.com/apis-docs/firely/Simplifier.net_FHIR_Package_API/1.0.1>`_

**Note**: It is not possible to create a package using the API. For more information on how to create a package please read our `documentation <https://docs.fire.ly/projects/Simplifier/simplifierPackages.html#publish-packages>`_ on packages. 

Project FHIR API
""""""""""""""""

The endpoint of a Simplifier.net project can be used to search for resources in the project 
or to read, create and update resources with a FHIR client. History 
searches are also supported. To retrieve the endpoint of a project in Simplifier 
click on ``API`` in the top right menu when visiting either the 
:ref:`project <project-page>` or :ref:`resource <resource-page>` page. 
The below image shows the location.

.. image:: ./images/ProjectApiLocation.png

It supports all the API operations like reading, creating or deleting a resource and search.

You can also use this to point :ref:`Firely Server<main_docs:vonk_index>` 
to a Simplifier.net project via the FHIR API to import the conformance resources. 
Either via a (manual) import operation or by configuration
of the project's endpoint and authentication in the appsettings.

Project ZIP API
"""""""""""""""
The project ZIP API is available at project level. You can use the ZIP endpoint 
for synchronization of a complete project. With an HTTP tool you can use 
GET or PUT on https://api.simplifier.net/<yourproject>/zip to retrieve or
update your project in zipped form.

.. image:: ./images/ProjectApiLocation.png

Global FHIR API
"""""""""""""""

.. TODO: Should we keep the global API?

Using the global Simplifier FHIR API, users can search for all resources in Simplifier. For example, the request ``GET https://stu3.simplifier.net/open/Patient`` can be used to retrieve all (STU3) Patient resources from Simplifier. The global Simplifier endpoint of your resource is available at the resource page beneath the API icon. All resources have a globally unique GUID.

.. image:: ./images/ResourceGlobalEndpoint.PNG


Search Parameters 
=================

It is possible to use search parameters and search result parameter to filter the results from Simplifier. All parameters, with the exception of 'description', follow the STU3 FHIR specification. The following parameters are implemented:

Search paramters

=============  ==========  =============================================================   ================================
Name           Type        Description                                                     Expression
=============  ==========  =============================================================   ================================
url            uri         The uri that identifies the structure definition                StructureDefinition.url
type           token       Type defined or constrained by this structure                   StructureDefinition.type
status         token       The current status of the structure definition                  StructureDefinition.status
publisher      string      Name of the publisher of the structure definition               StructureDefinition.publisher
jurisdiction   token       Intended jurisdiction for the structure definition              StructureDefinition.jurisdiction
kind           token       (primitive-type | complex-type | resource | logical) |br|       StructureDefinition.kind
                           Only accepted value is "logical", the rest of the |br|
                           values will return non-logical model resources. |br|
                           (So this parameter will distinguish between |br|
                           profiles and logical models)
description    string      Will look at the publication description used in |br|           StructureDefinition.description
                           Simplifier (set either manually by user or generated |br| 
                           automatically using the FHIRpath metadata expressions |br|
                           written in project settings), not the description |br|
                           value inside the Confromance Resources. |br|                
=============  ==========  =============================================================   ================================

Search result parameters

=============  ============================================================================================    
Name           Description                                           
=============  ============================================================================================    
_sort          Only default "lastUpdated" is implemented.     
_count         Default value is "false". The parameter _count is defined as a hint to 
               Simplifier regarding how many resources should be returned in a single page.       
_summary       The _summary parameter requests the server to return
               a subset of the resource. 
=============  ============================================================================================    

.. |br| raw:: html

   <br />

Examples

* type |br|

::

  GET https://stu3.simplifier.net/<yourproject>/Patient
  
* description |br|

::

  GET https://stu3.simplifier.net/<yourproject>/StructureDefinition?description:contains=<searchedterm>

* _summary |br|

::

  GET https://stu3.simplifier.net/<yourproject>/StructureDefinition?_summary=true
