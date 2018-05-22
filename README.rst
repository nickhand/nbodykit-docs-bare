Setting up nbodykit documentation
=================================

The documentation is built using Sphinx -- general documentation can be
found at http://www.sphinx-doc.org. The documentation is located in the
``docs`` directory, and

- the documentation files are located in the `docs/source`_ directory and are restructured text files
- the configuration is controlled by `conf.py`_; this is generally the same template file with a few modifications for specific packages.
- the main page of the documentation is `docs/source/index.rst`_, which sets up the structure of the documentation by linking to the other files via table of contents commands
- the build process is controlled by `Makefile`_; this is also filled with template build commands, and we've added a few more for this package.


.. _conf.py: docs/source/conf.py
.. _Makefile: docs/Makefile
.. _docs/source: docs/source
.. _docs/source/index.rst: docs/source/index.rst

Build Instructions
------------------

To build a local copy of the nbodykit docs, install the programs in
environment.yml and run 'make html'. If you use the conda package manager
these commands suffice::

  git clone git@github.com:nickhand/nbodykit-docs-bare.git
  cd nbodykit/docs
  conda env create --name nbodykitdocs -f environment.yml
  source activate nbodykitdocs
  make html
  open build/html/index.html

The documenation can be cleaned using::

  make clean

This uses `environment.yml`_ to install the necessary dependencies of nbodykit
and the dependencies necessary to build the documentation. 

.. _environment.yml: docs/environment.yml 

Configuration
-------------

The configuration for the build process is handled by the `conf.py`_ file. This file 
is responsible for a few things: 

- loading the listed extensions
- setting various parameter that control how the documentation
- defining the html theme
- automatically generating a restructured text file containing a list of modules and telling Sphinx to autogenerate the docs for each module

We'll expand on the last two points in the sections below. 

Setting the Theme
^^^^^^^^^^^^^^^^^

There are various theme choices for the documentation. A common one is the 
Read the Docs (RTD) theme, which generates documentation that looks like https://sphinx-rtd-theme.readthedocs.io/.
For the nbodykit documentation, we used the `Sphinx Bootstrap theme`_, which lets you 
set any of the version 3 Bootstrap themes. We chose the `Readable`_ theme for its clarity.
This theme is chosen and configured near the bottom of the `conf.py`_ file, 
and the various options can be found in the documentation for the theme.

.. _Sphinx Bootstrap theme: https://ryan-roemer.github.io/sphinx-bootstrap-theme/
.. _Readable: https://bootswatch.com/3/readable/

Auto-generating the Docs
^^^^^^^^^^^^^^^^^^^^^^^^

In `conf.py`_, we use the function `autogen_modules()` to automatically generate 
the file `docs/source/api/modules.rst`. This file lists all of the modules in the package
under an `autosummary::` command. This command is described in the documentation here: 
http://www.sphinx-doc.org/en/master/ext/autosummary.html. By setting the ``toctree`` option
of this command to ``_autosummary``, Sphinx will automatically generate stub .rst files for 
each module in the ``docs/source/api/_autosummary``. After running ``make html``, you should
see both the ``docs/source/api/modules.rst`` files and all of the corresponding .rst files
in ``docs/source/api/_autosummary``.

This process allows us to dynamically generate the docs on the fly. With the documentation 
generated, I like to add explicit links to the relevant documentation from a single page
within the documentation. In this case, it is `api.rst`_. For the single module `nbodykit.io`, 
this page in the documentation will list out the name and a brief description of the 
specific classes/functions
that we list, and it will be linked to the full documentation for that object.

.. _api.rst: docs/source/api/api.rst

Using Jupyter Notebooks
-----------------------

The documentation for any GitHub repo can be easily hosted for free on Read the Docs, but
unfortunately, there is a rather short time limit for the documenation building process.
There are extensions that will show execute and show code snippets and output on the fly
at build time, but generally this will make you run over the time limit on Read the Docs. 
To get around this issue with nbodykit, we use the ``nbsphinx`` extension 
which lets you include executed Jupyter notebooks
in your documentation. So to avoid the time limit, we execute and commit notebooks to the 
repo, which are then displayed in the documentation without the code cells 
being executed again.

There is an example notebook at `docs/source/catalogs/reading.ipynb`_. This file 
is linked to from the main ``index.rst`` file. The documenation 
for the extension is very handy and can be found at https://nbsphinx.readthedocs.io.

.. _docs/source/catalogs/reading.ipynb: docs/source/catalogs/reading.ipynb

Workflow for editing notebooks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We use the ``nbsphinx`` extension to include ``.ipynb`` files in the docs. A few useful things to know:

1. **Hidden Cells**: You can include hidden cells in the notebook, which will not show up in the HTML output, by editing the cell metadata. Use View -> Cell Toolbar -> Edit Metadata, and then go to the cell you want, click edit metadata, and insert into the metadata dictionary the key/value pair: ``"nbsphinx" : "hidden"``.
2. **ReST Cells**: You can include raw restructured text cells in the notebook, which will be converted properly. You must set the cell type to raw ReST. This can be done using:  View -> Cell Toolbar -> Raw Cell Format, and then going to the cell you want, and setting the type to ReST. 
3. **Linking to notebook files**: From other RST files, you can link to the notebooks via the ``ref`` directive. The important thing to remember is that you must use the full notebook file path, as if the top level directory is ``source``. So you can link to a notebook in the cookbook directory, using the path "cookbook/lognormal-mocks.ipynb".

Executing notebooks
^^^^^^^^^^^^^^^^^^^

To execute all notebooks in the documentation before committing them or re-building 
the docs, use::

    python helper_scripts/run_notebooks.py

or equivalently, you can use ``make ipynb``.