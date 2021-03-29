========================
RESTful API for CRAMS
========================

The data stored in CRAMS instances is made accessible through
a RESTful API.

The API version ``v1`` is built on the Tastypie framework ??

The RESTful API can also be explored via the automatically generated Swagger
documentation at  < location>

See `swagger.io`_ for details on the Swagger standard.

.. _`swagger.io`: http://swagger.io


Below CRAMS Services detailed in the CRAMS Architecture section are implemented as a collection of rest API services. 
The APIs are described next.

Allocation Request
Authentication
Authorisation
Request Approval
Resource Provision
Provisioner
Data Administration
Data Ingest
Reporting
Usage Ingester


Lookup API
Lookup APIs return data related to system level constants. They are used to populate drop down boxes, identify client systems, list products available for provisioning etc. The current set of lookup APIs include
List of Crams Clients serviced by current system. The clients are identified as EResearchBody and subsystems within them identified as EResearchBodySystem.
For example: 
EResearchBody:  HPC
EResearchBodySystem:  M3, CVL, Monarch
List of Storage Products available per eResearchBodySystem
List of Compute Products available per eResearchBodySystem

api/v1/exists
api/v1/e_research_body
api/v1/contact_role
api/v1/alloc_home
api/v1/durations
api/v1/grant_types
api/v1/for_code
api/v1/seo_code
api/v1/<erb>_sps
api/v1/<erb>_cps
api/v1/funding_scheme

Contact API
  Contacts are the primary users of the Crams system. Crams contacts are different from users defined in Django User model. Contact APIs assist in management 
  of  contact information including creating and updating of contact information, search by email, name etc. 
  The APIs under this category are 
  Search contact by email, name
  Create new Contact
  Update existing contact
  add/update client subsystem specific Identifier for a contact
  For example: set HPC posix user id for a given contact
  For information on metadata available for a given contact, please refer to the Data Model described elsewhere in this document.

Membership API
  Manages project membership roles and assignments. With membership APIs:
  Users can request to join or leave a project
  Project leaders can invite, approve or remove team members
  Admin users can act on behalf of the project leaders to invite, add or remove user's association with a project
  Both Admin and Project leaders can change project roles associated with a particular user of the project

  api/v1/member/project_leader_members
  Project leader view of members in their project. Returns a list that includes all current members in the project, users who have requested to join, users who have been invited join and users who were former members of the project.

  api/v1/member/project_member
  User view of all projects user is a member of. Returns a list that includes all projects user is a member of, projects user have been invited to join, projects user have requested to join and former projects user was a member of.

  api/v1/member/project_leader_invite
  Project leader invite to a user to join their project.

  api/v1/member/project_leader_request
  Project leader actions to accept, decline, reject and revoke a users member project request.

  api/v1/member/project_member_request
  User actions to accept, reject their invitation or request to join a project.

  api/v1/member/project_member_join
  User action to request to join a project.

  api/v1/member/project_join_search
  Public search of project using project title or project identifier returns a list of search result projects.

  api/v1/member/project_admin_add_user
  Admin action to add a user directly to a project. User added to project is instantly a project member bypassing request/invite acceptance step.

  api/v1/member/project_leader_set_role
  Project leader action to change a project team member existing role to a new role.
Software Licence API
  Manages software licences, user software licence requests and CRAMS user’s software licence agreements. Within the software licence API’s:
  A user can view all available software products in CRAMS.
  A user can view the software product’s licence information.
  A user can view all the software product licences they have applied for and view the current status of request. (e.g: status of request can be: Approved, Requested, Declined)
  A user can apply for a software product by agreeing to the licence.
  An admin can view all user requested software licences.
  An admin can approve a user requested software licence.
  An admin can decline a user requested software licence.

  api/v1/software/products
  Public list of all available software products.

  api/v1/software/products/current_user
  User list of all software products current user has applied for. 

  api/v1/software/products/<product_id>
  View a single software product detail information 
  <product_id> - SoftwareProduct primary key

  api/v1/software/license
  View all available software products and their associated licences.

  api/v1/software/license/current_user
  User list of all software product licences the current user has applied for.

  api/v1/software/license/<licence_id>
  View a single software product licence detail information
  <licence_id> - SoftwareLicence primary key

  api/v1/software/contact_license
  Lists all current CRAMS users who have requested software products.

  api/v1/software/contact_license/request




  api/v1/software/contact_license/<licence_id>
  View a single user contact object software product request.
  <licence_id> - ContactSoftwareLicense primary key

  api/v1/software/contact_license/<licence_id>/accept_request 
  Admin approves a software product licence request from user.
  <licence_id> - ContactSoftwareLicense primary key

  api/v1/software/contact_license/<licence_id>/decline_request 
  Admin declines a software product licence request from user.
  <licence_id> - ContactSoftwareLicense primary key

  api/v1/software/category
  Lists all the software categories. (E.g: Neuroimaging, Deep Learning, Chemistry…)

  api/v1/software/type
  Lists all the software licence types. (E.g: GPL, Apache, MIT….)

Project API 
  Projects are the primary entry point for requesting resource allocation. With project APIs:
  Users can create a new project and associate supporting metadata related to grants, domains, for codes, publications etc.
  Add other project metadata in the form of a predefined set of question/answer pair 
  add/update client subsystem specific Identifier for a project
  For example: set HPC posix group id for a given project
  To facilitate rapid development, current API also permits applicant and users with edit access to the project:
  the ability to add/remove users to project, including project leaders
  request new or update existing resource allocation by including request API json along with project API. A project can have more than one request, usually one
  per client subsystem. However, this restriction is not enforced in code.

Request API 
  Given a project, Request APIs can be used directly to request New allocations or amend existing Allocations. In addition to allocation information, request APIs provide additional information related to status, client subsystems. With request API users can:
  Query current status, allocation information and related metadata
  Request/Amend compute or storage allocations
  Associate additional metadata in the form predefined set of Question/Answer pairs for a given client subsystem

Provisioning API 
  Provisioning APIs can be used for querying Crams to list resources that require provisioning. Companion APIs to update Crams regarding the status of 
  provisioning process is also available.  

  api/v1/software/provision






API accessible models
=====================




Authentication
==============




  

Querying the database (GET)
===========================

All endpoints support querying lists and individual records via GET requests.
Some support more complex queries via GET parameters as well.


Creating objects, adding files (POST)
=====================================

The creation of Experiments, Datasets and Dataset_Files via POSTs with the
option to include metadata/parametersets has been implemented and tested.

The following examples demonstrate how to go about it.

In all except the file attachment case the POST data should be a JSON string,
the ``Content-Type`` header needs to be set to ``application/json`` and the
``Accept`` header as well. Other response formats may be made available in the
future.

In all cases the URI of the created object is returned in the ``Location``
header of the response.


Example JSON input


   

Example JSON input:




