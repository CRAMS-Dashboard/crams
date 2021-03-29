CRAMS
======

Overview
---------
The Monash University developed Cloud Resource Allocation Management System (CRAMS) is for resource allocation, instantiation and to report resource utilisation across Research Data Storage,  High Performance Computing Platform (HPC) and Research Computing Cloud.   CRAMS not only enables researchers to request access to resources across  research storage, cloud and  HPC allocations, it also collects project details across all allocations over time to form a rich metadata registry. CRAMS is a production system that is meeting key milestones of its transformation-driven road map. 

Key Features for Users
----------------------
CRAMS will provide an effective self service mechanism for researchers and research facilities  to request cloud resources, monitor usage and manage own allocations.  CRAMS will further enable faster processing of resource allocation requests and provisioning of resources to end users. CRAMS reporting will enable effective strategic decisions on resource planning across Monash Research Data Storage, High Performance Computing Platform and Research Computing Cloud to address research needs better. 

CRAMS Developments
-----------------------
CRAMS is mostly written in the `Python programming language <https://www.python.org/>`_ and is built on top of the `Django web framework <https://www.djangoproject.com/>`_.


Find out more
-------------

The source code is hosted at https://github.com/CRAMS-Dashboard/CRAMS

Documentation at https://crams.readthedocs.org/ includes

- User documentation
- Administrator documentation
- Developer documentation



Known deployments
-----------------
- **Data-Dashboardn**: https://datadashboard.erc.monash.edu/


Releases
--------

The default branch on GitHub is ``develop``. This is the cutting edge
development version. Please DO NOT use this in production, as it may have bugs
that eat your data.

The ``master`` branch is the current stable release with all the latest bug fixes
included. It will move to newer versions automatically. Follow this branch
if you want to stay up to date in a production environment.

Each version has its own branch named by version number. At the time of
writing, the latest release is ``x.x.x``, tagged from the ``series-x.x``
branch. Follow this branch for your production installation and
perform version upgrades manually.

Each bug fix or set of fixes bumps the minor version and each new release is
tagged, eg. ``x.x.x``. Use tagged releases if you are paranoid about changes to
the code you have not tested yourself.

To follow development, please see the contributing section below.


Reporting Bugs
--------------

Bug reports and feature requests can be made via our `public issue tracker`_.

.. _`public issue tracker`: https://github.com/CRAMS-Dashboard/CRAMS/issues


Contributing
------------

New contributors are always welcome, however all developers should review the
`pull-request checklist`_ before making pull requests.

For any wishes, comments, praise etc. either open a GitHub issue or contact us.

Contact details can be found on https://www.monash.edu/researchinfrastructure/eresearch/contact-us

.. _`pull-request checklist`: https://github.com/crams-test/crams-test/blob/main/Contributing.rst

