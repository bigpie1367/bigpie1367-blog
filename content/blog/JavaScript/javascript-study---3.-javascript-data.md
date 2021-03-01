---
title: JavaScript Study - 3. JavaScript Data
date: 2021-02-26
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=OCCpGh4ujb8&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=3)

 
# Variable
변수(Variable)란, 변경될 수 있는 값을 의미한다. `let` Keyword를 통해 변수를 선언할 수 있는데, 이는 ES6(ECMAScript 6)에서 추가된 Keyword이다.

``` javascript
//variable.js
'use strict';

let name = 'RohSuIn';
console.log(name);
name = 'SuInRoh';
consloe.log(name);
```

## Scope
### Block Scope
``` javascript
//Block Scope 사용예제
//variable.js

{
	let name = 'RohSuIn';
	console.log(name);
	name = 'SuInRoh';
	console.log(name);
}
console.log(name);	//Error
```
이를 실행해보면 Block 내에서 정의한 변수인 name을 Block 외부에서 접근할 수 없음을 확인할 수 있다

### Global Scope
``` javascript
//Global Scope 사용예제
//variable.js

let globalName = 'global SuIn';
{
	let name = 'RohSuIn';
	console.log(name);
	name = 'SuInRoh';
	console.log(name);
	console.log(globalName)
}
console.log(name);
console.log(globalName);
```
Blcok Scope와는 달리 Global Scope 영역에서 정의한 변수는 Block 내부와 외부에서 모두 접근할 수 있음을 확인할 수 있다.

### 참조
모든 변수를 Global 변수로 선언하는 것이 좋다고 생각할 수 있겠으나, Global Scope에서 선언된 변수는 프로그램이 실행하는 순간부터 종료하는 순간까지 항상 Memory 영역에 올라가있기에 최소한으로 사용해야만 한다. 반면 Block Scope에서 선언된 변수는 해당 Block이 종료됨과 동시에 Memory가 해제된다.


## var
`let` 키워드는 ES6 이후 추가된 키워드이다. ES6 이전에는 `var` 키워드를 사용하였는데, 여러 단점들로 인해 `let` 키워드가 생긴 이후론 사용되지 않는다.

### Demerits.1
일반적으론 변수를 선언한 뒤 사용하는 것이 일반적이다. 그러나 `var`을 통한 변수는 선언하기 전에 값을 할당할 수 있으며, 출력까지도 가능하다. 

``` javascript
//var 사용예제
//variable.js

console.log(age);	//undefined
age = 4;
console.log(age);
var age;
```

이는 **var hoisting**로 인한 결과이다. var hoisting이란 함수, 혹은 파일을 실행할 때 변수를 선언하는 코드를 최우선적으로 실행하는 것을 말한다. 즉, 이로인해 코드상으론 아직 선언되지 않은 변수라고 할지라도 사용이 가능한 것이다.

### Demertis.2
`var`은 Block Scope를 지니지 않는다. 이는 Block Scope를 무시함을 뜻한다.

``` javascript
//variable.js

{
	age = 4;
	var age;	//var hoisting
}
console.log(age);	// 4
```


# Constants
상수(Constants)는 선언한 뒤 값을 변경할 수 있는 변수(Variable)와는 달리, 한 번 할당한 뒤 값을 변경할 수 없다. 즉 상수는 불변하다(immutable). `const` Keyword를 통해 선언할 수 있다.

## Why use Constants?
### 1. Security
상수는 보안적으로 우수한 특징을 지니는데, 한 번 작성한 값을 외부의 요소(ex. Hacker)로 인해 강제적으로 변경될 수 없기 때문이다.

### 2. Thread Safety
여러개의 Thread가 동시에 접근하는 변수는 굉장한 위험성을 내포한다. 상수로 선언함으로써 이를 방지할 수 있다.

### 3. Reduce human mistakes
상수로 선언할 경우 불변하기에 사용자의 실수를 줄이기 위해서라도 값이 바뀌어야 할 목적이 아니라면 상수로 선언함이 일반적이다.

    
# Variable Types
## Primitive Type
더 이상 작은 단위로 나뉘어질 수 없는 아이템, Single item 들을 뜻한다. 그 예로 `number`, `string`, `boolean`, `null`, `undefiedn`, `symbol` 등이 있다.

### number
JavaScript에서는 숫자를 선언하기 위한 Keyword로 `number` 하나만 사용한다.

#### Special Number : `Infinity`
`infinity`는 `number`의 특별한 값 중 하나로, 일반적으로 입력받은 값이 타당한(valid) 지 판단하기 위해 사용된다.

``` javascript
const infinity = 1 / 0;	// Infinity
const negativeInfinity = -1 / 0;	// -Infinity
const nAn = 'not a number' / 2;	//NaN
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);
```

