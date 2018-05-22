|
|

.. image:: _static/nbodykit-logo.gif
   :width: 425 px
   :align: center

|
|

.. title:: nbodykit documentation

a massively parallel, large-scale structure toolkit
===================================================

**nbodykit** is an open source project written in Python
that provides a set of state-of-the-art, large-scale structure algorithms
useful in the analysis of cosmological datasets from N-body simulations and
observational surveys. All algorithms are massively parallel and run using the
Message Passing Interface (MPI).

Driven by the optimism regarding the abundance and availability of
large-scale computing resources in the future, the development of nbodykit
distinguishes itself from other similar software packages
(i.e., `nbodyshop`_, `pynbody`_, `yt`_, `xi`_) by focusing on:

- a **unified** treatment of simulation and observational datasets by
  insulating algorithms from data containers

- support for a wide **variety of data** formats, as well as **large volumes of data**

- the ability to reduce wall-clock time by **scaling** to thousands of cores

- **deployment** and availability on large, supercomputing facilities

- an **interactive** user interface that performs as well in a `Jupyter
  notebook`_ as on a supercomputing machine

.. _nbodyshop: http://www-hpcc.astro.washington.edu/tools/tools.html
.. _pynbody: https://github.com/pynbody/pynbody
.. _yt: http://yt-project.org/
.. _xi: http://github.com/bareid/xi
.. _Jupyter notebook: http://jupyter-notebook.rtfd.io

----

Getting nbodykit
----------------

To get up and running with your own copy of nbodykit, please follow the
:doc:`installation instructions <getting-started/install>`.
nbodykit is currently supported on macOS and Linux architectures. The
recommended installation method uses the
`Anaconda <https://www.continuum.io/downloads>`_ Python distribution.

nbodykit is compatible with **Python versions 2.7, 3.5, and 3.6**, and the
source code is publicly available at https://github.com/bccp/nbodykit.

.. _help:

----

Getting Help
------------

* :doc:`api/api`
* :doc:`help/support`

.. --------------------------------------------
.. include hidden toc tree for site navigation
.. -------------------------------------------

.. toctree::
  :maxdepth: 1
  :caption: Getting Started
  :hidden:

  getting-started/install
  catalogs/reading

.. toctree::
  :maxdepth: 1
  :caption: Help and Reference
  :hidden:
  :includehidden:

  api/api
  help/support
