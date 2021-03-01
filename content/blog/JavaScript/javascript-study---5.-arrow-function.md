---
title: JavaScript Study - 5. Arrow Function
date: 2021-03-01
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=e_lU39U-5bQ)

# Function?
프로그램을 구성하는 기본적인 요소로, 사용자의 입력값에 대해 내부 로직대로 연산한 결과를 출력해준다. 일반적으로 한가지의 작업 혹은 특정 값을 계산하기 위해 사용된다. function을 정의할 때 주의할 것은, 한 가지의 일만 하도록 정의해야 한다. 또한 이전 Data Type에 관한 글에서 설명하였듯이 JavaScript에서는 fucntion 또한 Data Type의 일종이며, Object이다. 

참조 : [JavaScript Study - 3. JavaScript Data](https://bigpie1367.netlify.app/JavaScript/javascript-study---3.-javascript-data/)

## Function Declaration
`functuion name(param1, param2) { body ... return; }`
일반적으로 함수의 이름은 명사가 아닌 동사형태로 지정한다. ex) postMD

``` javascript
function log(message) {
	console.log(message);
}

log('Hello!');
```

JavaScript는 Dynamic Typed Language로, 변수의 타입을 선언하지 않기 때문에 함수의 Interface만으로는 어떤 데이터 타입을 입력해야 하는지 불분명하기에 주의해야 한다.

## Function Parameters
함수의 파라미터로 들어오는 데이터 타입에 따라 전달되는 요소가 달라진다
- Primitive parameters : passed by value
- Object Parameters : passed by reference

``` javascript
// object parameters

function changeName(obj) {
	obj.name = 'coder';
}

const suin = { name: 'suin' };
changeName(suin);
console.log(name);
```

즉, Object는 reference로 전달되기에 내부요소가 정상적으로 변경된 걸 확인할 수 있다.

## Default Parameters
`Default Parameter`는 함수가 요구하는 파라미터를 사용자가 입력하지 않을 시를 위한 것으로, 파라미터의 default 값을 설정하는 것이다. 즉, 사용자가 해당 파라미터를 전달하지 않을 시 `Default Parameter`로 설정해 둔 값이 자동적으로 할당되는 것이다.

``` javascript
// example of default parameters

function showMesage(message, from = 'unknown') {
	console.log(`${message} by ${from}`);
}

showMessage('Hi!');	// Hi! by unknown
```

## Rest Parameter
`Rest Parameter`는 배열형태로 파라미터를 전달하기 위함이다. 사용하기 위해서는 `...`을 함수의 파라미터 앞에 추가하면 된다.

``` javascript
// example of rest parameter

function printAll(...args) {
	for (let i = 0; i < args.length; i++) {
		console.log(args[i]);
	}
}

printAll('dream', 'coding', 'suin');
```

## Local Scope
Local Scope의 기본적인 원칙은 아래와 같다.
**밖에서는 안을 볼 수 없지만, 안에서는 밖을 볼 수 있다**

``` javascript
let globalMessage = 'global';	// global variable

function printMessage() {
	let message = 'hello';	// local variable
	console.log(message);
	console.log(globalMessage);
}

printMessage();
// hello
// global

console.log(message);	// Error!
```

JavaScript에서는 함수 내부에 또다른 함수를 추가하는 경우가 있는데, 해당 경우도 마찬가지다.

``` javascript
let globalMessage = 'global';

finction printMessage() {
	let message = 'hello';
	console.log(message);
	console.log(globalMessage);
	
	function printAnother() {
		let childMessage = 'hello Another!';
		
		console.log(message);
	}
	
	console.log(childMessage);	// Error!
}
```

## Return a value
기본적으로 모든 함수는 return을 정의해야만 한다. 다만 위의 함수들의 경우 return이 존재하지 않는데, return이 없는 경우는 `return undefined`가 생략된 것이다.
``` javascript
function sum(a, b) {
	return a + b;
}

const result = sum(1, 2);
console.log(`sum: ${sum(1, 2)}`);	// sum: 3
```

### Early return, early exit
코드를 작성할 때, 함수의 목적에 부합하지 않는 경우엔 함수를 조기종료할 수 있도록 예외처리하는 것이 좋다.

``` javascript
// bad case
function upgradeUser(user) {
	if (user.point > 10) {
		// upgrade logic ...
	}
}

// good case
function upgradeUser(user) {
	if (user.point <= 10) {
		return;
	}
	// upgrade logic ...
}
```

## Function Expression
JavaScript는 First-class function이 지원되는 언어로, 이는 아래의 특징을 지닌다.
- 함수는 변수의 일종이다.
- 함수는 변수의 값으로 할당될 수 있다.
- 함수는 다른 함수의 파라미터로 전달될 수 있다.
- 함수는 다른 함수의 return 값으로 지정될 수 있다.

이를 토대로 function expression이 성립하는데, 그 사용 방법이 다양하다.

### Anonymous Function
함수를 선언함과 동시에 변수에 할당이 가능하다. 이는 변수에 함수를 담아 사용함으로써 코드를 줄이기 위함이다. 

``` javascript
// anonymous function

const print = function() {
	console.log('print');
};
print();	// print
const printAgain = print;
printAgain()	//print
```

### Named Function
`Anonymous Function`과는 달리, 함수를 선언하는 과정에서 함수의 이름을 별도로 정의할 수 있다. 이를 통해 Debugging 과정에서 StackTrace에 함수의 이름이 출력되어 Debug를 보다 용이하게 할 수 있다. 또는, 함수 내부에서 자기 자신을 다시 호출하기 위해서도(재귀적 용법) 사용한다.

``` javascript
const printNamed = function print() {
	console.log('print');
	print();
};

printNamed();	// loop
```

### Callback Function
특정 함수의 파라미터로 다른 함수를 전달할 수 있는데, 이를 통해 조건에 따라 파라미터의 함수가 실행되게끔 할 수 있다. 이를 `Callback Function`이라 한다.

``` javascript
// Callback Function

function randomQuiz(answer, printYes, printNo) {
	if (answer === 'love you') {
		printYes();
	} else {
		printNo();
	}
}

const printYes = function () {
	console.log('yes!');
};

const printNo = function print() {
	console.log('no!');
};

randomQuiz('wrong', printYes, printNo);		// no!
randomQuiz('love you', printYes, printNo);	// yes!
```

### Arrow Function
`Arrow Function`을 통해 만들어지는 function은 모두 `anonymous function`이다.

``` javascript
// basic function - simplePrint
const simplePrint = function() {
	console.log('simplePrint!');
};

// arrow function - simplePrint
const simplePrint = () => console.log('simplePrint!');

// basic function - add
const add = function(a, b) {
	return a + b;
}

// arrow function - add
const add = (a, b) => a + b;
```

### IIFE - Immediately Invoked Function Expression
``` javscript
// IIFE는 선언함과 동시에 함수를 실행하기 위함이다.

function hello() {
	console.log('IIFE');
}

hello();

// same with
(function hello() {
	console.log('IIFE');
})();
```