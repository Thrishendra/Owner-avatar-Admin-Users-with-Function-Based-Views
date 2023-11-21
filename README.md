
# Ex-03-Admin User using function-based views
STUDENT DETAILS :

Name : T.Thrishendra

Department : AIDS

Reference No : 23003501

# AIM : 
Display Admin User's data using function based views in django framework.
# STEP 1 : Create a Django Project
Create django project using the following commands:

Django-admin startproject mymodels

# STEP 2 : Create a Django App
Create django app using the following command

Python manage.py startapp myapp

# STEP 3 : Define User Creation View

In your app's views.py file (myapp/views.py), define a view function to create the users with the specified attributes.

To create a Django website with five users (two staff users, including an admin, and three non-staff users), set email, first name, and last name for all users, you can use the following Python view function:
```
from django.contrib.auth.models import User
from django.shortcuts import render

def create_users(request):
    # List of users to create
    users_to_create = [
        {'username': 'admin', 'password': 'adminpass', 'is_staff': True, 'is_superuser': True, 'email': 'admin@example.com', 'first_name': 'Admin', 'last_name': 'User'},
        {'username': 'staff1', 'password': 'staff1pass', 'is_staff': True, 'email': 'staff1@example.com', 'first_name': 'Staff', 'last_name': 'User1'},
        {'username': 'user1', 'password': 'user1pass', 'email': 'user1@example.com', 'first_name': 'User', 'last_name': 'One'},
        {'username': 'user2', 'password': 'user2pass', 'email': 'user2@example.com', 'first_name': 'User', 'last_name': 'Two'},
        {'username': 'user3', 'password': 'user3pass', 'email': 'user3@example.com', 'first_name': 'User', 'last_name': 'Three'},
    ]

    # Loop through users and create them
    for user_data in users_to_create:
        username = user_data['username']
        password = user_data['password']

        # Check if the user already exists
        if not User.objects.filter(username=username).exists():
            # Create user
            user = User.objects.create_user(username=username, password=password)

            # Set additional attributes
            user.is_staff = user_data.get('is_staff', False)
            user.is_superuser = user_data.get('is_superuser', False)
            user.email = user_data.get('email', '')
            user.first_name = user_data.get('first_name', '')
            user.last_name = user_data.get('last_name', '')

            # Save the user
            user.save()
            print(f"User created with username: {username}")
        else:
            print(f"User with username {username} already exists.")

    return render(request, 'myapp/user_creation_success.html')

```
# STEP 4 : Create Templates
Create a template directory within your app (myapp/templates) if it doesn't already exist. Inside this directory, create a template named 'user_creation_success.html' to display a success message.
user_creation_success.html : 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin User Created</title>
</head>
<body>
    <h1>Admin User Created Successfully</h1>
</body>
</html>
```

 # STEP 5 : Define URL pattern
 In your app's urls.py file (myapp/urls.py), define a URL pattern to route to the create_users view.
```
"""mypro URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/4.1/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path

from myapp import views
from myapp.views import create_users

urlpatterns = [
    path('admin/', admin.site.urls),
    path('create_users/', views.create_users, name='create_users'),
]

```

# STEP 6: Apply Migrations
Apply migrations to create the necessary database tables for the User model.
python manage.py makemigrations
python manage.py migrate

# STEP 7: Run the Development Server
Start the development server to run your Django application.
python manage.py runserver

# Step 9: Verify the Users
You can verify that the users have been created with the specified attributes by checking the Django admin interface.

Visit http://localhost:8000/admin/ 


Note: Don't forget to add myapp in the settings.py file

```
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "myapp",
]
```
# OUTPUT : 
User Profiles creation successful:


![image](https://github.com/SANTHAN-2006/ODD2023-WT-Ex-04-Django-Models/assets/80164014/a0f7939e-0d34-467a-a75b-3f675e430d95)

Verifying the Admin Users :


![image](https://github.com/SANTHAN-2006/ODD2023-WT-Ex-04-Django-Models/assets/80164014/cc0723dc-23b5-42cd-ba94-96a882d7c79d)

# RESULT : 
Created a Django website with five users. Two users are to be staff users (including admin) and the other three users are non-staff users successfully

