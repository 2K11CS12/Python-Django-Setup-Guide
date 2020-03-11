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
 - Install Django ``` v2.2.* ```
    - If found ``` requirements.txt ``` file on root
        ```
        pip install -r requirements.txt
        ```
    - if not, run following commands
        ```python
        pip install Django==2.2.*
        pip install mysqlclient==1.4.*
        pip install django[argon2]==19.2.*
        pip install django[bcrypt]==3.1.*
        pip install python-nmap==0.6.*
        pip install factory-boy==2.12.0
        pip install django-smart-selects==1.5.4
        ```

## DJANGO FIRST APPLICATION SETUPS
 - Create Project
     ```python
     django-admin makeproject projectname
     cd projectname
     django-admin makeapp appname
     ```
 - Create Django App
    ```python
     django-admin makeapp appname
     ```
 - Migrations Commands
    ```python
     python manage.py showmigrations
     python manage.py migrate
     python manage.py makemigrations
     ### OR ###
     django-admin showmigrations
     django-admin migrate
     django-admin makemigrations
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
### Plugins

Currently extended with the following plugins. Instructions on how to use them in your own application are linked below.

| Plugin | Link |
| ------ | ------ |
| Python N-MAP | [https://pypi.org/project/python-nmap/][nmap] |
| mysqlclient | [https://pypi.org/project/mysqlclient/][msql] |


### Data Seeding and Fixtures Instructions
I we are using fixture then we need the following two commands.

# Data exporting through fixtures by using following commmands
# by using model name
python manage.py dumpdata <appname>.<modelname> > fixtures/appname/file.json 

# by using table name
python manage.py dumpdata <appname>.<tablename> > fixtures/appname/file.json 

# Data importing through fixtures by using this command
python manage.py loaddata fixtures/appname/file.json


### Production & Deployment Instructions
Coming Soon!

### Misc
 - Get list of all installed packages and their versions
    ```
    pip freeze
    pip freeze > requirements.txt # Save all the packages in the file with
    python manage.py dumpdata auth.user --indent 4 > user.json # dumpdata to create fixtures
    python manage.py loaddata user.json # To fill your models with Fixtures
    ```

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
All rights reserved by ``` Certstation ```

   [nmap]: <https://pypi.org/project/python-nmap/>
   [msql]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
