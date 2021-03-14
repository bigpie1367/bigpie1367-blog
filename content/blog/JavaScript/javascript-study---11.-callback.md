---
title: JavaScript Study - 11. Callback
date: 2021-03-14
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=s1vpVCrT8f4&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=11)

# Sync VS Async
JavaScript는 동기적(Synchronous)인 언어로, 호이스팅(hoisting)을 기반으로 순서에 따라 코드 블럭을 실행하는 언어이다.     

``` javascript
// Synchronous
console.log('1');	// 1

// Asynchronous
setTimeout(() => console.log('2'), 1000);

// Synchronous
console.log('3');	// 3
```   

`setTimeout()`은 대표적인 비동기적(Asynchronous)한 함수(function)로, 해당 코드를 실행해보면 순차적으로 1, 3, 2가 출력됨을 확인할 수 있다. JavaScript에서는 비동기적인 함수를 실행할 시 응답을 기다리지 않고 다음 코드를 실행한다.

# Callback
## Synchronous Callback
``` javascript
// Synchronous Callback
function printImmediately(print) {
	print();
}

console.log('1');	// 1
setTimeout(() => console.log('2'), 1000);
console.log('3');	// 3

printImmediately(() => console.log('hello'));

// 실행결과 : 1, 3, hello, 2
```

## Asynchronous Callback
``` javascript
function printWithDelay(print, timeout) {
	setTimeout(print, timeout);
}

console.log('1');	// 1
setTimeout(() => console.log('2'), 1000);
console.log('3');	// 3

printWithDelay(() =<> console.log('async callback'), 2000);

// 실행결과 : 1, 3, hello, 2, async callback
```

## Callback Hell
콜백 지옥(Callback Hell)이란 Callback 함수의 반복된 사용으로 인해 발생하는 문제이다. Callback 함수의 결과로 또다른 Callback 함수를 호출하며 콜백 체인(Callback Chain)을 형성하는 것이다. 이는 코드의 가독성을 낮추며, 에러가 발생할 시 디버깅조차 어렵게 만들며 유지보수를 힘들게 한다. 따라서 Callback 함수를 사용할 시 주의해야한다. 