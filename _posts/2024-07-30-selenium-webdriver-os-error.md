---
title:      Selenium webdriver OSError 해결하기
summary:    "Selenium webdriver OSError: [Errno 8] Exec format error"
categories: 
  - Error
tags:
  - Selenium_Webdriver
  - Webdriver_OS_Error
last_modified_at: 2024-07-30T23:06:00-05:00
---
<br />

# issue
**selenium webdriver**를 실행하니 *OSError: [Errno 8] Exec format error*가 발생했다.
```
OSError: [Errno 8] Exec format error: '/Users/juyoung/.wdm/drivers/chromedriver/mac64/127.0.6533.72/chromedriver-mac-arm64/THIRD_PARTY_NOTICES.chromedriver'
```
<br />

실행한 코드는 다음과 같다.
```
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager


driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
driver.get('https://www.starbucks.co.kr/store/store_map.do?disp=locale')
```
참고로 실행한 맥북 macOS 버전은 Ventura 13.5.1 이다.
<br />
<br />
<br />
# solution
https://stackoverflow.com/a/78796691/14461707 에 따라 해결했다.
<br />

1. webdriver-manager를 4.0.2로 package 업데이트한다.
```
pip freeze\
selenium==4.23.0\
webdriver-manager==4.0.2
```
<br />

2. `/Users/****(사용자 이름)/` 경로에 있는 `.wdm` directory를 삭제한다.
