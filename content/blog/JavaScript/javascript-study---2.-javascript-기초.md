---
title: JavaScript Study - 2. JavaScript 기초
date: 2021-02-22
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로, 
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=tJieVCgGzhs&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=2)

# Hello World!
``` javascript
#main.js
console.log('Hello World!');	//console 창에 'Hello World!'를 출력
```
`console.log()`는 Console API에서 제공하는 가장 기초적인 Method이며, 일반적으로 변수이 값을 기록할 때 사용함.

참고 문헌 : [Console API - Web API](https://developer.mozilla.org/ko/docs/Web/API/Console_API)

# async VS defer
HTML에서 JavaScript를 포함하기 위해서는 다양한 방법이 존재한다.

1. `<head>` 내에 `<script>`를 포함
``` html
<!DOCTYPE html>
<html lang="en">
    <head>
		<meta charset="UTF-8" />
		<title>Document</title>
		<script src="main.js"></script>
	</head>
	<body></body>
</html>
```
사용자가 HTML 파일을 다운받았을 때, HTML을 한 줄씩 파싱(Parsing)하게 된다. 파싱 과정에서 `<script>`태그를 발견할 시 `main.js` 파일을 서버로부터 다운받고 실행한 뒤 다시 파싱을 진행한다.
  ### Demerits
  **js 파일의 사이즈 혹은 인터넷 속도에 영향을 받는다**    
  사용자가 HTML 파일을 다운로드 받은 뒤 JavaScript 추가적으로 다운받게 된다. 따라서 JavaScript 파일의 사이즈가 크거나 인터넷 속도가 느릴 시, Page를 완성하는 데 오랜 시간이 소요된다.
  
2. `<body>` 의 끝에 `<script>`를 포함
``` html
<!DOCTYPE html>
<html lang="en">
    <head>
		<meta charset="UTF-8" />
		<title>Document</title>
	</head>
	<body>
		<div></div>
		<script src="main.js"></script>
	</body>
</html>
```
`<body>`의 끝에 `<script>`를 정의함으로써 다른 모든 HTML을 파싱, 즉 Page가 모두 준비 된 뒤 서버로부터 다운로드를 진행한다.

   ### Demerits
   **해당 Web의 JavaScript 의존도에 따라 속도가 달라진다.**    
   이전 방법에 비해 사용자가 기본적인 HTML Contents를 빨리 볼 수 있지만, JavaScript 파일에 의존하는 내용들의 경우에는 서버로부터 다운로드 받고 실행하는 시간을 기다려야만 한다.

3. head + async
``` html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Document</title>
		<script async src="main.js"></script>
	</head>
	<body>
		<div></div>
	</body>
</html>
```
`<script>` Tag에 `async` 속성을 정의할 경우, HTML 파싱을 진헹하는 도중 `<script>`를 만날 시 파싱을 중단하지 않고 병렬로 서버로부터 다운로드를 진행한다. 이 때, 서버로부터 다운로드가 완료될 시 파싱을 중단하고 JavaScript 파일을 실행한다.
