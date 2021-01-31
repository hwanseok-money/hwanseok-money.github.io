---
title: "[Django] 모델 생성 방법"
excerpt: "https://docs.djangoproject.com/en/3.1/topics/db/models/"
date: 2021-01-30
last_modified_at: 
categories:
  - Django
tags:
  - Django
  - The Polls
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 django의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

# 모델 생성

[hwanseok-dev/the-insta의v1.0][1]를 기준으로 정리하겠습니다. 현재는 Todo class만 존재하는 상태입니다. 여기에 Todo 테이터를 생성한 사용자 정보를 도입해보겠습니다.  

한 명의 사용자는 여러 개의 Todo를 생성할 수 있습니다. 1 : M 관계에서 FK는 M쪽이 가져야하기 때문에 Todo Class에 FK를 추가합니다.  

```python
class Todo(models.Model):
    title = models.CharField(max_length=120)
    description = models.TextField()
    completed = models.BooleanField(default=False)
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name='owner_todo')

    def _str_(self):
        return self.title
```

사용자 테이블은 Auth에서 제공하는 `auth_user` 테이블을 사용하기 위해서 아래와 같이 
`py manage.py createsuperuser`으로 한 명의 사용자를 생성합니다. User Class를 따로 생성하는 것이 더 옳은 방법이지만 우선은 코드 수정을 간소화하기 위해서 이와 같이 진행하겠습니다.    

Todo app의 models.py에서 수정을 했으므로 아래의 두 명령을 수행합니다.

1. python manage.py makemigrations todo
1. python manage.py migrate



**Success Notice:**
{: .notice--success}

[1]: https://github.com/hwanseok-dev/the-insta/tree/v1.0
[2]: https://docs.djangoproject.com/en/3.1/topics/db/models/