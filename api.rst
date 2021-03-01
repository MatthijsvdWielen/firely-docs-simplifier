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

The `Package Server API <https://simplifier.net/docs/package-server>`_ allows you to
search and retrieve FHIR packages.

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
-----------------
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
