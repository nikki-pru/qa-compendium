=============================
Contributing to Documentation
=============================

This compendium runs on Sphinx There are three ways to contribute to this Compendium. 

.. note::
  This compendium will take docs in either the reStructuredText (`*.rst`) or Markdown (`*.md`) format.

Create the article on Github
------------------------------

#. On the `Compendium github repository`_, navigate to the folder where you'd like to add the article.
#. Click on **Add file** button > **Create new file**.
#. Name your file and create your doc.
#. Send in a pull request.

Upload the article on Github
-----------------------------

#. On the `Compendium github repository`_, navigate to the folder where you'd like to add the article.
#. Click on **Add file** button > **Upload files**.
#. Select your file and upload (``.md`` or ``.rst``).
#. Send in a pull request.

Build locally using Compendium source
-------------------------------------

It is recommended to use this format if you are doing the following:

* Creating a new folder or editing an existing folder.
* Adding images.
* Would like to view what the article/document will look like in the readthedocs site.

Using the ``*.rst`` format also allows adding tags using the following directive at the top of the file:
::
  .. meta::
    :keywords: list, of, tags

#. Fetch the `Compendium github repository`_. 
#. Assuming you have Python installed, install sphinx using ``pip install sphinx``.
#. On the ``/docs`` folder of the fetched repository, run ``make html``. This should create a ``_build`` folder where the *.html files will be created.
#. On the ``_build`` folder, view the ``index.html`` file to view the locally built Compendium.
#. Create your docs using your preferred editor.
#. Create your commits and send in a pull request.

.. note::
  * `Sphinx Quick Start guide`_
  * `reStructuredText Primer`_
  * `reStructuredText and Sphinx CheatSheet`_
  
  
.. _Compendium github repository: https://github.com/nikki-pru/qa-compendium
.. _Sphinx Quick Start guide: https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html#quick-start
.. _reStructuredText Primer: https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html
.. _reStructuredText and Sphinx CheatSheet: https://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html
