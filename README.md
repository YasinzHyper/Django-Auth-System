# 🔐 Django Auth System

A robust and modular **user authentication system** built with Django. It provides clean registration, login, logout, password management, and email verification flows—ready to integrate into any Django project.

---

## 📋 Table of Contents

1. [Overview](#overview)  
2. [Features](#features)  
3. [Tech Stack & Dependencies](#tech-stack--dependencies)  
4. [Project Structure](#project-structure)  
5. [Setup & Installation](#setup--installation)  
6. [Usage](#usage)  
7. [Security Considerations](#security-considerations)  
8. [Contributing](#contributing)  
9. [License](#license)

---

## 💡 Overview

This Django-based project handles common user authentication flows out-of-the-box:

- ✅ User **registration** (with email confirmation option)  
- 🔐 **Login** and **logout**  
- 🔄 **Password reset** via email  
- 🔒 Secure password hashing and session management :contentReference[oaicite:1]{index=1}

It’s designed as a standalone app that you can incorporate into your own Django projects as a reusable authentication layer.

---

## ✅ Features

- Register new users with **email** and **username**  
- Login/logout with Django’s authentication backend  
- Reset forgotten passwords with **tokenized email flow**  
- Optional **email confirmation** upon registration  
- Profile update form (email, username, password)  
- Clean, minimalistic **Bootstrap-based UI**

---

## 🛠️ Tech Stack & Dependencies

- **Python 3.8+**, **Django 4.x**  
- Built-in `django.contrib.auth`, `django.contrib.sessions`, `django.contrib.messages`  
- **Bootstrap 5** for styling and responsive templates  
- Optional Email backend (SMTP/Gmail) for confirmation flows :contentReference[oaicite:2]{index=2}  
- SQLite by default (configurable for PostgreSQL/MySQL)

---

## 🗂️ Project Structure

```

django\_auth\_system/
├── authentication/      # Main app handling auth logic and views
│   ├── templates/
│   │   └── authentication/  # Registration, login, password reset templates
│   ├── forms.py         # Custom forms for registration, login, password change
│   ├── urls.py          # URL routes for auth views
│   └── views.py         # View logic for all auth flows
├── project/             # Django project settings and main configurations
│   ├── settings.py
│   ├── urls.py
└── manage.py

````

---

## ⚙️ Setup & Installation

```bash
git clone https://github.com/MisaghMomeniB/Django-Auth-System.git
cd Django-Auth-System
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
````

Configure email settings in `project/settings.py`:

```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = '<your-email>@gmail.com'
EMAIL_HOST_PASSWORD = '<app-password>'
```

Run migrations and start the server:

```bash
python manage.py migrate
python manage.py runserver
```

---

## 🚀 Usage

Access these routes:

* `/register/` – Create a new account
* `/login/` – Sign in to your account
* `/logout/` – Sign out
* `/password-reset/` – Request a password reset link
* `/password-reset-confirm/...` – Set a new password
* `/profile/` (optional) – Update user details

Templates are customizable—update them in `authentication/templates/authentication/`.

---

## 🔐 Security Considerations

* Secure password hashing with Django’s default **PBKDF2**
* Time-limited tokens for password reset and email confirmation
* CSRF protection and session security from Django middleware
* Optional **email confirmation** to verify user addresses ([github.com][1])

---

## 🤝 Contributing

Improvements are welcome! You could add:

* Social login (OAuth) integration
* Two-factor authentication (2FA)
* Customizable email templates and styling
* Unit tests for views and form validity

**To contribute**:

1. Fork the repo
2. Create a branch (`feature/...`)
3. Implement changes with tests
4. Open a Pull Request

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` file for details.
