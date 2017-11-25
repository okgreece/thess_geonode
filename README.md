# Thess_Geonode

Current GeoNode customization takes place using a django template project that has been created for this purpose.

To install the thess_geonode theme to further customize and test it in a clean local virtual machine (Ubuntu 16.04 LTS) follow the next steps.

## Installation

First, install GeoNode to your system with:

```
$ sudo add-apt-repository ppa:geonode/stable
$ sudo apt-get update
$ sudo apt-get install geonode
```
Download the theme in your home directory and install it:

```
$ cd /home/{your_username}
$ git clone https://github.com/okgreece/thess_geonode
$ sudo pip install -e thess_geonode
```

Now if you go to your browser and open http://localhost/ you will see the default Geonode website.

## Usage

Rename the local_settings.py.sample to local_settings.py and edit it's content by setting the SITEURL and SITENAME.

Make sure to use the `SECRET_KEY` and `DATABASE_PASSWORD` from /etc/geonode/local_setting.py .

Edit the file /etc/apache2/sites-available/geonode and change the following directive from:

> WSGIScriptAlias / /var/www/geonode/wsgi/geonode.wsgi

to:

> WSGIScriptAlias / /home/{your_username}/thess_geonode/thess_geonode/wsgi.py

Add the "Directory" directive for your folder like the following example:

> <Directory /home/{your_username}/thess_geonode/thess_geonode/">
>
> > Order allow,deny
> >
> > Options Indexes FollowSymLinks
> >
> > Allow from all
> >
> > Require all granted
> >
> > IndexOptions FancyIndexing
>
> </Directory>

Install all the packages from requirments.txt that isn't already installed (used pycharm IDE) and migrate

```
$ python manage.py migrate
```

Restart apache:

```
$ sudo service apache2 restart
```

In the thess_geonode directory run:

```
$ python manage.py collectstatic
```

Click yes when prompted and then visit http://localhost/ . You'll see the theme is now installed.

Edit the templates in thess_geonode/templates, the css and images to match your needs and then run:

```
$ python manage.py collectstatic
```

## Github Considerations

While it is helpful to recommit your django project wrapper back to a distributed version control repository. * It is also important to remember that production instances will store security information in the local_settings.py * Admin/Devs should always remember to exclude this file in the .gitignore file in the same folder as the .git:

```
$ nano .gitignore
/{project}/local_settings.py
```

save, make sure the file is also removed from git cache:

```
$ git rm -f --cache //local_settings.py
$ git status
```

confirm the file is no longer staged for the next commit or that if it is as "removed"