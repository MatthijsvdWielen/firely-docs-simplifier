Create your first IG
====================

You can access the IG editor via the ``Guides`` tab in your project. Use the ``Create`` button to create a new Implementation Guide and provide a title for the IG. Simplifier will automatically generate a URL Key, but you can choose your own URL Key.

.. image:: ../images/ImplementationGuideCreate.png  

Click on ``Browse`` or the Implementation Guide itself for a preview of the guide. Click on the ``Edit`` button to open the Implementation Guide in the IG editor. In the left bottom a help section is available to get started with adding images and tree renderings etc.

IG Editor Settings
^^^^^^^^^^^^^^^^^^
The IG editor opens on the page of the root folder. Simplifier stores newly created IGs in a folder based structure allowing users to easily ``copy`` guides and maintain multiple versions of their guides. 

To adjust the settings of your IG click on the Settings icon (the middle icon representing a gear wheel). This brings you to a section that allows you to adjust the title and privacy on the Settings tab, or select an IG rendering format and Stylesheet file on the Style tab. In the settings you are also able to select a ``scope`` for your guide. The scope determines where the rendered resources in your guide come from. You can set the scope to released packages or you live development project. 

.. image:: ../images/IGEditorSettings.png   

The IG Editor consist of three sections. On the left is the IG's tree table which is used to define the outline of your IG and navigate between the pages of the IG. The middle section is the actual editor. The right section provides a preview of the actual IG page.   

By way of dragging the section bars you can adjust the size of each section to customize your view.

The IG folders work as follows:


- Home folder (1)
- Subsections folders (2)
- Subsection pages (3)
- Subsection page paragraphs (4)



In the IG Editor this looks like this: 


.. image:: ../images/IGeditorTreeHierarchy.png



In the IG rendering, when using a custom balottable IG design, it looks like this:


.. image:: ../images/IGPageHierarchy.png

The information on the ``index`` node is rendered on the Home, Subsections folder or Subsection pages. When more pages are added below the index file, these will be rendered as paragraphs for that page. If you want to use this, make sure the first page in a folder is named ``index``.

Markdown 
^^^^^^^^
In the middle section is a Markdown based editor used to compose your IG content. 
Markdown is a text-to-HTML conversion tool. 
It allows you to write using an easy-to-read, easy-to-write plain text format. 
The following link provides an overview of the Markdown features which can be used in this editor: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet.

A short summary of frequently used features are as follows:

- Header size edits using ``#Header size 1`` to ``######Header size 6``
- Adding Emphasis, also know as italics, with ``*asterisks*`` or ``_underscores_``
- Adding Strong emphasis, also known as bold, with ``**asterisks**`` or ``__underscores__``
- Adding Combined emphasis with ``**asterisks``` and ``_underscores_**``
- Strikethrough uses two tildes. ``~~Scratch this.~~``


The IG editor has features which allow you to include Simplifier content in your IG. 
These features work by using the statements written below in the editor. 
After adding these statements in the editor refresh the page, by pressing Crtl + Enter or clicking the Refresh button, to make them visible in the preview section. 

- ``{{tree:canonicalUrl}}``		                - renders a tree structure as seen in the resource overview tab
- ``{{table:canonicalUrl}}``		            - renders a table as seen in the resource table tab
- ``{{link:canonicalUrl}}``			            - provides a link to the specific resource page on Simplifier
- ``{{namingsystems:ProjectName}}``				- lists all namespaces of a project in a table


The location of the rendered resources is based on the scope of the IG as set in the settigns.  


The following statements add an index within the IG. 

- ``{{index:root}}``	- gives an index of the entire IG 
- ``{{index:current}}`` - gives an index of the current selected element


Formatting style
^^^^^^^^^^^^^^^^

An IG can be rendered in one of three formats: a Tree table, Two Level Menu or HL7 format(work in progress).

A Tree table rendering will display your IG with the elements in a format similar to the tree table with the elements and their hierarchy along the left side of the page.

.. image:: ../images/IGTreeNavigation.png

A Two Level Menu rendering will display your IG with the elements in tabs along the top of the page.

.. image:: ../images/IGHorizontalNavigation.png

A HL7 format rendering will display your IG with the elements in tabs along the top of the page similar to the Two Level Menu rendering, but in the style of a HL7 IG.

Every folder contains an index file which will be displayed as the folders homepage. Every folder can have child pages which can be added with the ``+`` icon. In the image below you can see the folder structure on the left and on the right de rendering of the Implementation Guide: 

.. image:: ../images/FolderStructure.png


FQL table generation
^^^^^^^^^^^^^^^^^^^^

With the introduction of FQL  it is now possible to create dynamic tables in your IG. FQL tables retrieve information from the resources in the select scope. Below is an example of the syntax. For more information and examples please look at our `documentation <https://simplifier.net/docs/fql>`_.

.. code-block:: SQL

    
    @```

    from <your recources>
    where <option>
    select <what you want in the table>
    
    ```

You can also save your FQL statements in order to re-use them on different pages and even in different projects. In the IG editor, the option for saving your custom snippets is available. This will save your statements in a .snippet.md file which is than usable within every IG page in that specific project. The .snippet.md file(s) can be downloaded and uploaded in different projects to use them across your organization. 

 .. image:: ../images/IGEditorSnippets.png

Pagelink using page topic
^^^^^^^^^^^^^^^^^^^^^^^^^

With the `pagelink` command you can create a link to a different page in your Implementation Guide: `{{pagelink:<url key for the markdown resource describing the page>} }` (without the space). You can find the url key for the markdown resource describing the page you want to link to with the help from the pagelink autocomplete, or by looking at the address bar when opening the resource describing the page from your project's Resources tab.

When a URLkey for a page that is referred to or one of the folders it is in changes, the pagelink might break. For that reason, we created a more robust way of linking to pages within a guide with the use of ``topic``. 

In an Implementation Guide page you can set the ``topic`` by starting the page with a topic header:


.. code-block:: yaml

    ---
    topic: yourpagename
    ---

Using the topic in you pagelink ``{{pagelink:yourpagename}}``, this will prevent the links from breaking even when creating copies of your guide. 


