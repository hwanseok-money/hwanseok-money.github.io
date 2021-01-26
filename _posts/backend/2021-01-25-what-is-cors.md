---
title: "[Back-end] CORS(Cross-Origin Resource Sharing)"
excerpt: "API 요청이 forbidden되는 이유"
date: 2021-01-25
last_modified_at: 2021-01-25 
categories:
  - Backend
tags:
  - Backend
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 backend의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

# CORS란

웹 개발을 하다가 CORS 정책을 위반해서 API로부터 데이터를 받아오지 못한 경험이 있습니다. CORS는 허용되지 Origin에서 요청을 받았을 때 발생하는 에러입니다.  

## CORS Error Message 

하나씩 차근차근 정리해서 아래와 같은 CORS가 발생해도 당황하지 않도록 해보겠습니다.  

```
Access to fetch at ‘https://hwanseok-dev.github.io/’ from origin ‘http://localhost:3000’ has been blocked by CORS policy: No ‘Access-Control-Allow-Origin’ header is present on the requested resource. If an opaque response serves your needs, set the request’s mode to ‘no-cors’ to fetch the resource with CORS disabled.
```

## Origin 구성

아래의 URL은 크게 다섯 가지 구조로 나누어져 있습니다.  

```
https://hwanseok-dev.github.io:443/posts?categories=backend#CORS란?  
``` 

1. Protocol : https://
1. Host(Port) : hwanseok-dev.github.io:443
1. Path : posts
1. Qeury String : ?categories=backend
1. Fragment : #CORS란? 

여기서 **Protocol + Host + Port**를 합친 것을 `Origin(출처)`라고 합니다.  

브라우저의 콘솔에서 해당 페이지의 origin을 확인할 수 있습니다.  

```javascript
console.log(location.origin)
```   

## SOP, CORS

`SOP(Same-Origin Policy)`는 같은 리소스가 있는 origin과 같은 origin에서만 리소스를 요청할 수 있다는 정책입니다. SOP만을 고집하면 웹 생태계를 활용할 수 없어서, 예외 사항으로 허용할 수 있는 origin을 추가하고 허용한 것이 `CORS(Cross-Origin Resource Sharing)`입니다.  


## Why CORS

보안을 위해서 입니다. `CSRF(Cross-Site Request Forgery)`나 `XSS(Cross-Site Scripting)`와 같은 방법으로 서비스의 정보와 소스코드를 확인하지 못하도록 하기 위해서 입니다.  

## Origin을 비교하는 주체는 Browser

Origin을 비교 할 때 port를 완전 무시하는 브라우저는 Internet Explorer가 있었고 지금은 사장되었습니다.  

서버가 허용된 origin 없이 SOP만을 적용하는 경우가 아니라면, 임의의 사용자가 서버에 요청을 보내고 서버는 응답할 수 있습니다. 서버의 응답이 CORS를 위반한 사용자에 의한 응답임을 판단하고 정보를 차단하는 것은 Browser가 하는 역할입니다.  

Browser는 서버의 응답 Response Header에서 `access-control-allow-origin: *`를 확인합니다. 그리고 자신이 요청한 origin과 비교하고 응답의 유효성을 판단합니다.  


## CORS의 동작 방식

세 가지가 있습니다. 

1. Preflight Request : 
  - Browser가 OPTION(예비 요청)을 보내고, Server는 CORS정책 정보를 전송한다
  - Browser는 요청을 보내는 것이 안전한 경우 GET(본 요청)을 보낸다. 
  - **Server에서는 OPTION에 응답했기 때문에 200이 떨어지고, 그 이후에 Brower에서 CORS 위반을 판단한다.**
  - OPTION이 실패했어도 (server에서 200이 아닌 다른 상태코드), server의 응답에 `access-control-allow-origin:`가 포함되어 있다면 CORS 위반이 아니다.
1. Simple Request:
  - OPTION 없이 바로 본 요청을 보내어 CORS를 확인하는 방식
  - OPTION을 보내고 응답받지 않는 것만 다를 뿐, 본 요청의 응답에 `access-control-allow-origin:`가 포함되어 있다.
  - Simple Request를 수행하기 위해서는 [까다로운 조건](https://evan-moon.github.io/2020/05/21/about-cors/#simple-request)을 만족해야 한다.  
1. Credentialed Request
  - 다른 출처 간 통신 보안을 강화하고 싶을 때 사용하는 방식
  - `쿠키`와 `인증` 관련 정보를 `요청 헤더`에 포함시켜주는 옵션 `credentials`을 사용한 방식
    1. same-origin (기본값)	같은 출처 간 요청에만 인증 정보를 담을 수 있다(chrome의 default value)
    2. include	모든 요청에 인증 정보를 담을 수 있다
      - **Browser의 `credentials인증` 모드가 include일 경우, 모든 요청을 허용한다는 의미의 *를 Access-Control-Allow-Origin 헤더에 사용하면 안된다**
    3. omit	모든 요청에 인증 정보를 담지 않는다
  - 인증정보가 담겨 있는 상태(same-origin으로의 요청 또는 include)에서 다른 출처의 리소스를 요청하면 브라우저는 CORS 위반 여부 검사에 두 가치를 추가한다. 
    1. Access-Control-Allow-Origin에는 *를 사용할 수 없으며, 명시적인 URL이어야한다.
    1. 응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야한다.
  - `Credentialed_Request`을 사용하는 과정은 [출처](https://evan-moon.github.io/2020/05/21/about-cors/#credentialed-request)에서 확인할 수 있습니다.  

## CORS 예방하는 방법 

1. Server : 정석대로 `Access-Control-Allow-Origin:`를 명시한다!  
1. Client : Proxy를 사용한다!  

### Proxy 사용하는 방법

서버에서 CORS 설정에 localhost를 추가하는 일은 없기 때문에, local front 환경에서 서버에 요청을 날릴 수 있도록 해주는 `proxy`를 사용해야 합니다. `webpack` 또는 `webpack-dev-server`를 사용해서 개발 환경을 구출할 때 `proxy` 설정을 해주면 됩니다.  

아래의 설정은 `fetch('/api/me');`의 요청에 대해서 `localhost:8000/api/me`로 요청을 보내는 것으로 Browser를 속이고, webpack이 뒤에서 `https://api.evan.com/api/me`으로 요청을 보내줍니다. 즉, Proxy 설정을 통해서 CORS 정책을 우회하는 것입니다.  

```javascript
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'https://api.evan.com',
        changeOrigin: true,
        pathRewrite: { '^/api': '' },
      },
    }
  }
}
```

### 개발환경에서만 동작하는 Proxy

개발환경에서는 `webpack-dev-server`가 `proxy`를 해주지만 운영 환경에서는 `webpack-dev-server`가 없어 `proxy`를  해주지 않습니다.  

예를 들어 클라이언트 앱의 출처는 `https://www.evan.com`이고 api 서버는 `https://api.evan.com`이라고 해보겠습니다. `fetch('/api/me');`요청에 대해서, 위에서 언급한 대로, 개발환경에서는 잘 동작합니다. 하지만 운영 환경에서는 `https://www.evan.com/api/me`로 엉뚱한 요청을 보냅니다.  

### 그럼 운영환경에서는?  

인턴을 할 때 보았던 운영환경에서의 방법은 `BaseUrl`을 사용하는 방법입니다. 기본적으로 소스코드에는 운영 환경에서의 URL이 BaseUrl로 되어있다. 그리고 로컬환경에서는 BaseUrl을 수정해서 사용하는 방법을 사용했습니다.   

## Reference

- <https://evan-moon.github.io/2020/05/21/about-cors/>

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}