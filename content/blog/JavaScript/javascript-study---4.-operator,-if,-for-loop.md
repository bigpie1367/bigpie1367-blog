---
title: JavaScript Study - 4. Operator, if, for loop
date: 2021-02-27
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=YBjufjBaxHo&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=4)

# Operator
## String concatenation
``` javascript
console.log('my' + ' cat');	
console.log('1' + 2);	// number가 string으로 취급
console.log(`string literals: 1 + 2 = ${1 + 2}`);
```

## Numberic operators
``` javascript
console.log(1 + 1);	// add
console.log(1 - 1);	// substract
console.log(1 / 1);	// divide
console.log(1 * 1);	// multiply
console.log(5 % 2);	// remainder
console.log(2 ** 3);	// exponentiation
```

## Increment and decrement operators
``` javascript
let counter = 2;

const preIncrement = ++counter;
// same with
// counter = counter + 1;
// preIncrement = counter;

console.log(`preIncrement: ${preIncrement}, counter: ${counter}`);
// preIncrement: 3, counter: 3

const postIncrement = counter++;
// same with
// postIncrement = counter;
// counter = counter + 1;

console.log(`postIncrement: ${postIncrement}, counter: ${counter}`);
// postIncrement: 3, counter: 4

const preDecrement = --counter;
console.log(`preDecrement: ${preDecrement}, counter: ${preDecrement}`);
// preDecrement: 3, counter: 3

const postDecrement = counter--;
console.log(`preDecrement: ${preDecrement}, counter: ${preDecrement}`);
// postDecrement: 3, counter: 2
```

## Assignment operators
``` javascript
let x = 3;
let y = 6;
x += y;	// x = x + y;
x -= y;	// x = x - y;
x *= y;	// x = x * y;
x /= y;	// x = x / y;
```

## Comparison operators
``` javascript
console.log(10 < 6);	// less than
console.log(10 <= 6);	// less than or equal
console.log(10 > 6);	// greater than
console.log(10 >= 6);	// greater than or equal
```

## Logical operators
### || (or)
`||` 연산자의 경우, 비교하는 값들 중 한 개라도 `true`일 경우 `true`. 모든 값들이 `false`일 경우 `false`를 return한다. 이 때 주의할 것은 `||` 연산을 진행하는 도중 `true`를 만날 시, 이후의 값들의 비교는 진행하지 않는다는 것이다.
    
**즉, 좋은 비교연산을 위해서는 단순한 값들을 우선적으로 비교하게끔 하는것이 좋다**
    
``` javascript
const value1 = false;
const value2 = 4 < 2;	// false
const value3 = true;

console.log(`or: ${value1 || value2 || check()}`);
// check
// or: true

console.log(`or: ${value1 || value3 || check()}`);
// or: true
// check function 실행 X

function check() {
	console.log('check');
	return true
}
```

### && (and)
`and` 연산자의 경우, 비교하는 값들 중 한 개라도 `false`일 경우 `false`. 모든 값들이 `true`일 경우 `true`를 return한다. `||` 연산과 마찬가지로 한 개라도 `false`일 경우 이후 값들의 비교를 진행하지 않으므로, 좋은 코드를 원한다면 단순한 값들을 우선적으로 비교하도록 작성하는 것이 좋다. 

``` javascript
const value1 = false;
const value2 = 4 < 2;	//false;

console.log(`and: ${value1 && value2 && check()}`);
// false
// check function 실행 X

function check() {
	console.log('check');
	return true;
}
```

또한 `&&` 연산은 Object의 `null` 체크를 위해서도 사용되는데, 이는 `null`이 `false`임을 응용한 것이다.

```
const myInfo = { name: 'rohsuin', age: '21' };

null && myInfo.name;	//null
myInfo && myInfo.name;	//rohsuin
// same with
// if (myInfo != null) {
//     myInfo.name;
// }
```

## ! (not)
``` javascript
const value1 = true;
console.log(!value1);	//false
```

## Equality
두 개의 피연산자가 같은지를 비교할 때 사용하는 연산자로, `==` 와 `===`가 존재한다. `==`는 loose equality라고 부르는데, 두 개의 피연산자의 Data Type이 다를지라도 내용물이 동일하면 `true`를 return한다. 이와는 반대로 `===` 연산자는 strict equality로, 피연산자의 Data Type까지 고려하여 결과를 return한다.

