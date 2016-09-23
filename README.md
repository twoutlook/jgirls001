# c9.io ubuntu 14.04, setup workinging environment

    sudo apt-get install -y python3.5 python3.5-venv
    
# python3.5, setup workinging environment    
    python3.5 -m venv myvenv
    source myvenv/bin/activate
    pip install django
    pip install --upgrade pip
    

# djangogirls,  create a new project mysite
https://tutorial.djangogirls.org/en/django_start_project/ 
NOTE: django-admin startproject mysite is bettern than django-admin startproject mysite .
    django-admin startproject mysite 
    cd mysite
    ./manage.py runserver $IP:$PORT
    
# edit settings 
    TIME_ZONE = 'Asia/Taipei'
    
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')

# c9.io, new terminal 
    source myvenv/bin/activate
    cd mysite

    ./manage.py collectstatic
    
    
    ./manage.py makemigrations
    ./manage.py migrate
    
    ./manage.py createsuperuser



# Create a new App
    ./manage.py startapp blog
    
# Add App to settings 
    INSTALLED_APPS = [
        'blog', 
    
# add model Post
    from django.db import models
    from django.utils import timezone
    
    
    class Post(models.Model):
        author = models.ForeignKey('auth.User')
        title = models.CharField(max_length=200)
        text = models.TextField()
        created_date = models.DateTimeField(
                default=timezone.now)
        published_date = models.DateTimeField(
                blank=True, null=True)
    
        def publish(self):
            self.published_date = timezone.now()
            self.save()
    
        def __str__(self):
            return self.title
# migrate Db
    
    ./manage.py makemigrations
    ./manage.py migrate
    
# register App to Admin
    from django.contrib import admin
    from .models import Post
    
    admin.site.register(Post)
    
# login to Admin and add some Posts

# add urls to mysite

    from django.conf.urls import include, url
    from django.contrib import admin
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),
        url(r'', include('blog.urls')),
    ]
    
# Create Template
## base.html
    
    {% load staticfiles %}
    <html>
    
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <!--<link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>-->
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    
    <body>
        <div class="page-header">
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>
        <div class="content container">
            <div class="row">
                <div class="col-md-8">
                    {% block content %} {% endblock %}
                </div>
            </div>
        </div>
    </body>
    
    </html>

# post_list.html
    {% extends 'blog/base.html' %}

    {% block content %}
        {% for post in posts %}
            <div class="post">
                <div class="date">
                    {{ post.published_date }}
                </div>
                <h1><a href="">{{ post.title }}</a></h1>
                <p>{{ post.text|linebreaksbr }}</p>
            </div>
        {% endfor %}
    {% endblock %}


# blog.css


   
# add views
    from django.shortcuts import render
    from django.utils import timezone
    from .models import Post
    
    def post_list(request):
        posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
        return render(request, 'blog/post_list.html', {'posts': posts})
    
# add urls to blog
    
    from django.conf.urls import url
    from . import views
    
    urlpatterns = [
        url(r'^$', views.post_list, name='post_list'),
    ]
        
    
    
# others    
    git clone https://github.com/twoutlook/hiring001.git
    
    cd hiring001
    cd myproject
    cp db.1.sqlite3 db.sqlite3
    
    ./manage.py collectstatic
    
    
    ./manage.py makemigrations
    ./manage.py migrate
    
    ./manage.py createsuperuser
    
    ./manage.py runserver $IP:$PORT

    
#New Project

    django-admin startproject mysite .
    
    
    TIME_ZONE = 'Asia/Taipei'
    
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')
    
    
    ./manage.py makemigrations
    ./manage.py migrate
    
    ./manage.py createsuperuser
    
    ./manage.py runserver $IP:$PORT# jgirls001
