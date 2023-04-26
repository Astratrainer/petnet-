---
title: "How to add an image in a Django Project - step by step explanation and guide"
seoTitle: "How to setup media/static connection on django."
datePublished: Wed Apr 26 2023 12:59:23 GMT+0000 (Coordinated Universal Time)
cuid: clgxpdetp000209kyh6272nqh
slug: how-to-add-an-image-in-a-django-project-step-by-step-explanation-and-guide
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682513866708/6ca0c3b2-5bc2-452c-80dc-fa0d9bb1ea7a.webp
tags: python, django, backend, images, frontend-development

---

### **Step 1: Define a model with ImageField**

The first step is to define a model that has an ImageField. For example, let's say we have a model called "Product" which has a field for an image:

```python
class Blog(models.Model):
    title = models.CharField(max_length = 200)
    description = models.TextField(null=True, blank = True)
    featured_image = models.ImageField(null = True, blank = True, default = "default.jpeg")
    demo_link = models.CharField(max_length = 200, null = True, blank = True)
    source_link = models.CharField(max_length = 200, null = True, blank = True)
    tags = models.ManyToManyField('Tag', blank = True)
    vote_total = models.IntegerField(default = 0, null = True, blank = True)
    Vote_ratio = models.IntegerField(default = 0, null = True, blank = True)
    created = models.DateTimeField(auto_now_add = True)
    id = models.UUIDField(default = uuid.uuid4,unique = True, primary_key = True, editable = False)
```

As we can see we have added the field featured\_image in Blog model. The image field is of type ImageField and has a upload\_to parameter which specifies where the image should be uploaded.

This will provide you the image field to upload in the Django backend admin panel as shown in the image below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682512181287/6159edea-d194-48f5-9941-7c3b0669edcc.png align="center")

### **Step 2: Add Media Settings**

Next, we need to add URL patterns for serving media files in our project [urls.py](http://urls.py) file.

```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'static/images')
STATIC_URL = '/images/'
```

As in the code above, we can add static media for image storage which will promote the images automatically

### **Step 3: Add URL patterns**

Next, we need to add URL patterns for serving media files in our project [urls.py](http://urls.py) file.

```python
from django.conf import settings 
from django.conf.urls.static import static 
```

And then we add the urls in urls.py file so that the image appears in our pages in front-end as shown in the code below:

```python
urlpatterns += static(settings.MEDIA_URL, document_root= settings.MEDIA_ROOT )
```

Here, we are importing the static function from django.conf.urls.static and the settings module from Django, and then adding a URL pattern that serves media files.

### **Step 4: Add a form to upload images**

Now, let's create a form to upload images. In your [forms.py](http://forms.py) file, define a form that has a FileField or ImageField for the image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513125144/baf4d54f-eec1-4c17-b6f6-b21608c5f7fd.png align="center")

Here, we are creating a form called "BlogForm" that has fields for the title, description, demo\_link, source\_link, tags and featured\_image of a product.

### **Step 5: Add a view to handle form submission**

Next, we need to create a view that handles the form submission and saves the image to the database.

```python
from django.shortcuts import render, redirect
from .forms import BlogForm
def createBlog(request):
    form = BlogForm()

    if request.method =='POST':
        form = BlogForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('blogs')
    context = {'form':form}
    return render (request, 'blog_form.html',context)
```

Here, we are defining a view called "createBlog" that handles the form submission. We check if the request method is POST, and if it is, we create a BlogForm instance with the data and files from the request. If the form is valid, we save the data to the database and redirect to the blogs page. If the request method is not POST, we create an empty ProductForm instance and render the "blog\_form.html" template with the form instance.

### **Step 6: Display images in templates**

Finally, we can display the images in our templates using the MEDIA\_URL and the image field of our model.

```python
{% extends 'major.html' %}

{% block content %}
<img src = "{{blog.featured_image.url}}">

<h1>{{blog.title}}</h1>
<hr>
{% for tag in blog.tags.all %}
    <span style = "border:1px solid grey">{{tag}}</span>

{% endfor %}
<hr>
<p>{{blog.description}}</p>

{% endblock content %}
```

After this we can view the image in the front-end as shown below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513690563/c92bab4a-db08-48a5-82de-835bf10babc4.png align="center")

After submitting the image from the back-end we can view the image in the front end as shown below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513753554/b0ddc0db-70f1-4ff2-89ee-b70f0865bc20.png align="center")

Then when we open the first blog we can view our uploaded image as:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513797458/ffe94791-a438-4577-8682-0ad7b3909932.png align="center")

Thank you for reading the blog, hope this will help for your project. If you have any questions, i am more than happy to help you for your project.