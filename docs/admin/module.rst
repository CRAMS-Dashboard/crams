============
Module
============

The sections below provide a Quick Start guide building and installing individual CRAMS modules. 

Module Build
------------

Setup python environment for CRAMS Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Each CRAMS module in the ``crams-app`` directory can be built and installed independently.

Some CRAMS modules are dependent on other CRAMS modules and require those modules to be installed first before the Module can be built.

Check the ``settings.py`` in the CRAMS Modules under ``INSTALLED_APPS`` to see what modules it requires. Take the ``crams_contact`` module for example::

    'merc_common',
    'crams',
    'crams_log',
    'crams_contact',
    'crams_manager',

The CRAMS Contact module requires the modules above to be installed first before you can build the module.

Starting with the ``merc_common`` module, it is the base module that all other CRAMS modules rely on. The following module setup example will be using ``merc_common`` module.

Before you can start building you need to setup your python environment, the easiest way is to use virtualenv with python 3.8 and pip see: https://docs.python-guide.org/dev/virtualenvs/ for more information on how to install and setup a virtual python environment.

Once you have your python virtual environment setup first install the python packages required using pip by running the command::

    pip install -r requirements.txt

This will install all the python packages required by the ``merc_common`` module into your python environment.

Building CRAMS Module
~~~~~~~~~~~~~~~~~~~~~

To build the CRAMS module simply run the following command::

    python setup.py sdist

This will build the CRAMS module to a Sourch Archive `tar.gz` file under the ``dist`` directory. Running the build command in the ``merc_common`` package should build the following file::

    merc_common/dist/merc_common-1.0.0.tar.gz

Module Installation
-------------------

Once the CRAMS module has been built to install the module into a python environment using pip::

    pip install merc-common/dist/merc_common-1.0.0.tar.gz

Module Configuration
--------------------

Most CRAMS module build configuration can be found in the module root directory. The ``MANIFEST.in`` file will define what files will be included in the module build and ``requirements.txt`` will define what python packages are required by the module to be installed.

The CRAMS module django app ``settings.py`` will have all the django related configuration.






