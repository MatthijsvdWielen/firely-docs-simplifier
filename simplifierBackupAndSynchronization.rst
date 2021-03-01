Backup and Synchronization
""""""""""""""""""""""""""
The Simplifier team has a solid backup process. We have continuous backup by our cloud storage provider. In addition, we perform a weekly manual backup.
Please note that this is for emergency situations, and you should not require to depend or rely on that from a user perspective.

Customers may want to have a possibility to backup whatever content they have on Simplifier (or more generally in the cloud for that matter). Here are some ways to make sure your data is regularly backed up:

API endpoint
-------------
Each Simplifier project has a :ref:`FHIR endpoint and Zip endpoint<simpl_endpoint>`:

* With the FHIR endpoint, you can get (or restore) a specific resource from your project using any FHIR client. You can also get all resources from a specific resource type.
* With the Zip endpoint you can download or upload a zip folder containing all resources from a project.


Download
--------
You can always download the current versions of all resources, including or excluding texts and images, from the Download drop-down on your project page.
Filepaths are preserved from GitHub and the regular upload. Resources that are initially uploaded through the FHIR endpoint will have a persistent filename, but no absolute path.

Client tool
-----------
We provide a client tool called Firely Terminal that allows easy and automated synchronization and backup. :doc:`Firely Terminal <firely_terminal_docs:index>` uses the simplifier ZIP API and was built to assist CI/CD scenarios.

All you need is this command line syntax: ``fhir sync <projectname> -down``

`Download it for free
<https://simplifier.net/downloads/firely-terminal>`_.

Atom feed
---------
If you want to automate backup on any updated file, you can use the atom feed of the project log to trigger your client backup.

Webhook
-------
This is not implemented yet, but will be put on our roadmap if there is enough demand.


.. |br| raw:: html

   <br />
