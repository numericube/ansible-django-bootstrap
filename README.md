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
* Ruby

Components :
* Nginx HTTP server
* Supervisord
* Gunicorn WSGI server
* Django
* SQLite

# Usage

Start the vagrant and let the provision setup everything.

	$ vagrant up

Then, you can access the Django website using http://localhost:8080 or https://localhost:8090 for the secure version.

# VM details

The main user is `www` and its home is under `/opt/www`.

The root repository is synced under `/vagrant`.
