---
title: JavaScript Study - 3. JavaScript Data
date: 2021-02-26
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로, gi
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=OCCpGh4ujb8&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=3)

 
# Variable
변수(Variable)란, 변경될 수 있는 값을 의미한다. JavaScript에선 변수를 선언하기 위해 `let` Keyword를 사용하는데, 이는 ES6(ECMAScript 6)에서 추가된 Keyword이다. 
``` javascript
//variable.js
'use strict';

let name = 'RohSuIn';
console.log(name);
name = 'SuInRoh';
consloe.log(name);
```

## Scope
JavaScript에는 2가지의 Scope가 존재하는데, 이는 각각 Global Scope와 Blcok Scope에 해당한다. Block Scope 내부에 작성한 코드는 해당 Block 외부에서는 접근할 수 없다. 이와는 반대로 Global Scope에서 작성한 코드는 Block Scope 내부에서도 접근이 가능하다.

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

#### **Demerits**
모든 변수를 Global 변수로 선언하는 것이 좋다고 생각할 수 있겠으나, Global Scope에서 선언된 변수는 프로그램이 실행하는 순간부터 종료하는 순간까지 항상 Memory 영역에 올라가있기에 최소한으로 사용해야만 한다. 반면 Block Scope에서 선언된 변수는 해당 Block이 종료됨과 동시에 Memory가 해제된다.


## var
위에서 변수를 선언하기 위해 사용한 `let` 키워드는 ES6부터 추가된 키워드이다. ES6 이전에는 `var` 키워드를 사용하였는데, `var` 키워드가 지닌 여러 단점들로 인해 ES6 이후, 즉 `let` 키워드가 나온 뒤로부터는 사용되지 않는다.

### Demerits.1
대부분의 프로그래밍 언어들은 변수를 선언한 뒤 값을 할당하는게 일반적이다. 그러나 `var`은 일반적인 프로그래밍 언어와는 달리 선언하기 전에 값을 할당할 수 있으며, 심지어 할당하기 전에 출력까지도 가능하다. 
``` javascript
//var 사용예제
//variable.js

console.log(age);	//undefined
age = 4;
console.log(age);
var age;
```

#### **var hoisting**
이는 var hoisting으로 인한 결과이다. var hoisting이란 변수를 선언하는 코드를 파일 혹은 함수를 실행할 때 최우선으로 실행하는 것을 의미한다. 즉, 변수를 코드의 제일 밑단에 선언한다고 할지라도, 해당 파일의 동작 과정에서 제일 먼저 실행하기에 정상적으로 동작하는 것이다.

### Demertis.2
`var`은 Block Scope를 지니지 않는다. 즉 Block Scope를 무시한다.
``` javascript
//variable.js

{
	age = 4;
	var age;	//var hoisting
}
console.log(age);	//age 정상 출력
```


# Constants
상수(Constants)는 선언한 뒤 값을 변경할 수 있는 변수(Variable)와는 달리, 한 번 할당한 뒤 값을 변경할 수 없다. 즉 상수는 불변하다(immutable). 상수를 선언하기 위해서는 `const` Keyword를 사용한다.

## Why use Contants?
### 1. Security
상수는 보안적으로 우수한 특징을 지니는데, 한 번 작성한 값을 외부의 요소(ex. Hacker)로 인해 강제적으로 변경될 수 없기 때문이다.

### 2. Thread Safety
일반적으로 Application이 실행되면 한 가지 Process가 할당되고, 그 Process 내부에서는 다양한 Thread가 실행되어 Application의 실행속도를 향상시킨다. 이 때, 여러개의 Thread가 동시에 한 값에 접근해 변경할 수 있는데 이는 굉장한 위험성을 내포한다.

### 3. Reduce human mistakes
해당 값이 변경되어야 할 특정한 목적이 있는 것이 아니라면 상수로 선언하는 것이 더 선호된다. 이로 인해 이후에 발생할 수 있는 실수를 방지할 수 있기 때문이다.

    
# Variable Types
JavaScript 또한 일반적인 언어와 같이 Primitive 타입과 Object 타입의 데이터가 존재한다.

