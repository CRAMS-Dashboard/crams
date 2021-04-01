========================
RESTful API for CRAMS
========================

The data stored in CRAMS is made accessible through a RESTful API.

Below CRAMS Services detailed in the CRAMS Architecture section are implemented as a collection of rest API services. 
The APIs are described next.

- Authentication
- Lookup
- Contact
- Membership
- Project Request
- Request Approval
- Resource Provision
- Reporting

Authentication
--------------

There are currently 2 methods of authentication, the default is using CRAMS user authentication and the other is using AAF rapid connect.

Rapid Connect Authentication
""""""""""""""""""""""""""""

Authenticate using rapid connect ::

  HTTP GET:
  /rapid_connect_token_auth

CRAMS Authentication
""""""""""""""""""""

Default basic CRAMS user authentication using username and password stored in CRAMS ::

  HTTP POST:
  /api_token_auth

Lookup
------

Lookup APIs return data related to system level constants. They are used to populate drop down boxes, identify client systems, list products available for provisioning etc. The current set of lookup APIs include
List of Crams Clients serviced by current system. The clients are identified as EResearchBody and subsystems within them identified as EResearchBodySystem. For example:

- EResearchBody: HPC
- EResearchBodySystem: M3, CVL, Monarch
- List of Storage Products available per eResearchBodySystem
- List of Compute Products available per eResearchBodySystem

Project Title Exist
"""""""""""""""""""
Check project title already exists in CRAMS ::
  
  HTTP GET:
  /exists/project

Get EResearch Body
""""""""""""""""""
Get a list of all available EResearch Body in CRAMS ::

  HTTP GET:
  /e_research_body/list

Get EResearch Body System
"""""""""""""""""""""""""
Get a list of all availble EResearch Body System for the EResearch Body ::

  HTTP GET:
  /e_research_body/e_research_system

Get Contact Roles
"""""""""""""""""
Get a list of all available user contact roles in CRAMS ::

  HTTP GET:
  /contact_role

Get Grant types
"""""""""""""""
Get a list of all available research grant types in CRAMS ::

  HTTP GET:
  /grant_types

Get FOR Codes
"""""""""""""
Get a list of all available FOR Codes in CRAMS ::

  HTTP GET:
  /for_code

Get SEO Codes
"""""""""""""
Get a list of all available SEO Codes in CRAMS ::

  HTTP GET:
  /seo_code

Get Funding Body
""""""""""""""""
Get a list of all available User funding body ::

  HTTP GET:
  /user_funding_body

Get Funding Schemes
"""""""""""""""""""
Get a list of all available funding schemes for a funding body ::

  HTTP GET:
  /funding_scheme

Get Storage Products
""""""""""""""""""""
Get a list of all available storage_products for a EResearch body ::

  HTTP GET:
  /storage_products

Contact
-------
Contacts are the primary users of the Crams system. Crams contacts are different from users defined in Django User model. Contact APIs assist in management 
of  contact information including creating and updating of contact information, search by email, name etc. 

Search contact
""""""""""""""
Search contacts in CRAMS by their email and name ::

  HTTP POST:
  /search_contact

Create new Contact
""""""""""""""""""
Creates a new contact into CRAMS ::
  
  HTTP POST:
  /contact

Update existing contact
"""""""""""""""""""""""
Update an existing contact ::
  
  HTTP PUT:
  /contact

Get Contact
"""""""""""
Get a users contact using their contact ID or email and returns a list of all projects they are a member of ::

  HTTP GET:
  /contact


Get Contacts
""""""""""""
Get all contacts in CRAMS ::

  HTTP GET:
  /admin/contact


Membership
----------
Manages project membership roles and assignments. With membership APIs:
Users can request to join or leave a project
Project leaders can invite, approve or remove team members
Admin users can act on behalf of the project leaders to invite, add or remove user's association with a project
Both Admin and Project leaders can change project roles associated with a particular user of the project

List all Project Members
""""""""""""""""""""""""
Project leader view of members in their project. Returns a list that includes all current members in the project, users who have requested to join, users who have been invited join and users who were former members of the project. ::

  HTTP GET:
  /member/project_leader_members

