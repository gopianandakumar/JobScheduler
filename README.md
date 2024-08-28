# JobScheduler
Project For Job Scheduling
first of all create vitual env

#virtualenv myenv

activate it by 
#myenv/Scripts/activate

then create django project in your local directory 

#django-admin startproject job_scheduler
#cd job_scheduler
#django-admin startapp jobs

Install required packages
#pip install django djangorestframework celery redis
 Update settings.py:
Add rest_framework and jobs to INSTALLED_APPS:
INSTALLED_APPS = [

    'rest_framework',
    'jobs',
    ...
]

Configure Celery in settings.py
#CELERY_BROKER_URL = 'redis://localhost:6379/0'
#CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'

Create a celery.py file in the same directory as settings.py

In __init__.py of the project directory, add

in linux bash run 
to start redis
sudo apt-get update
sudo apt-get install redis-server
sudo service redis-server start

#Redis will now be running on your WSL instance, and you can connect to it via localhost:6379 from your Windows environment.

#start the celery worker
celery -A job_scheduler worker --loglevel=info
python manage.py runserver
 Testing the API
You can now test your API using tools like Postman or curl:

List Jobs: GET /api/jobs/
Get Job Details: GET /api/jobs/{id}/
Create a Job: POST /api/jobs/ with a JSON body like
{
    "name": "Send Weekly Report",
    "interval": "every Monday",
    "task": "send_email"
}




