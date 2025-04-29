```markdown
# 🔐 Django Authentication and Authorization System

A secure and extensible user authentication and authorization system built with Django.

This project demonstrates how to build a complete login/registration flow with access control using Django best practices. Ideal for backend developers who want to learn or showcase user management systems in Django.

---

## 🚀 Features

- ✅ Custom User Model with email as username
- ✅ User Registration & Login System
- ✅ Logout with session management
- ✅ Protected Dashboard (login required)
- ✅ Django Best Practices (custom forms, views, templates)
- ✅ Clean project structure

---

## 📁 Project Structure

```
auth_system/
├── auth_system/         # Main Django project folder
│   ├── __init__.py
│   ├── settings.py      # Project settings
│   ├── urls.py          # Main URL configuration
│   └── wsgi.py
│
├── accounts/            # Authentication app
│   ├── admin.py
│   ├── apps.py
│   ├── models.py        # Custom user model
│   ├── views.py         # Views: register, login, logout, dashboard
│   ├── forms.py         # Registration/Login forms
│   ├── urls.py          # URLs specific to auth
│   └── templates/
│       └── accounts/
│           ├── login.html
│           ├── register.html
│           └── dashboard.html
│
├── manage.py
```

---

## 🛠️ How to Run the Project

### 1. 📦 Clone the Repository

```bash
git clone https://github.com/yourusername/django-auth-system.git
cd django-auth-system
```

### 2. 🐍 Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
```

### 3. 📥 Install Dependencies

```bash
pip install django
```

### 4. 🔧 Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. 🚀 Run Development Server

```bash
python manage.py runserver
```

Now open your browser and visit:  
👉 `http://127.0.0.1:8000/`

---

## 🌐 App URLs

| URL                          | Purpose             |
|-----------------------------|---------------------|
| `/register/`                | Register new user   |
| `/login/`                   | Login existing user |
| `/logout/`                  | Logout user         |
| `/dashboard/`               | Protected page      |

---

## ✍️ Implementation Details

### 🔸 Custom User Model

Used to extend the default Django `User` and use email as the unique identifier:

```python
# accounts/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    email = models.EmailField(unique=True)

    def __str__(self):
        return self.email
```

And in `settings.py`:

```python
AUTH_USER_MODEL = 'accounts.CustomUser'
```

---

### 🔸 Forms

```python
# accounts/forms.py

from django import forms
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
from .models import CustomUser

class CustomUserCreationForm(UserCreationForm):
    class Meta:
        model = CustomUser
        fields = ('username', 'email', 'password1', 'password2')

class CustomAuthenticationForm(AuthenticationForm):
    username = forms.EmailField(label='Email')
```

---

### 🔸 Views

```python
# accounts/views.py

from django.shortcuts import render, redirect
from django.contrib.auth import login, logout
from django.contrib.auth.decorators import login_required
from .forms import CustomUserCreationForm, CustomAuthenticationForm

def register_view(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            login(request, user)
            return redirect('dashboard')
    else:
        form = CustomUserCreationForm()
    return render(request, 'accounts/register.html', {'form': form})

def login_view(request):
    if request.method == 'POST':
        form = CustomAuthenticationForm(request, data=request.POST)
        if form.is_valid():
            user = form.get_user()
            login(request, user)
            return redirect('dashboard')
    else:
        form = CustomAuthenticationForm()
    return render(request, 'accounts/login.html', {'form': form})

def logout_view(request):
    logout(request)
    return redirect('login')

@login_required
def dashboard_view(request):
    return render(request, 'accounts/dashboard.html')
```

---

### 🔸 URL Configuration

```python
# accounts/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.register_view, name='register'),
    path('login/', views.login_view, name='login'),
    path('logout/', views.logout_view, name='logout'),
    path('dashboard/', views.dashboard_view, name='dashboard'),
]
```

```python
# auth_system/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('accounts.urls')),
]
```

---

## 🧪 Templates

### register.html

```html
<h2>Register</h2>
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Register</button>
</form>
<a href="{% url 'login' %}">Already have an account?</a>
```

### login.html

```html
<h2>Login</h2>
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Login</button>
</form>
<a href="{% url 'register' %}">Create an account</a>
```

### dashboard.html

```html
<h2>Welcome, {{ request.user.username }}</h2>
<a href="{% url 'logout' %}">Logout</a>
```

---

## ⚙️ Django Settings

```python
# settings.py

LOGIN_URL = 'login'
LOGIN_REDIRECT_URL = 'dashboard'
LOGOUT_REDIRECT_URL = 'login'
```

---

## 📌 Requirements

- Python 3.x
- Django 4.x+
- Virtualenv (optional, recommended)

---

## 📄 License

This project is open-source and free to use under the [MIT License](LICENSE).

---

## ✨ Author

Created with ❤️ by **Misagh**  
[LinkedIn](https://www.linkedin.com/in/misaghmomenib/) — [GitHub](https://github.com/MisaghMomeniB)

```
