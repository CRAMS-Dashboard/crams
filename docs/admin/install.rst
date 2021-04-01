
CRAMS Frontend Installation
===========================

Prerequisites
-------------
- Node.js
- NPM

Install Node.js® and NPM on Windows
==================================

Step 1: Download Node.js Installer
----------------------------------

In a web browser, navigate to https://nodejs.org/en/download/. Click the Windows Installer button to download the latest default version. 
The Node.js installer includes the NPM package manager.

Step 2: Install Node.js and NPM from Browser
----------------------------------------------
1. Once the installer finishes downloading, launch it. Open the downloads link in your browser and click the file. Or, browse to the location where you have saved the file and double-click it to launch.

2. The system will ask if you want to run the software – click Run.

3. You will be welcomed to the Node.js Setup Wizard – click Next.

4. On the next screen, review the license agreement. Click Next if you agree to the terms and install the software.

5. The installer will prompt you for the installation location. Leave the default location, unless you have a specific need to install it somewhere else – then click Next.

6. The wizard will let you select components to include or remove from the installation. Again, unless you have a specific need, accept the defaults by clicking Next.

7. Finally, click the Install button to run the installer. When it finishes, click Finish.

Step 3: Verify Installation
----------------------------
Open a command prompt (or PowerShell), and enter the following::

~] node –v

The system should display the Node.js version installed on your system. You can do the same for NPM::

~] npm –v

Install Node.js® and NPM on Ubuntu
=================================

To install Node.js and npm, open a terminal and type the following command::

~] sudo apt-get install nodejs npm


* Note: some nodejs packages expect the `node` command to be available. Some deb packages of nodejs include this symlink, some do not if not:
On Ubuntu you can install the nodejs-legacy package to fix this::

~] sudo apt-get install nodejs-legacy

Now we should have both the node and npm commands working
::

~] node -v
~] npm -v


install grunt-cli globally
--------------------------
::

~] npm install -g grunt-cli 


Installing Node.js® and NPM on Mac
==================================

Installing Node.js and NPM is pretty straightforward using Homebrew. Homebrew handles downloading, unpacking and installing Node and NPM on your system. 
The whole process (after you have Homebrew installed) should only take you a few minutes.

Installation Steps
-------------------

Open the Terminal app and type brew update. This updates Homebrew with a list of the latest version of Node
::

~] brew install node.


Sit back and wait. Homebrew has to download some files and install them. But that’s it.

Verify Node.js and NPM
-----------------------
::

~] node -v
~] npm -v

Setup CRAMS Frontend
=====================

Install the required node modules. Under the project root directory
--------------------------------------------------------------------
::

~] npm install


There are 'local', 'dev', 'demo', 'staging', 'qat', 'prod' settings in the Gruntfile.js. Modify the 'apiEndpoint' to fit the right crams api backend uri.

To run the project locally
-------------------------
::

~] grunt runlocal

To run the project in dev
--------------------------
::
 
~] grunt rundev

To run the project in demo
--------------------------
::
 
~] grunt rundemo

To run the project in staging
--------------------------
::
 
~] grunt runstaging

To run the project in qat
-------------------------- 
::
 
~] grunt runqat 

To run the project in prod
--------------------------
::
 
~] grunt runprod

To run test
-------------------------
::
 
~] grunt utest
 



CRAMS API Backend Installation
======================

The sections below provide a Quick Start guide for getting a basic CRAMS installation up and running. 

Deploying CRAMS via Docker
--------------------------

Prerequisites
~~~~~~~~~~~~~
- Python 3.8
- Docker 20+
- MySQL 5.7 or SQLite3

Setup CRAMS using Docker
~~~~~~~~~~~~~~~~~~~~~~~~
The quickest way to setup a working CRAMS backend API is to use the docker deployment that will automatically build and install all the packages, setup the python environment and setup nginx to run the service.

You will need to install docker and build/run 2 docker containers, the first one is to setup the mysql database container and the second one is the nginx container that will run CRAMS.

Setup MySQL docker 
~~~~~~~~~~~~~~~~~~
1. Go to ``deployment/database/dev/config`` folder, copy the ``my.cnf.sample`` file and save it as ``my.cnf``

2. Go to ``deployment/database/dev/init`` folder, copy the ``init.sql.sample`` file and save it as ``init.sql``, replace the root user password, replace the db_user name and password, replace the db_name with what you want.

3. Copy the ``.env.sample`` file, and save it as ``.env`` file, and replace the root password with the same as in ``init.sql`` file

4. To start the MySQL database, run the following docker-compose command::
   
      docker-compose -f docker-compose-dev.yml up -d
5. To stop the MYSQL database, run the following docker-compose command::

      docker-compose -f docker-compose-dev.yml down

Setup CRAMS NGINX docker
~~~~~~~~~~~~~~~~~~~~~~~~
1. Under deployment folder, copy the ``.env.sample`` file and save it as ``.env`` file, replace the network name is define in ``deployment/databases/docker-compose-dev.yml``::

      NETWORK_NAME=crams-apps-network

2. Make sure you have updated the ``local_settings.py`` under ``crams-apps/crams_api/local`` folder

3. Make sure the Django db config settings are right in ``crams-apps/crams_api/local/local_settings.py``. Make sure the db host is the same network as in ``deployment/database/docker-compose-dev.yml`` (network section)

4. Run docker compose commands::

      # bring the docker container down
      > docker-compose -f docker-compose-dev.yml down

      # build the docker container
      > docker-compose -f docker-compose-dev.yml build

      # start the crams api without deamon:
      > docker-compose -f docker-compose-dev.yml up

      # start the crams api with deamon:
      > docker-compose -f docker-compose-dev.yml up -d

      # stop the crams api:
      > docker-compose -f docker-compose-dev.yml down

Check CRAMS API is running
~~~~~~~~~~~~~~~~~~~~~~~~~~
Once you have the CRAMS docker container running you check by launching your web browser to::

   http://127.0.0.1:8080/

Setup a user account
~~~~~~~~~~~~~~~~~~~~
The last step before you can start using the API is to create a user account. To do this you will need to access the CRAMS API container and create a user using a django command.

1. To access your CRAMS API container you will need to ssh into using docker::

      docker exec -it crams-web bash

   NB: ``crams-web`` is the default name of the container, if you have modified the container change it here accordingly.

2. Once connected to your container you can run the django command directly to create a new user using::

      python manage.py createsuperuser 

   Follow the prompts to create username, email and password for a user.

3. The user created will not have admin privilieges (won't be able to access the django admin), to set the user to have admin access we can use django shell to modify the user::

      # run django command to access the django shell
      > python manage.py shell_plus

      # fetch the user we just created
      > user = User.objects.get(username='username')

      # set the user to a superuser
      > user.is_superuser = True

      # set the user to a staff
      > user.is_staff = True

      # save user
      > user.save()

      # exit django shell
      > exit()

Access Django Admin site
~~~~~~~~~~~~~~~~~~~~~~~~
To access the Django admin site using the created user account, go to the following::

   http://127.0.0.1:8080/admin/

Log in with the user credentials of your created user.

