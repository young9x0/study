---
title: 점사랑 설치 시 msvcp140.dll 파일 없음 에러 해결
search: true
categories:
  - braille
tags:
  - braillove5
  - braile-editor
---
<br />

mac m1에서 점사랑 프로그램을 지원하지 않아 vmware 가상서버에 window11 64 bit arm을 설치해서 돌려보았다.
<br />
점사랑5.0 설치파일을 국립국어원 홈페이지에서 다운받아 설치 파일을 실행하니 msvcp140.dll 파일이 없다는 에러가 발생했다. 같은 문의에 대한 답변을 보니 이 파일은 visual studio 2015용 visual c++ 재배포 가능 패키지의 일부 파일로, 윈도우 설치 시 혹은 업데이트할 때 자동으로 설치되는 필수 패키지입니다. 하지만, 어떤 이유로 파일이 손상되었거나 업데이트 누락으로 설치되지 않아 내 컴퓨터에 msvcp140.dll 파일이 존재하지 않아 발생하는 오류입니다.
microsoft 공식 웹사이트에서 microsoft visual c ++ 재배포 가능 패키지 파일을 다운로드하라고 되어있었다.
<br />
'Visual Studio 2015용 Visual C++ 재배포 가능 패키지'로 검색해서 vc_redist.x86.exe를 다운로드 받으면 된다.(점사랑 파일이 86 bit로 되어 있다.)

![점사랑5.0](https://recursive-o.github.io/voice-processing/assets/images/braillove5.png)

<br />
참고로 점사랑 2.0 수검용은 압축풀기 에러로 설치가 되지 않는다.

# 참고 자료
[점사랑 프로그램 설치 오류 관련한 문의](http://www.kbuwel.or.kr/Board/QNA/Detail?page=32&contentSeq=1214643)