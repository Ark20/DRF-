# DRF
DRF Tutorial 

* Create & Navigate to project home 
 ```
 mkdir twillionTracker
cd twillionTracker/
```

* Create & Activate virtual environment 
```
python3 -m venv env
source env/bin/activate
```

* Add Django & DRF 

```
pip install django
pip install djangorestframework
```

* Create a DRF Project & app 
 ```
django-admin startproject twillionTracker
cd twillionTracker 

django-admin startapp twillions
cd twillions 
```




#### views.py 

```python
from rest_framework import viewsets
from twillions.models import Twillion
from twillions.serializers import TwillionSerializer

class TwillionsViewSet(viewsets.ModelViewSet):
  queryset = Twillion.objects.all()
  serializer_class = TwillionSerializer
```

#### urls.py

```python

from rest_framework import routers
from twillions import views
from django.urls import path,include


router = routers.DefaultRouter()
router.register(r'twillions', views.TwillionsViewSet)

urlpatterns = [
    path('', include(router.urls)),
    path('admin/', admin.site.urls),
]


```

#### serializers.py

```python
from twillions.models import Twillion
from rest_framework import serializers


class TwillionSerializer(serializers.ModelSerializer):
  class Meta: 
    model = Twillion
    fields = ['name','title','hobby']
 
```

#### models.py

```python
from django.db import models

# Create your models here.

class Twillion(models.Model):
  name = models.CharField(max_length=30, default='')
  title = models.CharField(max_length=30, default='')
  hobby = models.CharField(max_length=50, default='')



```

#### settings.py

```python

'rest_framework',
'twillions.apps.TwillionsConfig',

```

* Create & Sync DB 

```
cd ..
python manage.py makemigrations
python manage.py migrate
```
