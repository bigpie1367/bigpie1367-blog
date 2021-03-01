---
title: JavaScript Study - 2. JavaScript 기초
date: 2021-02-23
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
//main.js
console.log('Hello World!');	//console 창에 'Hello World!'를 출력
```

# async VS defer
HTML에서 JavaScript를 포함하기 위해서는 다양한 방법이 존재한다.

## 1. `<head>` 내에 `<script>`를 포함
``` html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Document</title>
		<script src="main.js"></script>
	</head>
	<body>
		<div></div>
	</body>
</html>
```

### How it works
사용자가 HTML 파일을 다운받았을 때 이를 실행하기 위해 HTML 한 줄씩 읽어들이며 실행, 즉 파싱(Parsing)을 진행한다. 파싱 과정에서 `<script>`태그를 발견할 시 파싱을 중단한 채 `main.js` 파일을 서버로부터 다운받고 실행한 뒤 다시 파싱을 진행한다.    

### Demerits
	JavaScript 파일의 사이즈, 혹은 인터넷 속도에 영향을 받는다.
사용자가 HTML 파일을 다운로드 받은 뒤 js 파일을 추가적으로 다운받게 된다. 따라서 js 파일의 사이즈가 크거나 인터넷 속도가 느릴 시, Page를 완성하는 데 오랜 시간이 소요된다.
  
    
## 2. `<body>` 의 끝에 `<script>`를 포함
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

### How it works
`<body>`의 끝에 `<script>`를 정의함으로써 해당 HTML 파일을 모두 파싱, 즉 Page가 모두 준비 된 뒤 서버로부터 다운로드를 진행한다.
    
### Demerits    
	해당 Web의 JavaScript 의존도에 영향을 받는다.
    
이전 방법에 비해 사용자가 기본적인 HTML Contents를 빨리 볼 수 있지만, js 파일에 의존하는 내용들의 경우에는 서버로부터 다운로드 받고 실행하는 시간을 기다려야만 한다.

    
## 3. `<head>` + `async`
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

### How it works
`<script>` Tag에 `async` 속성을 추가할 경우, HTML 파싱을 진행하는 도중 `<script>`를 만날 시 파싱을 중단하지 않고 병렬로 서버로부터 다운로드를 진행한다. 이 때, js 파일이 다운로드가 완료될 시 파싱을 중단하고 js 파일을 실행한다. 이후 다시 파싱을 진행한다.

### Demerits
	JavaScript 파일을 실행하는 데 위험성을 내포한다.
    
js 파일이 HTML이 모두 파싱되기 전에 실행된다. 만약 js 파일을 통해 특정 HTML에 접근하고자 할 때, 해당 HTML이 아직 준비되지 않았을 때가 있을 수 있다. 또한 js 파일의 실행을 위해 HTML 파싱을 중단하므로 사용자가 Page에 접근하는 데 시간이 소요된다.  

## 4. `<head>` + `defer`
``` html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Document</title>
		<script defer src="main.js"></script>
	</head>
	<body>
		<div></div>
	</body>
</html>
```

### How it works
이전 `async`와 마찬가지로, HTML 파일의 파싱을 진행하는 도중 `defer` Tag를 만날 시 파싱을 중단하지 않는다. 다운로드가 완료될 시 파싱을 중단하는 `async`와는 달리 파싱을 모두 진행한 뒤 이후 파일을 실행한다.

# Option. `'use strict'`
``` javascript
//main.js
'use strict';

consloe.log('Hello World!');
```

Vanlia JS는 다른 일반적인 언어들에 비해 유연한(flexble)한 특징을 지닌다. 선언되지 않은 변수에 값을 할당, 기존에 존재하는 Prototype을 변경할 수 있는 것이 그 예이다. 이러한 것들의 사용을 방지하고자 추가하는 것이 `'use strict';`이다.

## Merits
`strict` mode를 사용할 경우 Web Browser의 JavaScript 엔진이 기존대비 더 효율적 & 빠르게 js 파일을 이해할 수 있어 성능개선을 기대할 수 있다. 