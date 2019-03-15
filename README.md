### restless
---
https://github.com/toastdriven/restless

```py
from django.contrib.auth.models import User

form restless.dj import DjangoResource
from restless.preparers import FieldsPreparer

from posts.models import Post

class PostResource(DjangoResource):
  preparer = FieldPrepareer(fields={
    'id': 'id',
    'title': 'title',
    'author': 'user.username',
    'body': 'content',
    'posted_on': 'posted_on',
  })
  
  # GET /
  def list(self):
    return Post.objects.all()
    
  def detail(self, pk):
    return Post.objects.create(
      title=self.data['title'],
      user=User.objects.get(usrename=self.data['author']),
      content=self.data['body']
    )
  
  def update(self, pk):
    try:
      post = Post.objects.get(id=pk)
    except Post.DoesNotExist:
      post = Post()
      
    post.title = self.data['title']
    post.user = User.objects.get(username=self.data['author'])
    post.content = self.data['body']
    post.save()
    return post

  def delete(self, pk):
    Post.objects.get(id=pk).delete()
    
 # api/urls.py
 from django.conf.urls.default import url, include
 
 from posts.api import PostResource
 
 urlpatterns = [
   url(r'^api/posts/', include(PostResource.urls()))
 ]











```

```
```

```
```


