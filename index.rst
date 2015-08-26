================================================
Welcome to the DCAT-AP Switzerland documentation
================================================

This page is a technical documentation of the DCAT-AP Switzerland metadata standard to help publishers get their data on the Swiss open data portal.

There are several possibilities to add metadata on the portal:

#. Use the provided form to enter all the data (*recommended for ~1-20 datasets*)
#. Upload data as RDF/XML conforming the DCAT-AP standard (*recommended for ~20-100 datasets*)
#. Provide a RDF/XML DCAT catalog endpoint for harvesting (*recommended for >=100 datasets*)


All of the above options make use of the :doc:`DCAT-AP format <dcat-ap-format>`.

:doc:`dcat-ap-format`
  Description of the fields that are used and how to create the RDF/XML file

:doc:`form`
  How to use the form provided by the Swiss open data portal

:doc:`upload`
  Import a RDF/XML by uploading a file to the portal

:doc:`harvester`
  How to build a source to be harvested

.. toctree::
  :maxdepth: 1
  :hidden:

  dcat-ap-format
  form
  upload
  harvester