## Primitive Type
더 이상 작은 단위로 나뉘어질 수 없는 아이템, Single item 들을 뜻한다. 그 예로 `number`, `string`, `boolean`, `null`, `undefiedn`, `symbol` 등이 있다.

### number
C나 Java같은 경우엔 숫자를 선언하기 위한 다양한 Data Type이 존재한다. C에서는 short, int, long과 같이 정수(integer)를 선언하기 위한 Data Type과 float, double과 같은 실수(float)를 선언하기 위한 Data Type이 따로 존재한다. 이와는 달리 JavaScript에서는 숫자를 선언하기 위한 Keyword로 `number` 하나만 사용한다.

---
#### Special Number : `Infinity`
`number`에서도 특별한 값이 몇 가지 존재하는데 `infinity`가 그 예이다. 이러한 특별한 세 값은 주로 입력받은 값이 타당한(valid) 값인지 아닌지 판단할 때 사용된다.
``` javascript
const infinity = 1 / 0;	// Infinity
const negativeInfinity = -1 / 0;	// -Infinity
const nAn = 'not a number' / 2;	//NaN
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);
```
---
#### Special Number : `bigInt`
JavaScript에서의 `number`은 -9.0071993e+15 ~ +9.0071993e+15(-2^53 ~ 2^53)의 값을 표현 가능하다. 그러나 이 범위를 넘어갈 경우를 대비한 `bigInt`라는 새로운 Type이 생겼다. 사용하기 위해서는 숫자 끝에 `n`을 추가하면 된다.
``` javascript
const bigInt = 1234567890123456789012345678901234567890n;
console.log(`value: ${bigInt}`, type: ${typeof bigInt}`);
```
---

### string
다른 언어에서는 1개의 문자(character)를 위한 Data Type이 별도로 존재하지만, JavaScript에서는 `string`으로 문자와 문자열을 모두 표현한다. 또한 일반 `string`과 다른 변수를 `+` 연산자를 이용하여 문자열을 합칠 수 있다.
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

#### **template literals**
문자열 내에 다른 변수의 값을 함께 출력하고자 할 때 사용한다. 변수의 값을 출력하고자 할 때는 `${variableName}`로 사용한다.

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
이후 설명할 `map` 자료형, 혹은 동시다발적으로 일어나는 코드에서 우선순위를 주고싶을 때 `symbol`을 통해 고유한 식별자를 부여할 수 있다. 간혹 `symbol`을 `string`을 통해 부여할 때도 존재하는데, 동일한 `string`을 부여한다고 할지라도 다른 `symbol`로 인식된다. 동일한 `symbol`을 부여하고자 할 경우엔 `Symbol.for`을 사용하면 부여할 수 있다. 뿐만아니라 `symbol`을 `console.log`를 통해 출력하고자 할 때에는 `symbol.dexcription`을 통해 출력해야만 한다.
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
Single Item들을 묶어서 한 박스로 관리할 수 있게 해주는 Object로, Box Container라고도 한다. `object` 또한 상수로 선언할 수 있는데, `object`를 상수로 선언할 경우 `object` 자체는 변경할 수 없지만, `object`를 구성하는 요소는 변경할 수 있다.
``` javascript
const myInfo = { name: 'rohsuin', age: 21 };
myInfo.name = 22;
```
    
  
## Function
JavaScript에서는 function도 Data Type의 일종이다. 통상 특정 언어에서 First-Class function이 지원된다고 함은 해당 프로그래밍 언어에서는 function도 다른 Data Type처럼 취급된다는 것을 의미한다. 이는 function이 변수에 할당이 가능하고, 또한 그렇기에 함수의 인자(Parameter)로 전달또한 가능하며 함수의 return type으로 function 또한 return이 가능함을 의미한다.
    
    
# Dynamic Typing
JavaScript는 Dynamically typed language라고 불린다. 이는 C나 Java와는 달리 변수를 선언할 때 Data Type을 미리 결정하지 않고, 프로그램이 동작하는 runtime 때 Data Type이 결정된다는 것을 의미한다. C나 Java같은 언어는 Static Typing 언어로, Dynamic Typing 언어의 반대이다.
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
다만 이처럼 runtime에서 Data Type이 변하는 특징으로 인해 연산과정에서 Error가 발생하는 위험이 존재하기도 한다.
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