---
title: jsp - mac intellj tomcat 연결하기
search: true
categories: 
  - jsp
tags:
  - microsoft-openjdk@21
  - tomcat@9
  - intellij
---
<br />
jdk, tomcat을 mac brew로 설치한다. 그후 intellij에 jdk와 tomcat을 연결한다.

## 1. jdk 설치
> brew search jdk 
> brew install --cask microsoft-openjdk@21
> java —version

![brew_install_jdk.png]({{site.url}}{{site.baseurl}}/assets/images/jsp/brew_install_jdk.png)

## 2. tomcat 설치
> brew search tomcat
> brew install tomcat@9

![brew_install_jdk.png]({{site.url}}{{site.baseurl}}/assets/images/jsp/brew_install_tomcat.png)

> /opt/homebrew/opt/tomcat@9/bin/catalina run

![run_tomcat_at_terminal]({{site.url}}{{site.baseurl}}/assets/images/jsp/run_tomcat_at_terminal.png)

## 3. intellij에 jsp 프로젝트 생성
- [intellij tomcat 연동하기](https://velog.io/@ccorgi1997/JSP-M1-%EB%A7%A5-%EC%9D%B4%ED%81%B4%EB%A6%BD%EC%8A%A4-%EC%9D%B8%ED%85%94%EB%A6%AC%EC%A0%9C%EC%9D%B4-Tomcat-%EC%97%B0%EB%8F%99-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%84%9C%EB%B2%84-%EB%91%90%EA%B0%9C-%EB%8F%99%EC%8B%9C%EC%97%90-%EC%98%AC%EB%A6%AC%EA%B8%B0) 이 블로그 글을 참고했다.
- 다만 jdk 경로 설정 부분에서 자세한 설명이 없어 애를 먹었는데 jdk를 설치하면 다음 경로에 jvm이 생설되어 있을 것이다. 해당 home 폴더를 선택해주면 된다. 
- 예를 들면 `/Library/Java/JavaVirtualMachines/microsoft-21.jdk/Contents/Home
![config_new_project]({{site.url}}{{site.baseurl}}/assets/images/jsp/config_new_project.png)
- 프로젝트가 생성되었다면 서버를 tomcat으로 설정해준다.


## 4. tomcat server 연동하기
- tomcat home dir path에서도 한참을 헤맸는데 앞서 블로그 설명과 다르게 libexec로 설정한다. 예를 들어 나는 `/opt/homebrew/Cellar/tomcat@9/9.0.96/libexec`였다.
![set_tomcat_home_path]({{site.url}}{{site.baseurl}}/assets/images/jsp/set_tomcat_home_path.png)
- application_context는 '/'로 설정한다.
![run_configurations_application_context]({{site.url}}{{site.baseurl}}/assets/images/jsp/run_configurations_application_context.png)

## 5. server 실행하기
- 실행이 정상적으로 되면 다음과 같이 보인다.
![connect_tomcat_success]({{site.url}}{{site.baseurl}}/assets/images/jsp/connect_tomcat_success.png)
![show_browser]({{site.url}}{{site.baseurl}}/assets/images/jsp/show_browser.png)

# reference
- [adoptopenjdk8와 openjdk@8의 차이점은 무엇인가?](https://adjh54.tistory.com/216)
- [Unexpected method 'appcast' called on Cask adoptopenjdk-jre.](https://built.tistory.com/m/74)
![brew_appcast_error.png]({{site.url}}{{site.baseurl}}/assets/images/jsp/brew_appcast_error.png)
