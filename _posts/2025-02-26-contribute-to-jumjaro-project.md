---
title: 점자로 프로젝트 contribute하기
search: true
categories:
  - contribute
tags:
  - jumjaro
  - dotnet_sdk
  - crlf
---
점자번역기 [점자로](https://jumjaro.org/) 프로젝트에 기여한 과정을 기록한다.
<br />

## dotnet-sdk 설치하기

C# 언어로 된 코드는 처음 보는 나로써는 프로젝트를 어떻게 실행시켜야 하는지부터 난감했다. C#으로 작성되었다는 것도 파일 확장자 `.cs`를 검색해보고 알았다.
폴더마다 하나씩 있는 `.csproj`를 살펴보니 파일 맨 윗부분에 공통적으로 `<Project Sdk="Microsoft.NET.Sdk">`란 부분이 보였다. 아무래도 이 sdk를 설치해야 프로그램을 실행할 수 있어보여 검색해보니 mac에는 brew로 dotnet-sdk를 설치하면 된다는 것을 알게 되었다.
[mac에 dotnet 환경 설정](https://anyons.net/?p=2525)에 따라 다음 명령어로 sdk를 설치해주었다.

> brew install --cask dotnet-sdk

이렇게 설치한 dotnet-sdk version는 9.0.2 이었다.

## dotnet 프로젝트 실행하기
[[ C# ] Hello World!](https://mu7a7ion.tistory.com/34) 대로 따라해보니 `.csproj`가 포함된 폴더로 경로를 이동해 `dotnet run`을 하면 이 파일이 실행되며 각 폴더의 코드가 실행되는 구조라는 걸 이해할 수 있었다.

점자로 프로젝트의 폴더 구조는 다음과 같다.
```
├── Jumjaro
├── JumjaroCLI
├── JumjaroTest
├── JumjaroWeb
└── JumjaroWebServer
```
모든 폴더에 들어가 `dotnet run`을 실행해보았다. JumjaroCLI 폴더에서는 해당 명령어가 실행은 되나 다음 에러가 발생했다.
> error CS0246: The type or namespace name 'TestCase' could not be found (are you missing a using directive or an assembly reference?)

구글링 결과 sdk 버전이 프로젝트와 맞지 않을 때 발생하는 오류로 보였다. `.csproj`를 확인해보니 TargetFramework의 버전이 netcoreapp3.1이라서 sdk버전도 이에 맞춰서 다시 설치해보았다.
```
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>
```

기존 버전을 우선 다음 명령어로 삭제해주었다.
> brew uninstall dotnet-sdk


원하는 버전 설치 방법은 [Multiple versions of .Net Core on Macos with brew](https://stackoverflow.com/questions/55387250/multiple-versions-of-net-core-on-macos-with-brew)를 보고 따라했더니 성공했다.

> brew tap isen-ng/dotnet-sdk-versions  
> brew install --cask dotnet-sdk3

cli를 다음 명령어로 실행하니 다음과 같이 정상 작동했다.

> dotnetx64 run "~" --brf


![run cli]({{site.url}}{{site.baseurl}}/assets/images/jumjaro-contributing/run-cli.png)

이 명령어를 실행하면 프로젝트 폴더에 bin과 obj가 자동으로 생성된다. 파이썬의 가상환경 설정 시 자동으로 생성되는 .venv 폴더와 비슷한 역할을 하는 것으로 보였다.
  
  

## test code 실행하기
JumjaroTest 폴더로 경로를 이동해 test code를 실행해보려 하는데 `dotnetx64 run`로는 실행이 되지 않았다.
구글링 결과 [NUnit 사용 단위 테스트(Unit Test)](https://www.dotnetnote.com/docs/testing/unit-testing-with-nunit/)에서 단위테스트 실행 명령어가 `dotnet test`라는 걸 알아냈다.

다음 명령어를 project root 경로에서 실행하니 
> dotnetx64 test

다음과 같은 결과가 나왔다.
```
Test run for /Users/juyoung/pjs/jumjaro/JumjaroTest/bin/Debug/netcoreapp3.0/JumjaroTest.dll(.NETCoreApp,Version=v3.0)
Microsoft (R) Test Execution Command Line Tool Version 16.7.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

A total of 1 test files matched the specified pattern.

Test Run Successful.
Total tests: 290
     Passed: 290
 Total time: 2.1459 Seconds
```
 
일부러 실패 케이스를 만들어 확인해보니 정상 작동했다.
다음 성공 케이스에 일부러 오타를 만들었다.
```
[TestCase("한글 점자", "⠚⠒⠈⠮⠀⠨⠎⠢⠨")]
```

다음과 같이 코드를 수정하고 테스트 케이스를 다시 돌려보았다. 
```
[TestCase("한글 점다", "⠚⠒⠈⠮⠀⠨⠎⠢⠨")]
```

의도한 대로 실패했다.
```
Test run for /Users/juyoung/pjs/jumjaro/JumjaroTest/bin/Debug/netcoreapp3.0/JumjaroTest.dll(.NETCoreApp,Version=v3.0)
Microsoft (R) Test Execution Command Line Tool Version 16.7.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

A total of 1 test files matched the specified pattern.
  X ToJumja("한글 점다","⠚⠒⠈⠮⠀⠨⠎⠢⠨") [96ms]
  Error Message:
     String lengths are both 9. Strings differ at index 8.
  Expected: "⠚⠒⠈⠮⠀⠨⠎⠢⠨"
  But was:  "⠚⠒⠈⠮⠀⠨⠎⠢⠊"
  -------------------^

  Stack Trace:
     at JumjaroTest.JumjaroTests.ToJumja(String testStr, String expected) in /Users/juyoung/pjs/jumjaro/JumjaroTest/JumjaroTests.cs:line 12


Test Run Failed.
Total tests: 290
     Passed: 289
     Failed: 1
 Total time: 2.2008 Seconds
```



## pull request
먼저 jumjaro github을 fork한 후 내 로컬 컴퓨터에 프로젝트 폴더를 clone해주었다. feature branch를 새로 생성해서 다음과 같이 코드를 추가해주었다.

먼저 현재 점자로 프로젝트에서 구현되지 않은 문장부호(겹낫표, 홑낫표, 겹화살괄호, 홑화살괄호, 줄표, 붙임표, 물결표)를 `/Jumjaro/PunctuationMarkBraille.cs` 파일에 추가해보았다.


```
namespace Jumjaro
{
    class PunctuationMarkBraille
    {
        private static readonly Dictionary<char, string> _brailleMap = new Dictionary<char, string>()
        {
            ... 앞 부분 생략
            
            { '『', "⠰⠦" },
            { '』', "⠴⠆" },
            { '《', "⠰⠶" },
            { '》', "⠶⠆" },
            { '「', "⠐⠦" },
            { '」', "⠴⠂" },
            { '〈', "⠐⠶" },
            { '〉', "⠶⠂" },
            { '―', "⠤⠤" }, // 줄표(dash)/긴 줄표(horizontal bar)
            { '-', "⠤" }, // 붙임표(hypen)
            { '~', "⠈⠔" },
         };
```

또한 기여 시 주의사항에 단위테스트로 추가한 코드를 확인해달라는 요청이 있어 `/JumjaroTest/JumjaroTests.cs` 파일에 다음과 같이 관련 테스트 케이스를 추가해주었다.
```
    namespace JumjaroTest
    { 
      public class JumjaroTests
      {
          앞 부분 생략 ...
          
          [TestCase("[윤석중 전집(1988), 70쪽 참조]", "⠦⠆⠩⠒⠠⠹⠨⠍⠶⠀⠨⠾⠨⠕⠃⠦⠄⠼⠁⠊⠓⠓⠠⠴⠐⠀⠼⠛⠚⠠⠨⠭⠀⠰⠣⠢⠨⠥⠰⠴")]
          [TestCase("훈민정음』은 1997년에 유네스코 세계 기록 유산으로 지정되었다.", "⠚⠛⠑⠟⠨⠻⠪⠢⠴⠆⠵⠀⠼⠁⠊⠊⠛⠀⠉⠡⠝⠀⠩⠉⠝⠠⠪⠋⠥⠀⠠⠝⠈⠌⠀⠈⠕⠐⠭⠀⠩⠇⠒⠪⠐⠥⠀⠨⠕⠨⠻⠊⠽⠎⠌⠊⠲")]
          [TestCase("이 곡은 베르디가 작곡한 「축배의 노래」이다.", "⠕⠀⠈⠭⠵⠀⠘⠝⠐⠪⠊⠕⠫⠀⠨⠁⠈⠭⠚⠒⠀⠐⠦⠰⠍⠁⠘⠗⠺⠀⠉⠥⠐⠗⠴⠂⠕⠊⠲")]
          [TestCase("《한성순보》는 우리나라 최초의 근대 신문이다.", "⠰⠶⠚⠒⠠⠻⠠⠛⠘⠥⠶⠆⠉⠵⠀⠍⠐⠕⠉⠐⠣⠀⠰⠽⠰⠥⠺⠀⠈⠵⠊⠗⠀⠠⠟⠑⠛⠕⠊⠲")]
          [TestCase("백남준은 2005년에 〈엄마〉라는 작품을 선보였다.", "⠘⠗⠁⠉⠢⠨⠛⠵⠀⠼⠃⠚⠚⠑⠀⠉⠡⠝⠀⠐⠶⠎⠢⠑⠶⠂⠐⠣⠉⠵⠀⠨⠁⠙⠍⠢⠮⠀⠠⠾⠘⠥⠱⠌⠊⠲")]
          [TestCase("이번 토론회의 제목은 ‘역사 바로잡기 ― 근대의 설정 ―’이다.", "⠕⠘⠾⠀⠓⠥⠐⠷⠚⠽⠺⠀⠨⠝⠑⠭⠵⠀⠠⠦⠱⠁⠇⠀⠘⠐⠥⠨⠃⠈⠕⠀⠤⠤⠀⠈⠵⠊⠗⠺⠀⠠⠞⠨⠻⠀⠤⠤⠴⠄⠕⠊⠲")] // 줄표(dash)
          [TestCase("드디어 서울-호치민의 항로가 열렸다.", "⠊⠪⠊⠕⠎⠀⠠⠎⠯⠤⠚⠥⠰⠕⠑⠟⠺⠀⠚⠶⠐⠥⠫⠀⠳⠐⠱⠌⠊⠲")] // 붙임표(hypen)
          [TestCase("9월 15일~9월 25일", "⠼⠊⠏⠂⠀⠼⠁⠑⠕⠂⠈⠔⠼⠊⠏⠂⠀⠼⠃⠑⠕⠂")]
          public void ToJumjaTestWithPunctuationMarkBraille(string testStr, string expected)
          {
              Assert.AreEqual(expected, new Jumjaro.Jumjaro().ToJumja(testStr));
          }
      }
```

변경사항을 commit을 하려는데 인텔리제이에서 [[Git]인텔리제이 커밋 후 모든 라인 개행 변경점 해결(CRLF/LF 충돌)](https://mingggu.tistory.com/154)에서와 같은 다음 경고창이 나왔다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb6myX3%2FbtqO7jdw5D3%2Fe3nJSKH4i4tajABhY0P7AK%2Fimg.png)

IntelliJ와 같이 인텔리한 IDE에서는 core.autocrlf 설정이 되어있지 않은 경우
"You are about to commit CRLF line separators to the Git repository"라는 경고 메시지를 출력한다고 한다.  

[Fix and Commit] 버튼 클릭 시 core.autocrlf= input으로 설정한다. 나는 lf로 변환하는 것이 맞으므로 [Fix and Commit] 버튼을 눌렀다.
그러자 develop branch를 target으로 pull request를 하려는데 내가 추가한 줄뿐만 아니라 `/JumjaroTest/JumjaroTests.cs` 파일이 처음부터 모두 변경된 것으로 확인되었다. 

![]({{site.url}}{{site.baseurl}}/assets/images/jumjaro-contributing/aurocrlf-issue.png)
  
  

## crlf issue 해결하기



이와 같은 문제가 발생하는 이유는 위의 블로그 설명에 따르면 운영체제 별 개행문자 차이로 내가 수정하지 않은 부분까지 모두 변경되어버린 것으로 보였다.

![]({{site.url}}{{site.baseurl}}/assets/images/jumjaro-contributing/lf-to-crlf.png)

commit을 할 때 git diff 창쪽을 보면 기존 코드는 lf 인데 현재 내가 변경한 버전은 crlf이다. 그런데 macOS의 경우 기본이 lf 로 설정되므로 프로젝트와 일치해야 정상이다.
git config 설정 중 core.autocrlf은 mac의 경우 기본이 input이며, 이는 'commit할 때만 CRLF를 LF로 변환한다.'는 설정이다.
다음 명령어로 설정을 해주었다. 

> git config --global core.autocrlf input

설정이 제대로 됐는지 확인해봤으나 다음처럼 문제가 없었다.
  

> git config --list|grep autocrlf  
core.autocrlf=input
  

> git config --list|grep eol  
> core.eol=native



autocrlf 설정을 false로도 해보고 true로도 해보았다. 변경 후에는 다음 명령어로 캐시를 삭제하고 적용했다.
> git rm -rf --cached .
> git reset HEAD --hard

변경되는 줄 번호가 달라지긴 하나 모두 내가 추가하지 않은 줄이 수정된 것으로 나왔다.  

해결 방법을 찾을 수 없어 새로운 파일에 테스트 코드를 작성하기로 했다. 문장부호만을 위한 테스트 코드가 없기도 했고 주제별로 테스트 코드 파일을 분리하는 것이 유지보수에도 좋기 때문에 이렇게 하는 것이 더 낫다고 판단했다.   
   
ps. 개행문자 관련 문제는 왜 해결되지 않았는지 추후에 다시 확인해보는 것으로... 

## pull request

[문장부호(겹낫표, 홑낫표, 겹화살괄호, 홑화살괄호, 줄표, 붙임표, 물결표) 추가 #1](https://github.com/teamdotsix/jumjaro/pull/1)로 develop branch을 target으로 pull request를 open했다.
