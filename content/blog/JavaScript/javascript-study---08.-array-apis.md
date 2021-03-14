---
title: JavaScript Study - 08. Array APIs
date: 2021-03-09
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=yOdAVDuHUKQ)

# Array
비슷한 종류의 데이터(Data)들을 묶어두기 위한 용도이다. 일반적으로 동일한 타입만을 담을 수 있는 다른 언어들과는 달리, 자바스크립트(JavaScript)는 Dynamic Typed Language로 다른 타입들도 함께 담을 수 있다. 다만 이러한 특징은 잘 사용되지 않는다. 배열은 인덱스(index)를 통해 접근할 수 있다.

## Array Declaration
``` javascript
const arr1 = new Array();	// object constructor
const arr2 = [1, 2];		// normal way

// Index position
const fruits = ['apple', 'banana'];
console.log(fruits);		// (2) ["apple", "banana"] 
console.log(fruits.length);	// 2
console.log(fruits[0])		// apple
console.log(frutis[1])		// banana
console.log(fruits[3])		// undefined

// for find last thing
console.log(fruits[fruits.length - 1]);	// banana
```

## Looping over an array
``` javascript
const frutis = ['apple', 'banana'];

// a. for
for (let i = 0; i < fruits.length; i++) {
	console.log(fruits[i]);	// "apple"
							// "banana"
}

// b. for of
for (let fruit of fruits) {
	console.log(fruit);	// "apple"
						// "banana"
}

// c. forEach - callback function (value, index, array[])
fruits.forEach(function (fruit, index, array) {
	console.log(fruit);	// "apple", "banana"
	console.log(fruit, index);	// "apple 0", "banana 1"
});

// advanced c. apply array function
fruits.forEach((fruit, index) => console.log(fruit, index));
```

## Addition, deletion, copy
### Addition
``` javascript
const fruits = ['apple', 'banana'];

// push : add an item to the end
fruits.push('grape', 'peach');
console.log(fruits);	// (4) ["apple", "banana", "grape", "peach"]


// unshift : add an item to the beginning
fruits.unshift('lemon');	// (5) ["lemon", "apple", "banana", "grape", "peach"]
```
    
### Deletion
``` javascript
const fruits = ['apple', 'banana', 'grape', 'peach', 'lemon'];

// pop : reomve an item from the end
fruits.pop();
console.log(fruits);	// (4) ["apple", "banana", "grape", "peach"]

fruits.pop();
console.log(fruits);	// (3) ["apple", "banana", "grape"]


// shift : remove an item from the beginning
fruits.shift();
console.log(fruits);	// (3) ["banana", "grape"]
fruits.shift();	
console.log(fruits);	// (2) ["grape"];
```
    
### Splice
``` javascript
const fruits = ['apple', 'banana', 'grape', 'peach', 'lemon'];
console.log(fruits);	// (5) ["apple", "banana", "grape", "peach", "lemon"]

// splice : remove an item || replace item by index position
// splice(start, deleteCount, ...items)
fruits.splice(1,1);
console.log(fruits);	// (4) ["apple", "grape", "peach", "lemon"];

fruits.splice(1, 1, 'watermelon'); 
console.log(fruits);	// (4) ["apple", "watermelon", "peach", "lemon"]

fruits.splice(1);
console.log(fruits);	// (1) ["apple"];
```

### Combine
``` javascript
const fruits = ['apple', 'banana];
const fruits2 = ['grape', 'peach'];

const newFruits = fruits.concat(fruite2);
console.log(newFruits);	// (4) ["apple", "banana", "grape", "peach"]
```

## Searching
``` javascript
const fruits = ['apple', 'banana', 'grape', 'peach'];

// indexOf : find an item and return its index position
console.log(fruits.indexOf('apple'));	// 0
console.log(fruits.indexOf('grape'));	// 2
console.log(fruits.indexOf('lemon'));	// -1

// includes : find an item and return true || false
console.log(fruits.includes('peach'));	// true
console.log(fruits.includes('lemon'));	// false

// lastIndexOf : return last index if it is duplicated
fruits.push('apple');

console.log(fruits.indexOf('apple'));		// 0
console.log(fruits.lastIndexOf('apple'));	// 4
```