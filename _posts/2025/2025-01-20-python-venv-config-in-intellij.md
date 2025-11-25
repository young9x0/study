---
title: intellij python venv(가상환경) 설정
search: true
categories: 
  - python
tags:
  - intellij 
  - venv
---
intellij에서 프로젝트별 python venv(가상환경)을 설정하는 방법을 기록한다.

<br />

1. .venv 폴더 생성
원하는 프로젝트 폴더에서 다음 명령을 통해 해당 프로젝트에서만 쓸 가상환경을 생성한다.
나의 경우 speech-recognition-takashima 폴더에서 다음 명령어를 실행해 .venv를 생성했다.
> python -m venv .venv

<br />

![make .venv]({{site.url}}{{site.baseurl}}/assets/images/intellij-python-venv-config/after-python-venv-command.png)

2. intellij project structure platform setting sdks 설정
- intellij에서 해당 프로젝트의 prject structure으로 들어간다.(단축키 _command + ;_ 를 사용한다) 
- 다음과 같이 platform setting - sdks 메뉴로 들어가 새로 생성한 python을 sdk에 등록해준다.
  - existing environment 을 선택한 후 폴더 경로를 다음과 같이 프로젝트 안의 *.venv/bin/python*으로 설정해준다.


<br />

![intellij project structure platform setting sdks]({{site.url}}{{site.baseurl}}/assets/images/intellij-python-venv-config/intellij-project-structure-python-sdk-config.png)


### 참고 문서
[[개발로그 Python] 가상환경 venv 사용해서 여러 형상 사용(intellij)](https://myjamong.tistory.com/285)