List all user Projects
""""""""""""""""""""""
User view of all projects user is a member of. Returns a list that includes all projects user is a member of, projects user have been invited to join, projects user have requested to join and former projects user was a member of. ::

  HTTP GET:
  /member/project_member

Send Invite to join Project
"""""""""""""""""""""""""""
Project leader invite to a user to join their project. ::
  
  HTTP POST:
  /member/project_leader_invite

Project Leader actions to accept/decline invite
"""""""""""""""""""""""""""""""""""""""""""""""
Project leader actions to accept, decline, reject and revoke a users member project request. ::

  HTTP POST:
  /member/project_leader_request

User actions to accept/decline invite
"""""""""""""""""""""""""""""""""""""
User actions to accept, reject their invitation or request to join a project. ::
  
  HTTP POST:
  /member/project_member_request


User request to join a project
""""""""""""""""""""""""""""""
User action to request to join a project. ::

  HTTP POST:
  /member/project_member_join

Search Projects to join
"""""""""""""""""""""""
Public search of project using project title or project identifier returns a list of search result projects. ::

  HTTP POST:
  /member/project_join_search

Admin add member to Project
"""""""""""""""""""""""""""
Admin action to add a user directly to a project. User added to project is instantly a project member bypassing request/invite acceptance step. ::

  HTTP POST:
  /member/project_admin_add_user

User project role change
""""""""""""""""""""""""
Project leader action to change a project team member existing role to a new role. ::

  HTTP POST:
  /member/project_leader_set_role

Project
-------

Projects are the primary entry point for requesting resource allocation. With project APIs:
Users can create a new project and associate supporting metadata related to grants, domains, for codes, publications etc.
Add other project metadata in the form of a predefined set of question/answer pair 
add/update client subsystem specific Identifier for a project
To facilitate rapid development, current API also permits applicant and users with edit access to the project:
the ability to add/remove users to project, including project leaders
request new or update existing resource allocation by including request API json along with project API. A project can have more than one request, usually one
per client subsystem. However, this restriction is not enforced in code.

Get a Project
"""""""""""""
Get a user Project using project/request id ::

  HTTP GET:
  /project_request  

Submit a Project Request
""""""""""""""""""""""""
User submit a new project request ::

  HTTP POST:
  /project_request


Update existing Project Request
"""""""""""""""""""""""""""""""
Update an existing project using the project/request id ::

  HTTP PUT:
  /project_request

Get all user Projects
"""""""""""""""""""""
Get all the projects user is a member, only returns minimal data set for each project::

  HTTP GET:
  /allocation_list


Admin get all Projects
""""""""""""""""""""""
Admin get all the projects in CRAMS, only returns minimal data set for each project::

  HTTP GET:
  /allocation_list/Admin


Request
-------

Given a project, Request APIs can be used directly to request New allocations or amend existing Allocations. In addition to allocation information, request APIs provide additional information related to status, client subsystems. With request API users can:
Query current status, allocation information and related metadata
Request/Amend compute or storage allocations
Associate additional metadata in the form predefined set of Question/Answer pairs for a given client subsystem

Get Request History
"""""""""""""""""""
Get all the request history to a project using project/request id ::

  HTTP GET:
  /request_history

Get all Submitted/Approved Projects
"""""""""""""""""""""""""""""""""""
Get all user submitted projects that are ready for reviewing to be approved/declined and can filter to requests that have been approved ::

  HTTP GET:
  /approve_list

Approve Request
"""""""""""""""
Approve a request that has been submitted or updated/extended ::

  HTTP POST:
  /approve_request

Decline Request
"""""""""""""""
Decline a request that has been submitted or updated/extended ::

  HTTP POST:
  /decline_request

Provisioning
------------

Provisioning APIs can be used for querying Crams to list resources that require provisioning. Companion APIs to update Crams regarding the status of 
provisioning process is also available.  

Get all Approved Requests
"""""""""""""""""""""""""
Get a list of all approved requests that are ready for provisioning ::

  HTTP GET:
  /provision_project/list

Get all Provisioned Projects
""""""""""""""""""""""""""""
Get a list of all provisioned projects ::

  HTTP GET:
  /approve_list/?req_status=active

Get an approved project that is ready to be provisioned
"""""""""""""""""""""""""""""""""""""""""""""""""""""""
Get project and request details of a project that is approved and ready to provisioned ::

  HTTP GET:
  /provision_project

Provision Project
"""""""""""""""""
Provision a project that has been approved ::

  HTTP POST:
  /provision_project

  




