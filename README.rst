Thess\_Geonode
==============

Current GeoNode customization takes place using a django template
project that has been created for this purpose.

To install the thess\_geonode theme to further customize and test it in
a clean local virtual machine (Ubuntu 16.04 LTS) follow the next steps.

Installation
------------

First, install GeoNode to your system with:

.. code:: 

    $ sudo add-apt-repository ppa:geonode/stable
    $ sudo apt-get update
    $ sudo apt-get install geonode

Download the theme in your home directory and install it:

.. code:: 

    $ cd /home/{your_username}
    $ git clone https://github.com/okgreece/thess_geonode
    $ sudo pip install -e thess_geonode

Now if you go to your browser and open http://localhost/ you will see
the default Geonode website.

Usage
-----

Rename the local\_settings.py.sample to local\_settings.py and edit it's
content by setting the SITEURL and SITENAME.

Make sure to use the ``SECRET_KEY`` and ``DATABASE_PASSWORD`` from
/etc/geonode/local\_setting.py .

Edit the file /etc/apache2/sites-available/geonode and change the
following directive from:

    WSGIScriptAlias / /var/www/geonode/wsgi/geonode.wsgi

to:

    WSGIScriptAlias /
    /home/{your\_username}/thess\_geonode/thess\_geonode/wsgi.py

Add the "Directory" directive for your folder like the following
example:

.. code:: 

    <Directory /home/{your_username}/thess_geonode/thess_geonode/">
       Order allow,deny
       Options Indexes FollowSymLinks
       Allow from all
       Require all granted
       IndexOptions FancyIndexing
    </Directory>

Install all the packages from requirments.txt that isn't already
installed (used pycharm IDE) and migrate

.. code:: 

    $ python manage.py migrate

Restart apache:

.. code:: 

    $ sudo service apache2 restart

In the thess\_geonode directory run:

.. code:: 

    $ python manage.py collectstatic

Click yes when prompted and then visit http://localhost/ . You'll see
the theme is now installed.

Edit the templates in thess\_geonode/templates, the css and images to
match your needs and then run:

.. code:: 

    $ python manage.py collectstatic

Github Considerations
---------------------

While it is helpful to recommit your django project wrapper back to a
distributed version control repository. \* It is also important to
remember that production instances will store security information in
the local\_settings.py \* Admin/Devs should always remember to exclude
this file in the .gitignore file in the same folder as the .git:

.. code:: 

    $ nano .gitignore
    /{project}/local_settings.py

save, make sure the file is also removed from git cache:

.. code:: 

    $ git rm -f --cache //local_settings.py
    $ git status

confirm the file is no longer staged for the next commit or that if it
is as "removed"

GPL License
===========

Thess_Geonode is Copyright 2017 Open Source Geospatial Foundation (OSGeo), Open Knowledge Greece, EOfarm P.C.

Thess_Geonode is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

Thess_Geonode is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with GeoNode.  If not, see <http://www.gnu.org/licenses/>.
