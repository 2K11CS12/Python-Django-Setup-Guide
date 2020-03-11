# Python Django Setup Guide

## ``` WINDOWS ``` - STEPS TO INSTALL PYHTON(``` 3.8.0 ```) & DJANGO(``` 2.2.* ```)
Application requires [Python](https://www.python.org/) ``` v3.8.0 ``` to run.
Steps to configure the application on local machine (Windows)

  - Install Python on Local Machine ``` v3.8.0 ```
  - Install pip package manager [PIP](https://pip.pypa.io/en/stable/installing/)
    ```python 
    python -m pip install -U pip 
    ```
  - Install virtualenv and virtualenvwrapper
    ```python
    pip install virtualenv
    pip install virtualenvwrapper-win
    ``` 
 - Create a virtual environment for your project 
    ```python 
    mkvirtualenv envname 
    ```
 - Activate/deactivate the environment
    ```python 
    workon envname 
    deactivate
    ```
 - requirements.txt
    A `requirements.txt` file is a file that lists all of the modules needed for the Django project to work. These are all the modules, such as Django, django-allauth, mysqlclient, numpy, etc. that the Django project needs to work.

    So how can we create a requirements.txt file?

    Well, before we do this, you may know that typing in, `pip freeze`, into your command terminal lists all of the modules that you have installed for your project.

    ```
    pip freeze
    ```
    we can list all of the modules with pip freeze and have a `requirements.txt` file created this listing copied to the text file.
    ```
    pip freeze > requirements.txt

    ## To install all listed modules/libraries, run following command
    pip install -r requirements.txt
    ```

## DJANGO APPLICATION SETUPS
#### Make sure that, you have created virtual environment & activated
- Install Django ``` v2.2.* ```
    - If you maintain ``` requirements.txt ``` file, `Django==2.2.*` is listed
        ```
        pip install -r requirements.txt
        ```
    - if not, run following commands
        ```python
        pip install Django==2.2.*
        ```
 - Create Project
     ```python
     django-admin startproject projectname
     cd projectname
     ```
 - Create Django App
    ```python
     django-admin startapp appname
     ```
 - Migrations Commands
    ```python
     python manage.py makemigrations
     python manage.py migrate
     python manage.py showmigrations
     ### OR ###
     django-admin makemigrations
     django-admin migrate
     django-admin showmigrations
     ```
 - Create Super USER
    ```
    python manage.py createsuperuser
    ```
 - Run Django Application
    ```
    python manage.py runserver
    ```
 - Open link on browser ``` http://127.0.0.1:8000/ ```

### Production & Deployment Instructions
Coming Soon!

### Setup Django with Apache/XAMMP
https://serverfault.com/questions/439070/apache-wont-restart-after-inserting-mod-wsgi
https://groups.google.com/forum/#!topic/modwsgi/dVCPbhiUw90
- Set `MOD_WSGI_APACHE_ROOTDIR` using following command`
    ```
    set MOD_WSGI_APACHE_ROOTDIR=D:/xampp72/apache/
    ```
- Install `mod_wsgi`
    ```
    pip install mod_wsgi
    ```
- if below does not work, download `.whl` file from here https://www.lfd.uci.edu/~gohlke/pythonlibs/#mod_wsgi and run following command
    ```
    pip install D:\path\to\Downloads\mod_wsgi-4.7.0+ap24vc15-cp38-cp38-win_amd64.whl
    ```
- To check Paths run this to command line `mod_wsgi-express module-config`, this will return following things
    ```
    LoadFile "c:/users/kalim.ullah/appdata/local/programs/python/python38/python38.dll"
    LoadModule wsgi_module "c:/users/kalim.ullah/appdata/local/programs/python/python38/lib/site-packages/mod_wsgi/server/mod_wsgi.cp38-win_amd64.pyd"
    WSGIPythonHome "c:/users/kalim.ullah/appdata/local/programs/python/python38"
    ```
- Open apache `httpd.conf` file and paste following line at the bottom of file
    ```
    LoadModule wsgi_module "c:/users/kalim.ullah/appdata/local/programs/python/python38/lib/site-packages/mod_wsgi/server/mod_wsgi.cp38-win_amd64.pyd"
    WSGIScriptAlias / "D:/projects/certdashboard/dashboard/wsgi.py"
    WSGIPythonHome "c:/users/kalim.ullah/appdata/local/programs/python/python38"
    WSGIPythonPath "D:/projects/certdashboard"

    Alias /media/ D:/projects/certdashboard/media/
    Alias /static/ D:/projects/certdashboard/static/

    <Directory D:/projects/certdashboard/static>
    	Require all granted
    </Directory>
    
    <Directory D:/projects/certdashboard/media>
    	Require all granted
    </Directory>
    
    <Directory "D:/projects/certdashboard">
    	<Files wsgi.py>
    		Require all granted
    	</File>
    </Directory>
    ```

License
----
All rights reserved by ``` Me ```

   [nmap]: <https://pypi.org/project/python-nmap/>
   [msql]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
