# Ex.08 Design of Interactive Image Gallery
# Date: 31/10/2024
# AIM:
To design a web application for an inteactive image gallery with minimum five images.

# DESIGN STEPS:
## Step 1:
Clone the github repository and create Django admin interface.

## Step 2:
Change settings.py file to allow request from all hosts.

## Step 3:
Use CSS for positioning and styling.

## Step 4:
Write JavaScript program for implementing interactivity.

## Step 5:
Validate the HTML and CSS code.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
### Gallery.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Wallpaper Gallery</title>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Montserrat', sans-serif;
      background-color: #1f1f1f;
      color: #ffffff;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    h1 {
      margin-top: 30px;
      font-size: 2.5rem;
      text-align: center;
      letter-spacing: 2px;
      text-transform: uppercase;
    }

    .section {
      width: 100%;
      max-width: 1400px;
      margin: 30px 0;
      padding: 25px;
      background: linear-gradient(135deg, #2a2a2a, #3e3e3e);
      border-radius: 15px;
      box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.5);
    }

    .section h2 {
      text-align: center;
      font-size: 2rem;
      margin-bottom: 20px;
      text-transform: uppercase;
      letter-spacing: 1px;
      position: relative;
      padding-bottom: 10px;
    }

    .section h2::after {
      content: '';
      width: 50px;
      height: 4px;
      background-color: #ff6347;
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      border-radius: 2px;
    }

    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
    }

    .gallery img {
      cursor: pointer;
      width: 400px;
      height: 250px;
      object-fit: cover;
      border: 3px solid #444;
      border-radius: 10px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .gallery img:hover {
      transform: scale(1.07);
      box-shadow: 0px 8px 20px rgba(255, 99, 71, 0.6);
    }

    /* Modal Styling */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.9);
      justify-content: center;
      align-items: center;
      animation: fadeIn 0.5s;
    }

    .modal img {
      max-width: 90%;
      max-height: 80%;
      border: 5px solid #ff6347;
      border-radius: 10px;
    }

    .modal .close {
      position: absolute;
      top: 20px;
      right: 30px;
      font-size: 50px;
      color: #ff6347;
      cursor: pointer;
      transition: color 0.3s ease;
    }

    .modal .close:hover {
      color: #ffffff;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
      }
      to {
        opacity: 1;
      }
    }
  </style>
</head>
{% load static %}
<body>
  <h1>Interactive Wallpaper Gallery</h1>

  <!-- Landscape Anime Wallpapers Section -->
  <div class="section">
    <h2>Landscape Anime Wallpapers</h2>
    <div class="gallery landscape">
      <img src="{% static 'sam1.jpeg' %}" alt="Anime 1">
      <img src="{% static 'sam3.jpeg' %}" alt="Anime 2">
      <img src="{% static 'sam2.jpeg' %}" alt="Anime 3">
      <img src="{% static 'zoro.jpeg' %}" alt="Anime 4">
    </div>
  </div>

  <!-- Landscape Car Wallpapers Section -->
  <div class="section">
    <h2>Landscape Car Wallpapers</h2>
    <div class="gallery landscape">
      <img src="{% static 'carl4.jpeg' %}" alt="Car 1">
      <img src="{% static 'carl1.jpeg' %}" alt="Car 2">
      <img src="{% static 'carl2.jpeg' %}" alt="Car 3">
      <img src="{% static 'carl3.jpeg' %}" alt="Car 4">
    </div>
  </div>

  <!-- Modal for Enlarged Images -->
  <div class="modal" id="modal">
    <span class="close" id="close">&times;</span>
    <img id="modalImg" src="" alt="Modal View">
  </div>

  <script>
    // Select all images in the gallery
    const images = document.querySelectorAll('.gallery img');
    const modal = document.getElementById('modal');
    const modalImg = document.getElementById('modalImg');
    const closeBtn = document.getElementById('close');

    // Add click event to each image
    images.forEach(img => {
      img.addEventListener('click', () => {
        modal.style.display = 'flex';
        modalImg.src = img.src;
        modalImg.alt = img.alt;
      });
    });

    // Close the modal when the close button is clicked
    closeBtn.addEventListener('click', () => {
      modal.style.display = 'none';
    });

    // Close the modal when clicking outside the image
    modal.addEventListener('click', (e) => {
      if (e.target === modal) {
        modal.style.display = 'none';
      }
    });
  </script>
</body>
</html>
```
### views.py
```
from django.shortcuts import render # type: ignore
def gal(request):
    return render(request,'gallery.html')
```
### settings.py
```
from pathlib import Path
import os

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = 'django-insecure-$!-6&=^=$%caeoq)k%*1ce6v=&g5naz3m^lb^!yxebucula+5^'

DEBUG = True

ALLOWED_HOSTS = []

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'photos',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'gallery.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'gallery.wsgi.application'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True

STATIC_URL = 'static/'
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```
### urls.py 
```
from django.contrib import admin # type: ignore
from django.urls import path # type: ignore
from photos import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('gal',views.gal)
]
```
# OUTPUT:
![alt text](<Screenshot 2024-12-19 094724.png>)
![alt text](<Screenshot 2024-12-19 094749.png>) 
# RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
