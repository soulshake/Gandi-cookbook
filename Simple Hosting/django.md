# enter python virtual environment

```
$ virtualenv env
$ source env/bin/activate
```

# create project directory and install djangocms-installer module

```
$ mkdir tutorial-project && cd tutorial-project
$ pip install djangocms-installer
```

# create a new django project called 'mysite'

```
$ sudo djangocms -p . mysite
Database configuration (in URL format) [default sqlite://localhost/project.db]: 
django CMS version (choices: 2.4, 3.0, stable, develop) [default stable]: stable
Django version (choices: 1.4, 1.5, 1.6, 1.7, stable) [default stable]: 1.6
Activate Django I18N / L10N setting (choices: yes, no) [default yes]: yes
Install and configure reversion support (choices: yes, no) [default yes]: yes
Languages to enable. Option can be provided multiple times, or as a comma separated list. Only language codes supported by Django can be used here: en,de
Optional default time zone [default America/Chicago]: 
Activate Django timezone support (choices: yes, no) [default yes]: yes
Activate CMS permission management (choices: yes, no) [default yes]: yes
Use Twitter Bootstrap Theme (choices: yes, no) [default no]: yes
Use custom template set [default no]: no
Load a starting page with examples after installation. Choose "no" if you use a custom template set. (choices: yes, no) [default no]: yes
Creating the project
```

# create wsgi.py

```
$ nano wsgi.py
```

Add the following contents:

    import sys
    import os
    import os.path
 
    sys.path.insert(0, os.path.abspath(os.path.join(os.path.dirname(__file__),'mysite')))
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
    from django.core.wsgi import get_wsgi_application
    application = get_wsgi_application()

# create requirements.txt

```
$ pip freeze > requirements.txt
```

# create git repository, push, and deploy

```
$ git init
$ git remote add origin ssh+git://146585@git.dc1.gpaas.net/default.git
$ git add .
$ git commit -m "testing django"
$ git push origin master
$ ssh 146585@git.dc1.gpaas.net 'deploy default.git'
```

References:

1. http://docs.django-cms.org/en/support-3.0.x/introduction/install_from_scratch.html
2. http://wiki.gandi.net/en/simple/instance/python



