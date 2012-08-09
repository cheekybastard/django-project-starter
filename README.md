django-project-starter
======================

Django 1.4 project quick start. 

Set up:

    $ virtualenv --no-site-packages env
    $ source env/bin/activate

    $ pip install django
    $ which django-admin.py (check django version, assumption is the mother of all fuck ups.)
    $ django-admin.py startproject myproject

Git that shit:

    $ git init
    $ git add *
    $ git commit -a -m 'Initial commit of myproject'
    $ git push origin master  [if 1st time: git remote add origin <server>]

South DB migrations:

    $ pip install south

    add 'south' to settings.py

    $ python manage.py syncdb
    $ git add .
    $ git commit -a -m 'Added South for database migrations'

    $ python manage.py startapp myapp

    $ python manage.py schemamigration myapp --initial
    $ python manage.py migrate myapp --fake 0001
    $ python manage.py migrate myapp
    $ python manage.py schemamigration myapp --auto
 
South - editing models:
   
    1.) save the model changes
    2.) run schemamigration --auto
    3.) run migrate to actually commit the changes to the database
    
South Options:

    $ --all: Used instead of an app name, allows you to migrate all applications to the same target. For example, ./manage.py migrate --all --fake 0001 if you are converting a lot of apps.
    $ --list: Shows what migrations are available, and puts a * next to ones which have been applied.
    $ --merge: Runs any missed (out-of-order) migrations without rolling back to them.
    $ --no-initial-data: Doesn’t load in any initial data fixtures after a full upwards migration, if there are any.
    $ --fake: Records the migration sequence as having been applied, but doesn’t actually run it. Useful for Converting An App.
    $ --db-dry-run: Loads and runs the migration, but doesn’t actually access the database (the SQL generated is thrown away at the last minute). The migration is also not recorded as being run; this is useful for sanity-testing migrations to check API calls are correct.


Git clone to dev folder:

    $ git clone /path/to/my/project/  (Git will create an exact copy of the entire repository. All changes, branches, and history will be available here. From here on out, you should be working from your development directory.)
    $ git checkout -b <branchname>  (will both create a new branch named and check it out. Almost all of your development should be done on a branch, so that master mimics the current production master and can be used for recovery at any time.)

Fabric for Deployment:
    
    $ pip install fabric
    
fabfile.py
from fabric.api import local

    def prepare_deployment(branch_name):
        local('python manage.py test myapp')
        local('git add -p && git commit')
        local('git checkout master && git merge ' + branchname)
    
