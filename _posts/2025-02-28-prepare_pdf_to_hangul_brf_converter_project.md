---
title: 자료조사 - brf converter 프로젝트 준비
search: true
categories:
  - project
tags:
  - brf
  - braille-ascii
  - braille-unicode
---
pdf to hangul brf file converter project를 위한 자료조사 내용을 기록한다.
<br />



# 1. 출력용 점자 파일 형식

[개정 점자 도서 제작 지침](https://www.nld.go.kr/upload/contents02/nld_jumja_jeajack_jichim(2019.3.).pdf) 제4장 전자형 점자 자료 제작 지침 제2절 1. 전자형 점자 자료의 외형 형식은 다음과 같이 정의되어 있다.
> 전자형 점자 자료는 출력용 점자 파일 형식인 BRF, BRL, BBF의 형태로 제작한다. 

이에 따라 본 프로젝트에서는 우선 brf형식으로 파일을 제공하며 추후 필요시 다른 확장자도 지원하기로 한다.


## 점자파일의 종류
  - 점자파일이란 점자 표시기나 점자 생성기에 사용되는 특수한 형식의 데이터 파일이다.
  - 출력용 점자 문서 파일 확장자로는 brf, bbf, brl 등이 있다.
  - 점자 음성 겸용 파일 확장자는 vbf가 있다.
  - 데이지(DAISY) 파일이란 시각장애인이 도서를 오디오 형식으로 들을 수 있도록 인쇄자료를 스캔하여 도서의 원본 그대로를 데이지국제표준에 맞게 편집한 디지털 전자파일 자료이다.

출처: [우리는 점글을 사랑합니다](https://blog.naver.com/gktkrk/223327656996)


<br />
<br />


# 2. 점자 변환 형식, 유니코드 vs 점자 아스키 

컴퓨터에서 우리 눈에 점자 형태로 보여지는 형식은 유니코드로 변환한 결과이다.   
다음 예시 문장을 보자.
> 매년 11월 4일은 ‘점자의 날’이다. 

위의 문장을 유니코드로 변환하면 다음과 같다.
> ⠑⠗⠉⠡⠀⠼⠁⠁⠏⠂⠀⠼⠙⠕⠂⠵⠀⠠⠦⠨⠎⠢⠨⠣⠺⠀⠉⠂⠴⠄⠕⠊⠲⠀

이를 brf로 변환하면 다음과 같다.
> erc* #aap1 #do1z ,8.s5.<w c10'oi4 

먼저 한글을 유니코드로 변경하는 규칙을 살펴보자.  ([점자로 코드 주석 참고](https://github.com/teamdotsix/jumjaro/blob/develop/Jumjaro/Braille.cs))
먼저 한글 점자를 구성하는 번호 위치는 아래와 같다.
     
       (1) (4)
       (2) (5)
       (3) (6)

점자 번호를 역순으로 나열해서 2진수로 계산하면 해당 점자 코드가 나온다. 
> ⠓ (1-2-5)일 경우  
 점자 유무로 표기 = "1 1 0 0 1 0 0 0"  
 역순 이진법 = "00010011(19, 0x13)"  
 점자 유니코드는 U+2800 부터 시작하므로 0x2800 + 0x13 = 0x2813  
즉 U+2813이 해당 점자의 유니코드가 된다.


<br />
<br />

brf 파일은 기본적으로는 [점자 아스키](https://ko.wikipedia.org/wiki/%EC%A0%90%EC%9E%90_%EC%95%84%EC%8A%A4%ED%82%A4)로 이뤄지지만 점자의 인쇄, 표시 방법을 제어하는 제어 문자를 포함한다. 
여기서 점자 아스키(Braille ASCII)는 0x20에서 0x5F까지의 64개 아스키 문자를 사용한다.    
  

본 프로젝트를 위해 필요한 글자 변환 과정은 다음과 같다.
1. pdf를 한글 text로 변환
2. 한글 text를 점자 아스키로 변환
3. 점자 아스키를 brf 확장자 파일로 저장
  

여기에 사용자에게 화면으로 점자를 유니코드로 변환해 보여주고 싶다면 다음 과정을 추가하면 된다. 
- 한글 text를 유니코드로 변환

<br />
<br />


확인 결과 1, 2 두 가지 과정을 구현한 라이브러리가 존재한다. 다만 2의 경우는 자바스크립트로 되어 있어 파이썬으로 변경이 필요하다.  
한편, 한글 text의 줄바꿈 기준으로 점자 아스키 또한 띄어쓰기가 되기 때문에 점자 에디터처럼 균일한 column에 맞게 개행문자를 추가해주지 못하는 문제가 발생한다.
기본 포멧을 32 column을 한 줄로 설정한다면 2번 과정을 다음과 같이 세분화 해야 한다.  

2-1. 한글 text를 유니코드로 변환  

2-2. 유니코드를 32글자씩 묶고 마지막에 개행문자 추가  

2-3. 개행문자가 추가된 유니코드를 한글 text로 변형  

2-4. 개행문자가 추가된 한글 text를 점자 아스키로 변형  

유니코드를 바로 점자 아스키로 변형해주면 과정이 단순화되나 현재 개발된 라이브러리를 사용하는 방법으로 진행해서 부득이하게 2-3 과정이 추가되었다. 이 부분은 추후 보완이 필요하다.

<br />
<br />


# 3. 관련 라이브러리

1. pdf to text
  - [pdfminer.six](https://github.com/hyonzin/hangul-braille-converter): python
2. text to hangul braille
  - [hanbraille](https://github.com/delvier/hanbraille): javascript, update 11개월 전, braile ascii와 유니코드 두 가지 타입 반환 지원
* [Hangul to Braille Converter](https://github.com/hyonzin/hangul-braille-converter) : python, update 8년 전, 숫자 배열 반환만 지원  

2-3. [BrailleToKor_Python](https://github.com/Bridge-NOONGIL/BrailleToKor_Python) : python, update 3년 전


