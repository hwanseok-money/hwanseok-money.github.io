---
title: "[Webinar] Microsoft Azure Virtual Training Day: Fundamentals 1일차"
excerpt: "Microsoft Certified: Azure Fundamentals"
date: 2021-01-14
last_modified_at: 
categories:
  - Webinar
tags:
  - webinar
  - microsoft
  - azure
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
`Microsoft Azure Virtual Training Day: Fundamentals 1일차`의 내용을 정리하는 포스팅입니다.  
{: .notice--info}

# 소개말

# 모듈 0: 학습과정  소개

본 포스팅은 [여기](https://docs.microsoft.com/ko-kr/learn/certifications/)에서 확인가능한 자격증의 가장 기초 자격증(AZ-900)에서 다루는 내용입니다.  

# 모듈 1: 클라우드 개념

## 클라우드 서비스의 정의와 장점

컴퓨팅 자원을 자체적으로 보유하던 방식을 `on-premise`라고 합니다. 반대로 컴퓨팅 자원을 원격 환경에서 운용하는 방식을 `cloud`라고 합니다.  

클라우드는 크게 세 가지 장점을 가지고 있습니다. `비용`,`생산성`,`낮은 진입장벽`입니다. 

1. 비용
    - 클라우드의 특성상 사용량이 많을 때는 자원을 많이 사용하고, 사용량이 줄어들 때는 과금을 중단할 수 있습니다.
1. 생산성
    - 사용량이 급증/급감하는 경우 컴퓨팅 자원을 확장/축소하기 위한 비용을 절감할 수 있습니다.(요청 - 승인 - 발주 - 수령 - 세팅의 과정을 생략)
    - 클라우드 환경을 수 초 ~ 수 분 내에 테스트(업무에 집중)할 수 있습니다.
1. 낮은 진입장벽
    - 하둡 등의 환경을 클라우드 플랫폼에서 패키지화 해서 제공해서 쉽게 접근할 수 있습니다. 

## 주요 개념 및 용어

- `내결함성(Fault tolerance)`
  - fault 발생시 어떻게 대응할 것인지 고려되어서 설계된 서비스입니다.
  - 내결함성의 구현 방식에는 `백업 후 복원`, `복제된 데이터 저장`등이 있습니다. 
- `고 가용성(High availability, HA)`
  - 클라우드 자원을 사용하지 못해서 발생하는 down time을 최소화하고 고객의 서비스를 `장시간 중지 없이 운용`하는 것에 집중되어 있습니다.
  - 예를 들어 `primary server`와 `secondary sever`를 나누어서 운용할 때, Primary server에 문제가 발생할 시 secdondary server가 primary의 역할을 수행할 수 있습니다.
- `재해 복구(Disaster recovery, DR)`
  - 자연재해로부터 물리적으로 벗어난 지역에서 연결된 서비스를 제공합니다. 
- 민첩성(Agility)
  - scale up/out을 빠르게 할 수 있습니다. 
- 확장성((Scalability)
  - 시스템 자원이 빠르게 늘어나는 성질을 말합니다.
- 탄력성(Elasticity)
  - 시스템 자원이 빠르게 줄어들 수 있는 성질을 말합니다.
- 글로버 지원(Global reach)
  - 대부분의 cloud vecdor(공급 업체)들은 global 서비스를 지원합니다.
  - cloud를 사용하는 서비스의 해외 진출을 용이하도록 돕기 위함입니다.
- 응답 속도(Customer latency)
  - 해외 지역의 사용자들이 물리적 거리에 의해 레이턴시를 경험하는데, 글로벌 지원을 하는 Azure를 사용하면 글로벌 서비스 확장시 사용자들이 경험하는 레이턴시를 최소화합니다.  
- 예측 비용(Predictive cost)
  - 비용 예측 가능합니다. 
- 보안(Security)
  - 보안 시스템 구축 및 검증을 대신 수행해줍니다.  

## 비용적 측면의 클라우드의 이점

**규모의 경제(Econommies of scale)** 

`규모 경제`의 개념은 작은 규모로 운영하는 것에 비해 더 큰 규모로 운영할 때 더 저렴하고 효율적으로 작업을 수행할 수 있는 능력입니다.

클라우드 제공업체는 매우 큰 비즈니스를 하기에 규모 경제의 이점을 활용한 후 그 혜택을 고객에게 배분하는 것이 가능합니다.

## CapEx vs. OpEx

`자본지출` : Capital Expenditure
  - 물리적 인프라에 대한 지출을 `선불`로 지불
  - 시간이 지남에 따라 세금 계산서에서 비용을 공제
  - 높은 초기 비용, 투자 가치는 시간이 지남에 따라 감소
  - `public cloud`를 사용하면 자본지출은 0이 됩니다. 
`운영 비용` : Operational Expenditure
  - 필요에 따라 서비스 또는 제품에 지출되고 즉시 청구
  - 같은 해에 세금 계산서에서 비용을 공제
  - 선 결제 비용이 없고, 종량제 사용
  - `public cloud`를 사용하면 운영 비용만 지불하면 됩니다. 


## 소비 기반 모델(Consummption-based model)

- 선 결제 비용 없음
- 비용이 많이 드는 인프라를 구매하고 관리할 필요가 없음
- 필요한 경우에 한해서만 추가 리소스에 대한 비용을 지불할 수 있음
- 더 이상 필요하지 않은 리소스는 비용 지불 중단 가능

## Public Cloud

- **클라우드 서비스 또는 호스팅 공급자가 소유**
- 여러 조직과 사용자에게 리소스와 서비스를 제공
- 보안 네트워크 연결을 통해 접근(일반적으로 인터넷을 통해 연결, vendor와 client 사이에 VPN 또는 ER로 연결하기도 함)
- `여러 고객사`를 위해 사용됨.
- `소비기반모델`
- 자본지출이 없습니다. 확장을 위해 새 서버를 구매할 필요가 없습니다.
- 민첩합니다. 응용 프로그램이 빠르게 액세스 할 수 있으며 필요할 때마다 `\*프로비저닝`을 해제할 수 있습니다.  

`\*프로비저닝(provisioning)` : 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요 시 시스템을 즉시 사용할 수 있는 상태로 미리 준비해 두는 것

## Private Cloud

- 클라우드 리소스를 **사용하는 조직이 소유 및 운영**
- 조직은 그들의 데이터 센터에 클라우드 환경을 구축
- 조직 내의 사용자에게 제공되는 리소스에 대한 셀프 서비스 액세스를 제공
- 조직에게 본인들이 제공하는 서비스를 운영할 책임
- 제어력. 조직은 리소스를 완벽하게 제어할 수 있습니다.
- 보안. 조직은 보안을 완벽하게 제어할 수 있습니다.

## Hybrid Cloud

공용 및 사설 클라우드를 결합하여 응용 프로그램이 가장 적합한 위치에서 실행되도록 합니다.  

- 유동성. 가장 유연한 시나리오
- 업체는 하이브리드 클라우드 설정을 통해 앱을 사설 클라우드에서 실행할지, 공용 클라우드에서 실행할지의 여부를 결정할 수 있습니다.
- 준수성. 조직은 필요에 따라 엄격한 보안, 규정 준수 또는 법적 요구 사항을 준수할 수 있는 기능을 유지합니다.(비용 상승 가능성)

## 클라우드 모델 비교




VM / App, Web / Email


프라이빗 클라우드
- 안전 X 안심 O

## 공동 관리 책임

![azure-0-0](/assets/images/webinar/azure-0-0.jpg)  

대략적으로 `Iaas`는 VM, `PaaS`는 App/Web, `SaaS`는 email이라고 생각할 수 있습니다.  

- Iaas[아이아스] : 물리적 + 가상화 + Guest OS + 보안
  - 가장 기본적인 클라우드 컴퓨팅 서비스 범주
  - 클라우드 공급자로부터 가상 머신, 스토리지, 네트워크 및 운영체제를 대여하여 종량제 IT 인프라를 구축
  - 네트워크를 통해 프로비저닝 및 관리되는 컴퓨팅 인스턴스
- PaaS[파쓰]
  - 소프트웨어 응용 프로그램을 개발, 테스트 및 배포하기 위한 환경을 제공
  - 기본 인프라 관리에 신경쓰지 않고, 응용 프로그램을 신속하게 만들 수 있도록 한다.
- Saas[싸쓰]
  - 커스터마이징 할 수 있는 부분이 거의 없다.
  - 최종 사용자를 위해 중앙에서 호스팅되고 관리되는 소프트웨어입니다.
  - 사용자는 인터넷을 통해 클라우드 기반 앱에 연결하고 사용합니다. 설치가 필요없다.
  - 예를 들어 Office 365, 전자 메일 및 일정을 예로 들 수 있습니다. 

## 클라우드 서비스 타입 비교

- Iaas[아이아스] : 유동성(자차)
  - 가장 유연한 클라우드 서비스
  - 앱을 실행하는 운영체제를 구성하고 관리할 수 있는 제어력을 가지고 있다.
- PaaS[파쓰] : 생산성(랜트카)
  - 응용 프로그램 개발에만 집중할 수 있다.
  - 플랫폼 관리자는 클라우드 공급자입니다.
- Saas[싸쓰] : 종량제(택시)
  - 사용자는 자신의 구독에서 사용하는 소프트웨어에 대한 비용만 지불합니다. 

## Review : 연습 문제

1. 다음 중 클라우드  서비스의 이점을 설명한 항목은?
    1. 규모의 경제(정답)
    1. 고정된 워크로드
    1. 예측할 수 없는 비용
1. 다음 중 미리 질불한 후 시간이 지남에 따라 공제되는 비용을 나타내는 용어는?
    1. 자본 지출(정답)
    2. 운영 비용
    3. 공급과 수요
1. 다음 중 장기간 가동 중지 시간 없이 서비스를 사용할 수 있도록 하는 특성은?
    1. 민첩성
    1. 내결함성
    1. 고가용성(정답)
    1. 성능
1. 어떤 클라우드 모델이 가장 높은 수준의 소유권과 제어를 제공합니까?
    1. 프라이빗(정답)
    1. 하이브리드
    1. 공용
1. 어떤 클라우드 모델이 가장 큰 유연성을 제공합니까?
    1. 프라이빗
    1. 하이브리드(정답)
    1. 공용
1. 다음 중 공용 클라우드를 설명한 항목은?
    1. 해당 클라우드의 리소스를 사용하는 조직에서 소유하고 운영한다.
    1. 클라우드 또는 온-프레미스에서 애플리케이션을 실행할 수 있다.
    1. 보안 네트워크 연결을 통해 연결하는 여러 조직 및 사용자에게 리소스와 서비스를 제공한다. (정답)
1. 다음 중 PaaS(서비스형 플랫폼)을 설명한 항목은 무엇입니까?
    1. 사용자는 운영체제, 미들웨어 및 앱 등 자체 소프트웨어를 구매,설치,구성 및 관리할 책임이 있다.
    1. 사용자는 기본 인프라 관리에 대해 걱정할 필요 없이 신속하게 애플리케이션을 만들고 배포할 수 있다.(정답)
    1. 사용자는 연간 또는 월간 구독료를 지불한다.
1. 전문 메인프레임 하드웨어가 필요한 레거시 앱과 최신의 공유 앱이 있는 경우 어떤 클라우드 배포 모델이 가장 적합한가?
    1. 프라이빗
    1. 하이브리드(정답)
    1. 공용
1. 다음 중 사용자의 관리가 가장 많이 필요한 클라우드 서비스는 무엇인가?
    1. 프라이빗(정답)
    1. 하이브리드
    1. 공용


# 모듈 2: 핵심 Azure 서비스

##  핵심 Azure 아키텍처 구성 요소

`Region`은 서로 근접한 `Data Center`의 묶음입니다. 사용자가 `VM`을 생성요청을 보낼 때 Region을 선택해야합니다. 단, Data Center는 지정하지 않습니다. Data Center는 같은 Region에 소속되어서 서로 간의 Latency가 작습니다.  

Region은 Paired Region를 가집니다. 한국 중부 Region과 한국 남부 Region이 Paired Region입니다. 서로 Disaster Recovery 용도로 서로 도와서 운용됩니다. 

VM 배포시 가용성을 유지하기 위해서는 최소 2개 이상의 VM을 배포해야 합니다. 그런데 두 개의 VM이 동일한 `Physical Server`(아래 그림의 노란색)에서 VM이 생성되면 안됩니다. VM을 설정할 때 `AvailableSet`을 설정해서 VM을 배포하면, `Fault Domain`이라는 것을 통해서, 서로 다른 `Physical Server`에 분산되어서 VM이 생성된다.  

또한 Azure 자체의 긴급 보안 배치시 물리 서버 전체를 내리는 것이 아니라, MS가 정한 update domain의 단위에 따라 서비스가 중단될 수 있습니다. 중단되는 단위는 Update Domain이라고 하고, 아래 그림에서 점선과 같은 형태로 나누어집니다. 다수의 Physical Data Center들에 속한 VM들을 하나로 묶어서 나누어서 업데이트를 진행합니다.    

마지막으로 DC 전체가 무너졌을 때를 대비해서 `AvailableZone`을 설정할 수 있습니다. 여러 개의 Physical Server를 포함하는 Data Center가 실패했을 때를 대비하기 위한 설정입니다.  

![azure-0-1](/assets/images/webinar/azure-0-1.jpg)  

## Regions

Azure는 전 세계에 위치한 데이터 센터로 구성됩니다. 지역이란 지도 상의 하나의 지리적 영역으로, 적어도 하나 이상의 데이터 센터를 포함하고 있습니다. 지역 안에 데이터 센터는 서로 근접한 위치에 있어 네트워크 대기 시간이 짧습니다.  

## Region Pairs

각 Azure region은 다른 region과 페어링 연결되어 있습니다. 이들 사이의 데이터 센터들은 적어도 300마일 거리 이상이 떨어져 있습니다. 

## 지리 Geographics

데이터 상주 및 규정 준수 경계를 보존하는 개별 시장입니다. 미주/유럽/아시아 태평양/중동 및 아프리카로 분류됩니다. 

## 가용성 옵션

프리미엄 스토리지를 사용하는 경우 단일 VM을 배포해도 연결성을 99.9% 보장해준다.  

## Azure 논리적 구조 이해하기

`구독`은 아래의 단위
  1. 비용. 각 층에서 이용하는 비용은 각 층의 비용으로 정산됨
  2. 접근제어. 각 층의 접근체어
  3. 기술적 제한. 1 구독시 1만개의 VM까지만 생성가능하도록 설정 가능. 넘는 경우 여러 개으ㅢ 구독으ㅡㄹ 해야 함.
    - 구독을 나누는 기준은? 클라이언트에 따라 다르다. 

사내의 프로제긑가 많은 경우 하나의 계정으로만 구독해서 모두 그 계정을 사용하면 월마다 어떤 프로제긑에서 얼마 과금됐는지 나눠야 한다. 구독 아래 용도에 따라 Resource Group을 나눠서 관리할 수 있다.(트ㅡ리 구조의 RG 에서 권한 관리 및 삭제가 용이하다)

### Azure 글로벌 인프라 이해하기

![azure-0-2](/assets/images/webinar/azure-0-2.jpg)

![azure-0-3](/assets/images/webinar/azure-0-3.jpg)

![azure-0-4](/assets/images/webinar/azure-0-4.jpg)

![azure-0-5](/assets/images/webinar/azure-0-5.jpg)

![azure-0-6](/assets/images/webinar/azure-0-6.jpg)

![azure-0-7](/assets/images/webinar/azure-0-7.jpg)

![azure-0-8](/assets/images/webinar/azure-0-8.jpg)

![azure-0-9](/assets/images/webinar/azure-0-9.jpg)

![azure-0-10](/assets/images/webinar/azure-0-10.jpg)

![azure-0-11](/assets/images/webinar/azure-0-11.jpg)

![azure-0-12](/assets/images/webinar/azure-0-12.jpg)

![azure-0-13](/assets/images/webinar/azure-0-13.jpg)

![azure-0-14](/assets/images/webinar/azure-0-14.jpg)

![azure-0-15](/assets/images/webinar/azure-0-15.jpg)

![azure-0-16](/assets/images/webinar/azure-0-16.jpg)

![azure-0-17](/assets/images/webinar/azure-0-17.jpg)

![azure-0-18](/assets/images/webinar/azure-0-18.jpg)


# 맺음말

추가적인 자료는 아래에서 확인가능합니다.  

- <https://docs.microsoft.com/ko-kr/learn/paths/azure-fundamentals/>

- <https://docs.microsoft.com/ko-kr/learn/modules/create-an-azure-account/>

# Reference

- Microsoft Azure Virtual Training Day: Fundamentals 1일차

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}
