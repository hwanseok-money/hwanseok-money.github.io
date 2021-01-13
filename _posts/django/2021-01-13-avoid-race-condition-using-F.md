---
title: "[Django] F() 사용해서 race condition 피하기"
excerpt: "가변 (키워드)인자의 사용법"
date: 2021-01-13
last_modified_at: 
categories:
  - Django
tags:
  - Django
  - race condition
  - F()
  - selected_choice.votes = F('votes')+1
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 django의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

## 필요성

The Polls 프로젝트를 진행하다가 [여기][1]에서 `F()`에 대한 설명을 보았습니다. DB에 저장된 row의 field의 값을 1 증가시키는 버튼이 view에 존재한다고 해보겠습니다. **여러 사용자가 정확히 동시에 그 버튼을 누른다면** race condition에 의해서 한 사용자의 입력이 무시될 수 있습니다.  

각 사용자가 버튼을 누르면 다음과 같이 3단계로 진행됩니다. DB에는 값이 1이 저장된 상태라고 해보겠습니다.  

1. A 사용자 : DB에서 값 retrieve (1)
1. A 사용자 : python에서 값 증가 (2)
1. A 사용자 : DB에 값 저장 (2)

만약 두 사용자가 동시에 버튼을 클릭하면 아래와 같이 진행될 수 있습니다.  

1. A 사용자 : DB에서 값 retrieve (1)
1. B 사용자 : DB에서 값 retrieve (1)
1. A 사용자 : python에서 값 증가 (2)
1. A 사용자 : DB에 값 저장 (2)
1. B 사용자 : python에서 값 증가 (2)
1. B 사용자 : DB에 값 저장 (2)

원래는 값이 3으로 저장되어야 하는데 race condition에 의해서 사용자 A의 입력이 무시됩니다.  

## Avoiding race conditions using F()

이를 위해서 cpp에서는 mutex를 사용하는데, django에서는 `F()`를 사용할 수 있습니다. python이 아닌 database가 field를 update하는 권한을 찾게 됩니다. `F()`를 사용하면 database는 `save()` 또는 `update()`가 실행되었을 때의 DB에 저장된 값을 기준으로 field를 update합니다.  

selected_choice 객체의 votes field를 update할 때 아래와 같이 진행할 수 있습니다.  

```python
# selected_choice.votes += 1
selected_choice.votes = F('votes')+1
```

아래는 전체 view 예시 입니다.  

```python
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        # selected_choice.votes += 1
        selected_choice.votes = F('votes')+1
        selected_choice.save()
        return HttpResponseRedirect(reverse('ns_polls:results', args=(question.id,)))

```

## F() assignments persist after Model.save()

주의할 점은 `save()`를 호출한 이후에도 `F()`를 적용한 것이 유지된다는 점입니다. 아래의 경우에 

```python
reporter = Reporters.objects.get(name='Tintin')
reporter.stories_filed = F('stories_filed') + 1
reporter.save()

reporter.name = 'Tintin Jr.'
reporter.save()
```

stories_filed의 값은 `save()`를 호출할 때마다 총 2번 +1 됩니다.  

`F()`의 적용을 풀기 위해서는 아래의 메서드를 사용해서 객체를 refresh 하면 됩니다.  

```python
reporter.refresh_from_db()
```

## Reference

- [args-and-kwargs][2]

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}

[1]: https://docs.djangoproject.com/ko/3.1/ref/models/expressions/#avoiding-race-conditions-using-f
[2]: https://www.programiz.com/python-programming/args-and-kwargs