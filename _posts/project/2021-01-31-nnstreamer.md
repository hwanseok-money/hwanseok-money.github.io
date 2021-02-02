---
title: "[오픈소스 컨트리뷰톤] NNStreamer"
excerpt: "날짜 "
date: 2021-01-30
last_modified_at: 
categories:
  - Project
tags:
  - Project 
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

### 요약
- 2019.9.7. ~ 2019.10.19.
- [NNStreamer](https://github.com/nnstreamer/nnstreamer) 오픈 소스 프로젝트에 참여
- 기여
  1. [tensorflow-light의 image segmentation model filter 개발](https://github.com/nnstreamer/nnstreamer/pull/1801)
  2. [tensorflow-light의 style transfer model filter pipeline design 제안](https://github.com/wooksong/contributon2019-nns/issues/8)
  2. tensorflow-light의 style transfer model과 NNStreammer 사이의 버전 호환성 문제 발견 및 리포트
- c, gstreamer, tensorflow, git
- [컨트리뷰터 커밋 내역](https://github.com/nnstreamer/nnstreamer/commits?author=niklasjang)
- [멘토링 repository](https://github.com/hwanseok-dev/contributon2019-nns)
- [컨트리뷰톤 수료 증명서](/assets/images/about/certification_nnstreamer.pdf)
- [MVP(팀 내 최우수 컨트리뷰터)선정](/assets/images/about/certification_nnstreamer_mvp.pdf)
- [최종 발표영상(발표자)](https://youtu.be/_lkvKkdZAZo)

---  

## Git똥차게 협업하는 즐거움  

1. 진행기간	: 2019-09-03 ~ 2019-11-02(2019 오픈SW 컨트리뷰톤)
2. 주요내용 : '이 코드를 이렇게 작성한 이유'를 전달하는 방법을 배우기 위해, 2019 오픈SW 컨트리뷰톤을 통해 NNStreamer 프로젝트에 참여했습니다. NNStreamer는 신경망들을 Stream Filter로 간주하여 사용할 수 있도록 해주는 GStreamer 플러그인 모음입니다. Gstreamer의 장점에 기대어 파이프라인을 단 한 줄의 명령으로 구성할 수 있기 때문에, 신경망 응용 프로그램 제작에 있어 획기적인 게임체인저가 되고자하는 프로젝트입니다. 
3. 오픈소스 기여 : 오픈소스 기여의 첫 단추는 ISSUE 등록이었습니다. 먼저 기존에 존재하는 문제점을 파악하고 해결 방법을 고민한 뒤 공유했습니다. 그리고 선배 개발자분들과 더 좋은 방법에 대한 논의를 진행한 이후에 개발을 시작했습니다. 개발 과정에서는 모두가 합의한 관습을 준수했고, 각 기능의 선후 관계에 대한 주석을 충분히 적고자 했습니다. 저는 구현된 기능들이 CI/CD 시스템 테스트를 통과한 뒤에 PR 했습니다. 마지막 단계로서 선배 개발자분들께 코드 리뷰를 받은 뒤 MERGE를 했습니다.
4. 협업 : 5명의 멘토들이 배경지식과 실력이 모두 달랐기 때문에 공통의 목표를 정하는 과정이 어려웠습니다. 오타를 수정하는 첫 번째 PR을 진행하면서 NNStreamer를 쉽게 이해할 수 있는 예제가 부족함을 느꼈습니다. 함께 논의한 결과 tensorflow-lite의 image segmentation과 style transfer의 filter를 작성한다는 목표를 세우고 진행했습니다. 가장 기본적인 모델이기 때문에 다양한 NNStreamer 사용자들이 쉽게 접할 수 있다고 생각했기 때문입니다.  
5. 어려움 : 제가 마주했던 두 가지 어려움은 다음과 같습니다. 첫째, 빌드 시스템의 구조가 복잡했습니다. 이를 이해하기 위해 멘티들과 구조를 분석하여 meson이 단계적으로 ninja 빌드 파일을 생성하면 ninja가 빌드해주는 과정을 내제화 하였습니다. 둘째, 진입장벽이 높았습니다. GStreamer와 tensorflow의 도메인을 모두 갖추고 있어야 NNStreamer에 기여할 수 있었습니다. 컨트리뷰톤의 기간이 6주로 제한되어 있었기 때문에 두 도메인에 대해서 best practice를 중심으로 익혔습니다.
6. 공헌 : 저는 tflite가 제공하는 기본 모델들에 대한 stream filter 작성을 맡았습니다. 첫 번째로 image segmentation 모델을 위한 필터 개발 및 pipeline 예제를 제공하였습니다. 두 번째로 style transfer 모델을 위한 필터 개발 중 버전 호환성 문제를 report하였습니다. 이는 모델을 구성하는 operator의 버전과 NNStreamer가 지원하는 tflite 버전 사이의 문제로, 커뮤니티에서도 알지 못했던 critical한 ISSUE였습니다.
7. Skill 또는 지식 : C, Ubuntu18.04LTS, nnstreamer, gstreamer
8. 결과 : https://github.com/nnstreamer/nnstreamer/commits?author=niklasjang
9. 성과 : 역설적이게도 코드를 통해서 개발 의도를 정확하게 전달하기 위해서는 충분한 의사소통이 선행되어야 했습니다. 비록 많은 Commit을 작성하지는 못했지만, Gstreammer와 Tensorflow라는 거대한 Domain을 빠르게 익히고 적용해볼 수 있었던 소중한 시간이었습니다. 게다가 이와 같은 성과를 인정받아 MVP로 선정되어 큰 영광이었습니다.
10. Target Github Repo : https://github.com/nnsuite/nnstreamer/
11. Contribution Github : https://github.com/niklasjang/contributon2019-nns
12. Contribution 발표영상 : https://www.youtube.com/watch?v=_lkvKkdZAZo&t=1s

**Success Notice:**  
감사합니다! :+1:
{: .notice--success}