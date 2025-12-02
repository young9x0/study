---
title: intellij markdown에 이미지 추가 작업 간소화하기
search: true
categories:
- blog
tags:
- markdown
- Liquid
- live template
- PasteImageIntoMarkdown
---
 1. Jekyll Liquid 언어를 사용해  _config.yml에 깃헙 url 관련 변수를 선언
- Jekyll Liquid는 Jekyll에서 사용하는 Ruby 기반의 오픈소스 템플릿 언어
- 정적인 html을 동적으로 만들어준다.
- 변수를 사용할 수 있게 해준다. (오브젝트)
- 논리와 흐름 제어를 제공한다. (태그)
- 함수를 사용할 수 있게 해준다. (필터)
- 참고자료: [Liquid란?](https://fuzzysound.github.io/jekyll-liquid)
- ![]({{site.url}}{{site.baseurl}}/assets/images/538301133291700.png)
- 이와 같이 설정하면 깃헙에 해당 이미지(아래 예에서는 'image_name.png'라는 이름을 가진 것으로 함)를 업로드한 경로를 site변수로 가져올 수 있다.
> ![]({{site.url}}{{site.baseurl}}/assets/images/image_name.png)

2. intellij의 live template 기능을 사용해 1번의 깃헙에 업로드한 이미지 경로를 'jimg+tab'을 입력해 사용할 수 있도록 설정
- 참고자료: 
  [[IntelliJ] 코드 템플릿 - Live Template을 이용하여 자주 사용하는 코드 템플릿화 해보기](https://velog.io/@max9106/IntelliJ-Live-Template)
- ![]({{site.url}}{{site.baseurl}}/assets/images/537630574558299.png)
- ![]({{site.url}}{{site.baseurl}}/assets/images/538967655600499.png)


3. intellij 'PasteImageIntoMarkdown' plugin을 설치
- plugin site: [PasteImageIntoMarkdown](https://plugins.jetbrains.com/plugin/13610-pasteimageintomarkdown)
- 플러그인 설정을 할 때 나는 현재 _posts 폴더 안에서 작업을 하고 있으므로 '..'을 넣어 _posts 폴더를 나와서 이와 형제 사이인 assets 폴더 경로로 이동하도록 수정했다.
- ![]({{site.url}}{{site.baseurl}}/assets/images/537283038591900.png)
- 클립보드의 이미지를 intellij md 에디터 창에 ctrl+v 로 붙여넣기 하면 다음과 같이 임의의 난수가 생성되면서 파일이 'assets/images/'경로에 저장된다.
> ![]({{site.url}}{{site.baseurl}}/assets/images/539220833264600.png)
- ![]({{site.url}}{{site.baseurl}}/assets/images/539220833264600.png)

4. intellij replace 기능으로 './..'을 '{{site.url}}{{site.baseurl}}'로 전체 변경하기

<br />
현재는 jekyll liquid 언어를 지원하는 플러그인이 없어 이 정도로 intellij에서 md에 이미지를 삽입할 때 과정을 간소화할 수 있어보인다.


