---
title: JavaScript Study - 7. Object
date: 2021-03-07
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=1Lbr29tzAA8)

# Object
오브젝트(Object)는 변수 하나당 한 값을 담을 수 있는 기본형 타입(Primitive Type)과는 달리 복수의 값을 담기 위한 데이터 타입(Data Type)이다. 

``` javascript
// primitive type
const name = 'suin';
const age = 22;

print(name, age);

function printPrimitive(name, age) {
	console.log(name);
	console.log(age);
}

// object type
// object = { key : value }
const suin = { name: 'suin', age: 22 };

function printObject(person) {
	console.log(person.name);
	console.log(person.age);
}
```

## Object Declaration
``` javascript
// object declaration

const obj1 = {};	// 'object literal' syntax
const obj2 = new Object();	// 'object constructor' syntax
```
    
JavaScript는 Dynamically Typed Language로, runtime중에 데이터 타입이 결정된다. 이로인해 아래와 같은 일이 가능한데, 일반적으론 사용되지 않는다.

``` javascript
const suin = { name: 'suin', age: 22 };
console.log(suin.name);	// suin
console.log(suin.age);	// 22

// can add properties later
suin.hasJob = true;
console.log(suin.hasJob);	// true

// can delete properties later
delete suin.hasJob;
console.log(suin.hasJob)	// undefined
```

## Computed properties
일반적으로 오브젝트 내의 데이터에 접근하기 위해서는 `.`을 사용한다. 혹은 Computed properties로 접근또한 가능한데, 요구되는 정확한 Key를 모를 때 사용한다.

``` javascript
const suin = { name: 'suin', age: 22 };

// access by `.`
console.log(suin.name);

// access by computed properties
console.log(suin['name'])

// used example
function printValue(obj, key) {
	console.log(obj.key);	// undefined
	console.log(obj[key]);	// suin
}

printValue(suin, 'name');
```

## Property value shorthand
일반적으로 오브젝트를 반복적으로 생성하고자 할 때 function을 이용하는데, 이 때 Key 값과 Value 값이 동일하다면 이를 생략할 수 있다. 이를 Property value shorthand라 한다.

``` javascript
const person1 = { name: 'bob', age: 2 };
const person2 = { name: 'steve', age: 3 };
const person3 = { name: 'dave', age: 4 };
const person4 = makePerson('name', 30);

function makePerson(name, age) {
	return {
		// deafult
		name: name,
		age: age
	
		// Property value shorthand
		name,
		age
	};
}
```

## Constructor Function
위에서 소개한 것을 개선한 것으로, function을 Class와 유사하게끔 만들 수 있다. 이를 Constructor Function이라 한다.

``` javascript
function Person(name, age) {
	// this = {};
	this.name = name;
	this.age = age;
	// return this;
}
```

## in operator 
`in` 연산자(operator)는 오브젝트 안에 해당 값이 존재하는지 체크하기 위한 연산자이다.

``` javascript
const suin = { name: 'suin', age: 22 };
console.log('name' in suin);	// true
console.log('hasJob' in suin);	// false
```

## for..in vs for..of
``` javascript
// for (key in obj)
const suin = { name: 'suin', age: 22 };

for (key in suin) {
	console.log(key);	// name
						// age
}

// for (value of iterable)
const array = [1, 2, 4, 5];

for (value of array) {
	console.log(value);		// 1
							// 2
							// 4
							// 5
}
```

## Fun cloning
특정 Object가 다른 Object를 참조할 경우, 값이 복사되는 것이 아닌 동일한 값을 공유하게 된다. 이를 방지하기 위해 Object Class의 `assign` method를 활용한다.

``` javascript
const user = { name: 'suin', age: 22 };
const user2 = user;

user2.name = 'coder';
console.log(user);	// {name: "cojde", age: "20"};

// Object.assign(dest, [obj1, obj2, obj3...])
// single source
const user3 = {};
Object.assign(user3, user);

const user4 = Object.assign({}, user);

// multiple source - 뒤의 properties가 우선됨
const fruit1 = { color: 'red' };
const fruit2 = { color: 'blue', size: 'big' };
const mixed = Object.assign({}, fruit1, fruit2);

console.log(mixed.color);	// blue
console.log(mixed.size);	// big
```