``` javascript
const stringFive = '5';
const numberFive = 5;

// == (loose equality, with type conversion)
console.log(stringFive == numberFive);	//true
console.log(stringFive != numberFive);	//false

// === (strict equality, no type conversion)
console.log(stringFive === numberFive);	//false
console.log(stringFive !== numberFive);	//true
```

Equality 연산자는 Object의 reference를 비교할 때도 사용할 수 있다.

``` javascript
const myInfo1 = { name: 'rohsuin' };
const myInfo2 = { name: 'rohsuin' };
const myInfo3 = myInfo1;

console.log(myInfo1 == myInfo2);	// false, 서로 다른 reference 저장
console.log(myInfo1 === myInfo2);	// false, 서로 다른 reference 저장
console.log(myInfo1 === myInfo3);	// true, myInfo1의 reference를 저장
```

## if (Conditional operators)
``` javascript
// if, else if, else

const name = 'rohsuin';
if (name === 'rohsuin') {
	console.log('Welcome, SuIn!');
} else if (name === 'bigpie1367') {
	console.log('Welcome, bigpie1367!');
} else {
	console.log('who r u?');
}
```

## ? (Ternary operator)
``` javascript
// condition ? value1 : value2;

const name = 'rohsuin';
console.log(name === 'rohsuin' ? 'yes' : 'no');	// yes
```

## Switch statement
연속적으로 `if`문을 사용해야 할 경우 `switch`문을 고려해볼 수 있으며, 이는 가독성의 향상으로 이어진다. `switch`문을 사용할 때 `break`를 각각의 경우마다 추가해야하는데, `break`문이 없을 경우 `switch`문을 종료하는 것이 아닌 계속해서 실행하게 된다. 이를 응용하면 동일한 결과값이 출력되는 경우, `break`문을 작성하지 않고 연달아 작성함으로써 코드를 간략화할 수 있다.

``` javascript
const browser = 'IE';
switch (browser) {
	case 'IE':
		console.log('trash');
		break;
	case 'Chrome':
	case 'Firefox':
		console.log('good');
		break;
	default:
		console.log('same all');
		break;
}
```

## Loops
### while loop
``` javascript
// while loop
// while 반복문의 경우, 조건이 참일 경우 코드를 실행한다.

let i = 3;
while (i > 0) {
	console.log(`while: ${i}`);
	i--;
}
console.log(loop done);

// while: 3
// while: 2
// while: 1
// loop done
```

### do-while loop
``` javascript
// do-while loop
// do-while 반복문의 경우, 우선 코드를 실행하고 조건문이 참인지 여부를 판단한다.

let i = 3;
do {
	console.log(`do while: ${}`);
	i--;
} while (i > 0);
console.log('loop done');

// do while: 3
// do while: 2
// do while: 1
// do while: 0
// loop done
```

### for loop
``` javascript
// for loop, for(begin; condition; step)
// begin은 반복문을 처음 실행할 때 한 번만 실행하며,
// 이후 condition이 참일 경우 block을 실행한 뒤 step을 실행한다.

let i;

for (i = 3; i > 0; i--) {
	console.log(`for: ${i}`);
}
console.log(`i: ${i}}`);
// for: 3
// for: 2
// for: 1
// i: 0


// 반복문과 함께 선언된 변수는 반복문이 종료된 뒤 Memory가 해제된다.
for (let j = 3; j > 0; j--) {
	console.log(`inline variable for: ${j}`);
}
console.log(`j: ${j});
// inline variable for: 3
// inline variable for: 2
// inline variable for: 1
// error : j is not defined
```

### break, continue
`break`와 `continue`는 각각 반복문을 제어하기 위해 존재한다. 반복문 Block 내의 코드를 실행하는 도중 `break`를 만날 시, 해당 반복문을 종료한다. `continue`는 실행중이던 Block만을 종료하며, 다시 반복문의 Condition을 판단하고 참일 경우 반복문을 다시 실행한다. 즉, 해당 조건하에 실행된 반복만을 종료한다. 

``` javascript
for (let i = 0; i < 5; i++) {
	if (i === 1) {
		console.log('2 is skipped');
		continue;
	} else if (i === 4) {
		console.log('loop done');
		break;
	}
	
	console.log(`i: ${i}`);
}

// i: 0
// 2 is skipped
// i: 2
// i: 3
// loop done
```