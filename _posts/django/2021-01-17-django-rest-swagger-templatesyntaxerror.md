---
title: "[django-rest-swagger] TemplateSyntaxError 에러 발생시 해결 방법"
excerpt: "django.template.exceptions.TemplateSyntaxError: 'staticfiles' is not a registered tag library."
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

## django.template.exceptions.TemplateSyntaxError:  

[공식 docs][1]에 따라서 swagger 연동을 하다보면, 아래와 같은 에러가 발생합니다.  

```txt
django.template.exceptions.TemplateSyntaxError: 'staticfiles' is not a registered tag library. Must be one of:
admin_list
admin_modify
admin_urls
cache
i18n
l10n
log
rest_framework
static
tz
```

`pip install django-rest-swagger`으로 설치한 라이브러리의 문제인데, **github가 read-only로 되어있어서 PR이 현재는 안되는 상황입니다.**

제가 fork 하고 수정해놓은 내용인데 [hwanseok-dev/django-rest-swagger][2]를 보고 따라하시면 됩니다. 저는 `python -m venv theinsta`라는 명령어로 가상환경을 사용해서 을 했는데 위 파일이 다운로드 받아진 경로는 `\theinsta\Lib\site-packages\rest_framework_swagger\templates\rest_framework_swagger`여기 였습니다. 이 경로에 보시면 위 경로에서 수정된 파일이 있는데 똑같이 수정해주시면 됩니다.  

**Success Notice:**
{: .notice--success}

[1]: https://django-rest-swagger.readthedocs.io/en/latest/
[2]: https://github.com/hwanseok-dev/django-rest-swagger/commit/94ab39c5b1f821c2fc1c3bd1453226be3f779609