---
title: "[React] export default class ClassName"
excerpt: ""
date: 2021-01-30
last_modified_at: 
categories:
  - Frontend
tags:
  - Frontend 
  - React
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 React의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

# export default class ClassName

default 키워드가 없으면 named export를 의미합니다. name export는 아래와 같이 하고,  

```javascript
class Template {}
class AnotherTemplate {}

export { Template, AnotherTemplate }
```

다른 파일에서 import할 때에는 { }를 사용해야 합니다.  

```javascript
import {Template, AnotherTemplate} from './components/templates'
```  

default 키워드를 사용하면 {} 없이 import 할 수 있습니다.  

```javascript
export default class Template {}

import Template from './components/templates'
```

default export는 파일 하나당 한 개만 가능하고, import하는 파일에서 이름을 바꾸어서 import해도 됩니다. 어차피 export할 수 있는 component는 하나뿐이므로 인식이 가능합니다.  

```javascript
import TheTemplate from './components/templates'
```

그리고 default export와 named export를 동시에 하는 것도 가능합니다.  

```javascript
import Template,{AnotherTemplate} from './components/templates'
```  

# Reference

- https://stackoverflow.com/questions/31852933/why-es6-react-component-works-only-with-export-default

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}