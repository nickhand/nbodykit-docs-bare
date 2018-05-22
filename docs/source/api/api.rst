API Reference
=============

The full list of nbodykit modules is available :doc:`here <modules>`. We
summarize the most important aspects of the API below.

.. contents::
   :depth: 2
   :local:
   :backlinks: none

.. _api-io:

The IO Library (:mod:`nbodykit.io`)
-----------------------------------

Base class:

.. autosummary::

  ~nbodykit.io.base.FileType

Subclasses available from the :mod:`nbodykit.io` module:


.. autosummary::

  ~nbodykit.io.bigfile.BigFile
  ~nbodykit.io.binary.BinaryFile
  ~nbodykit.io.csv.CSVFile
  ~nbodykit.io.fits.FITSFile
  ~nbodykit.io.hdf.HDFFile
  ~nbodykit.io.stack.FileStack
  ~nbodykit.io.tpm.TPMBinaryFile
  ~nbodykit.io.gadget.Gadget1File
