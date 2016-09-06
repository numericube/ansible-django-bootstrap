# ansible-django-bootstrap

A skeleton of a Django+bootstrap+Vagrant+Ansible combo.

# Requirements

* Vagrant >= 1.7
* VirtualBox

# Overview

OS :
* Ubuntu 16.04 LTS (Xenial Xerus)

Languages :
* Python 2.7

Components :
* Nginx HTTP server
* Supervisord
* Gunicorn WSGI server
* Django
* SQLite
* Bootstrap 3

# Usage

Start the vagrant and let the provision setup everything.

	$ vagrant up

Then, you can access the Django website using <http://localhost:8080> or <https://localhost:8090> for the secure version.

# Running Django

By default, Django is already running trough Gunicorn as it would run in a production environment. (Note that the default settings aren't ready for production despite that)

If you wish to run Django in a developement mode using `runserver`, you must beforhand shutdown the Gunicorn and Nginx servers :

	$ sudo supervisorctl stop django
	$ sudo service nginx stop

Then you can go to your Django project directory and run it over the 8000 HTTP port.

	$ cd /vagrant/{ project name }/
	$ python manage.py runserver 0.0.0.0:8000

Your Django website will be available at the <http://localhost:8000> address.

# Building Bootstrap

The Grunt task runner bundled with Bootstrap can build the source files as soon as you edit them.

You just have to navigate to the Bootstrap directory and launch the watch :

	$ cd /vagrant/{ project name }/bootstrap-{ version }/
	$ grunt watch

You could also do a one-time compilation of the library as is :

	$ grunt dist

Note that the Django base template uses the non-minified version of Bootstrap by default because it's the one that's updated by `grunt watch`, so don't forget to do a `grunt dist` and use the minifed version of the Bootstrap files when you've done your work on them.

# Using HTTPS on Nginx

Nginx uses by default a self-signed SSL certificate to enable HTTPS and HTTP2.

You can replace them with your own certificates by putting them in the `/provision/ansible/roles/nginx/files` folder, and replacing the corresponding values in the `/provision/ansible/roles/setup/vars/main.yml` file.

# VM details

The main user is `www` and its home is under `/opt/www`.

The root repository is synced under `/vagrant`.

All the commands shown above assume that you're logged on as the `www` user. You can do it thanks to the `sudo` command :

	$ sudo su - www
