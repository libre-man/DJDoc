Installation
============

Requirements
------------

Running the sdaas server is CPU and memory intensive. To ensure that the server
runs properly make sure that your server meets the following requirements:

* 1 CPU core per channel you wish to create.
* At least 800 MB of RAM per channel, preferably 1GB of RAM.

The server needs to run linux. The sdaas server is tested with Ubuntu 16.04,
but probably works with other linux-based systems as well.

Setup
-----

To start deploying sdaas, the server will first need to be configured to run
sdaas.

Required packages to install:

* apache2
* libapache2-mod-wsgi-py3
* libmysqlclient-dev
* libmysqlclient20
* mysql-client
* mysql-server
* python3.5 (usually already installed)
* docker

Then clone the Server and Controller github repositories at:
https://github.com/libre-man/DJFeet and
https://github.com/libre-man/DJServer. Run *make setup* in both repositories.

Configuration
-------------

After the server setup the webserver needs to be configured and the Controller
docker instance needs to be build.

Database
~~~~~~~~~

Before sdaas can be deployed, a database needs to be configured. Use mysql to
create a new database and a user for the web application.

After this is done go to the deploy directory of the DJServer repository. Copy
the *example_db.cnf* file to *db.cnf* and edit it to reflect the database name,
user and password.

Apache
~~~~~~

Your server consists of a streaming server and a webserver. To run both servers
on one server, we use apache virtualhosts. Create two virtualhost files in
*/etc/apache2/sites-available/your_site.com.cnf*. One for the streaming server
and one for the webserver.

Then copy *example_deploy.cnf* in the deploy directory in *DJServer* to
*deploy.cnf*. Change the path in this file to the directory where you want the
web application to be deployed (this should be the same path as in your
virtualhost config).

Next edit the *sdaas/sdaas/settings/production.py* file in *DJServer* and
change all the directories to the desired directory. To the same thing for
the *sdaas/sdaas/wsgi.py* file.

Controller
~~~~~~~~~~

The channel controllers run in a docker instance. A docker image needs to be
built for this to work. To do this, go to the cloned DJFeet repository. The
docker instances need access to the github repository to pull the latest
version. This means that you first need to create a new ssh keypair and add it
to the github repository. Then move the public and private key to the DJFeet
directory and name them: *docker_ssh* and *docker_ssh.pub*. Then build the
docker image using: *sudo docker build . -t controller*.

Deploying
---------

After everything is configured we are finally ready to deploy sdaas. To do
this go to the DJServer directory and *cd* into the deploy directory. Then run
*sudo ./deploy.sh*. Now your webserver is live and ready to be used.

To login, we do need to create an initial super user. To do this, go to the
*sdaas* directory inside DJServer and run:
::
    sudo python3 manage.py createsuperuser --settings=sdaas.settings.production


