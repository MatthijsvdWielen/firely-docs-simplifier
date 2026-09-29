Resources
=========
Simplifier is a repository for FHIR resources. There are a multitude of resources that are available to the public including profiles, extensions, valuesets, dictionaries, mappings, examples and more.
.. _resource-page:

Resource page
"""""""""""""
You can visit the page of a resource by selecting the resource from your search results or the ``Resources`` tab in your project, or following the direct link to the resource. While viewing resources you can display information in a few different ways.  

Depending on the type of resource, the different views include:

* **Overview** – This is either a preview (e.g. texts) or a Logical view (e.g. profiles) of the resource. The Logical view of a profile includes Element names in the leftmost column followed by Flags, Cardinality, Type, and  Description & Constraints.
* **Details** – This is an easy-to-read list per element of all the details of a profile. The specification refers to this as the dictionary.
* **Mappings** - This is a list of all the mappings specified in a profile.
* **Table** – This is a simple table view of the resource.
* **XML & JSON** – Respective views of resources in either XML or JSON formatting.
* **Related** - The references to the profiles from which this profile was derived.
* **History** – On this tab you can view the difference between two versions of the same profile. This is a great feature for comparing and tracking changes. To compare two different files, see :ref:`compare-files`.
* **Issues** - On this tab users with a paid account can track issues. New issues can be created by clicking the ``New issue`` button. The issue list can be filtered on open, closed or your own issues. By clicking on an issue you can read the entire conversation and add a new comment.
* **Documentation** - Here you can provide extra documentation on your resource.


Update Resources
""""""""""""""""
When you want to update your resource, there are several ways to do so. Choose one of the following options from the ``Update`` menu at the top of the Resource page:

* **Upload**: Update by uploading a file (either XML or JSON)
* **Fetch**: Update by fetching from a different FHIR server (provide a GET request to the server where your resource is located)
* **Edit**: Update by editing the last version (opens a XML-editor in a small window where you can directly edit the XML code of your resource)
* **Editor**: Update by editing the last version (opens a stand-alone full screen XML-editor in a different tab where you can directly edit the XML code of your resource)


Download Resources
""""""""""""""""""
You may also choose to download the resource and save a local copy on your computer. You can either choose to download the resource as a XML or JSON file or directly copy the XML or JSON code of the resource to your clipboard, so you can easily copy-paste it to another location.


Add Resources
"""""""""""""
Go to your Project page to `add new resources <../adding_content/upload-resources.html>`_ to your project.


.. _compare-files:

Comparing two files
"""""""""""""""""""
The ``History`` tab compares two versions of the same file. To compare two *different* files, use the ``Compare`` menu at the top of any resource page or package file page.

The menu holds two slots, A and B:

#. Open the first file and choose ``Set as file A``.
#. Navigate to the second file and choose ``Set as file B``. The two files do not have to be in the same project: you can compare across projects, across packages, and across package versions.
#. Click ``Compare A <-> B`` to open a side-by-side diff. This option stays disabled until both slots are filled.

The menu shows what is currently in each slot, as clickable links to the project or package and to the file itself. Use ``Clear selection`` to empty both slots.

.. image:: ../images/CompareFileMenu.png
   :scale: 75%

The diff shows file A on the left and file B on the right, with the same links above each side.

.. image:: ../images/CompareFilesDiff.png
   :scale: 75%

.. note::

   Your selection is stored in a browser cookie that expires after one day, which is what lets you pick the two files in separate visits. It is not shared between browsers or devices.

