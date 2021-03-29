============
Installation
============

The sections below provide a Quick Start guide for getting a basic CRAMS installation up and running. 


Prerequisites
-------------




Download
--------

To get the most recent stable release::



Quick configuration
-------------------



  
  

Initialisation
--------------



Running in a Docker Container
-----------------------------






Essential Production Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Database
~~~~~~~~






Access Rights & Licensing
~~~~~~~~~~~~~~~~~~~~~~~~~

Licences
^^^^^^^^

By default, the Creative Commons Attribution 4.0 International licences are loaded.

You can use the admin interface to add other licences. Please ensure
``allows_distribution`` is set to the correct value to ensure the licence
appears in conjunction with suitable public access types.


Legal Notice
^^^^^^^^^^^^

When changing the public access rights or licence for an experiment, a
legal notice is displayed. You can override it by
specifying following settings in *settings.py*:

.. code-block:: python

   LEGAL_TEXT = "A sample legal Text"




Deployment
----------
