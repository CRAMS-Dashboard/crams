============
Installation
============

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