#### Special Number : `bigInt`
일반적인 Javascript `number`의 표현상의 한계를 넘었을때를 위함이다. 숫자 끝에 `n`을 추가해 `bigInt`로 선언할 수 있다.

``` javascript
const bigInt = 1234567890123456789012345678901234567890n;
console.log(`value: ${bigInt}`, type: ${typeof bigInt}`);
```
---

### string
JavaScript에서는 `string`으로 문자와 문자열을 모두 표현한다. 또한 일반 `string`과 다른 변수를 `+` 연산자를 이용하여 문자열을 합칠 수 있다.

``` javascript
const char = 'C';
const brendan = 'brendan';
const greeting = 'hello ' + brendan;
console.log(`value: ${greeting}, type: ${typeof greeting}`);
const helloBob = `hi ${brendan}!`;	// template literals (string)
console.log(`value: ${helloBob}, type: ${typeof helloBob}`);
console.log('value: ' + helloBob + ' type: ' 
 + typeof helloBob);	//same with above
```

`Template literals`라는 Javascript의 문법을 사용함으로써 편리하게 문자열과 변수를 출력할 수 있다. 변수의 값을 출력하고자 할 때는 `${variableName}`로 사용한다.

### boolean
참과 거짓을 표현하기 위한 자료형이며, `false`에는 `0, null, undefined, NaN, ''`이 해당된다. 다른 모든 값들은 `true`로 할당된다.

``` javascript
false: 0, null, undefined, NaN, ''
true: any other value
const canRead = true;
const test = 3 < 1;	//false
console.log(`value: ${canRead}, type: ${typeof canRead}`);
console.log(`value: ${test}, type: ${typeof test}`);
```

### null vs undefined
`null`과 `undefind`는 비슷해 보이지만 뚜렷한 차이가 존재한다. `null`이라고 값을 할당하는 경우는 직접적으로 빈 값이라고 알려주는 것이다. 이와는 반대로 `undefined`는 선언은 되었지만 아무런 값도 할당되지 않은 상태를 뜻한다.
``` javascript
let nothing = null;
console.log(`value: ${nothing}, type: ${typeof nothing}`);

let x;
console.log(`value: ${x}, type: ${typeof x}`);
```

### symbol
우선순위를 부여하기 위해 사용한다. `string`을 통해 부여할 때도 존재하는데, 동일한 `string`을 부여한다고 할지라도 다른 `symbol`로 인식된다. 동일한 `symbol`을 부여하고자 할 경우엔 `Symbol.for`을 사용하면 부여할 수 있다. `symbol`을 `console.log`를 통해 출력하고자 할 때에는 `symbol.dexcription`을 통해 출력해야만 한다.

``` javascript
const symbol1 = Symbol('id');
const symbol2 = Symbol('id');
console.log(symbol1 === symbol2);	//false

const gSymbol1 = Symbol.for('id');
const gSymbol2 = Symbol.for('id');
console.log(gSymbol1 === gSymbol2);	//true

console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);
```

	
## Object Type 
`Object Type`은 `Single Item`들을 묶어서 관리하기 위함으로, `Box Container`라고도 한다.

``` javascript
const myInfo = { name: 'rohsuin', age: 21 };
myInfo.name = 22;
```

## Function
JavaScript에서는 function도 Data Type의 일종이다. Javascript는 First-Class function을 지원하는 언어로, function도 다른 Data Type처럼 취급된다는 것을 의미한다. 이는 function이 변수에 할당이 가능하고, 또한 그렇기에 함수의 파라미터로 전달또한 가능하며 return 값으로 function 가능함을 뜻한다.
    
    
# Dynamic Typing
JavaScript는 Dynamically typed language로, 변수를 선언할 때 Data Type을 결정하지 않는다. . Data Type은 프로그램의 runtime 동안에 결정되며, 값이 변경됨에 따라 Data Type 또한 변경될 수 있다.

``` javascript
let text = 'hello';
console.log(`value: ${text}, type: ${typeof text}`);	
// value: hello, type: string

text = 1;
console.log(`value: ${text}, type: ${typeof text}`);	
// value: 1, type: number

text = '7' + 5;
console.log(`value: ${text}, type: ${typeof text}`);	
//value: 75, type: string

text = '8' / '2';
console.log(`value: ${text}, type: ${typeof text}`);	
//value: 4, type: number
```
    
다만 이로인해 특정 연산과정에서 오류가 발생하기도 한다.
    
``` javascript
let text = 'hello';
console.log(text.charAt(0));	//h
console.log(`value: ${text}, type: ${typeof text}`);	
// value: hello, type: string

text = 1;
console.log(`value: ${text}, type: ${typeof text}`);	
// value: 1, type: number

text = '7' + 5;
console.log(`value: ${text}, type: ${typeof text}`);	
//value: 75, type: string

text = '8' / '2';
console.log(`value: ${text}, type: ${typeof text}`);	
//value: 4, type: number

console.log(text,charAt(0));	
//TypeError
```