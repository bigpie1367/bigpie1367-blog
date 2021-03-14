---
title: JavaScript Study - 09. Array functions
date: 2021-03-10
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=3CUjtKJ7PJg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=10)

# Array Functions
## join
``` javascript
// Adds all the elements of an array
// separated by the specified separator string

const fruits = ['apple', 'banana', 'grape'];

const result = fruits.join();
console.log(result);	// apple,banana,grape

const result2 = fruits.join('|');	
console.log(result2);	// apple|banana|grape
```

## split
``` javascript
// split a string into substrings using the specified separator

const fruits = 'apple, banana, grape, peach';

const result = fruits.split(',');
console.log(result);	// (4) ["apple", "banana", "grape", "peach"]

const result2 = fruits.split(',', 2);
console.log(result2);	// (2) ["apple", "banana"]
```

## reverse
``` javascript
// reverse whole array

const array = [1, 2, 3, 4, 5];

const result = array.reverse();
console.log(result);	// (5) [5, 4, 3, 2, 1]
console.log(array);		// (5) [5, 4, 3, 2, 1]
```

## slice
``` javascript
// returns a section of an array

const array = [1, 2, 3, 4, 5];

const result = array.slice(0, 2);
console.log(result);	// (2) [1, 2]

const result2 = array.slice(2, 5);
console.log(result2);	// (3) [3, 4, 5]

console.log(array);		// (5) [1, 2, 3, 4, 5]
```
      
# Object Array
``` javascript
class Student {
	constructor(name, age, enrolled, score) {
		this.name = name;
		this.age = age;
		this.enrolled = enrolled;
		this.score = score;
	}
}

const students = [
	new Student('A', 29, true, 45),
	new Student('B', 28, false, 80),
	new Student('C', 30, true, 90),
	new Student('D', 40, false, 66),
	new Student('E', 18, true, 88),
];
```

## find 
``` javascript
// returns the value of the first element in the array
// where 'predicate' is true, and undefined otherwise

// predicate : callback func

const result = students.find((student) => return student.score === 90);

console.log(result);	// Student {name: "C", age: 30, 
						//			enrolled: true, scpre: 90}
```

## filter
``` javascript
// returns new array with the elements that pass the callback func

const result = students.filter((student) => student.enrolled);
console.log(result);	
// (3) [Student, Student, Student]
// 0 : Student {name: "A", age: 29, enrolled: true, score: 45}
// 1 : Student {name: "C", age: 30, enrolled: true, score: 90}
// 2 : Student {name: "E", age: 18, enrolled: true, score: 88}
```

## map
``` javascript
// return a new array with each element 
// being the result of the callback function.

const result = students.map((student) => student.score);
console.log(result);	// (5) [45, 80, 90, 66, 88]
```

## some
``` javascript
// determines whether the specified callback function returns true

const result = students.some((student) => student.score < 50);
console.log(result);	// true
```

## every
``` javascript
// determines whether all the elements are passed the callback func

const result = students.every((student) => student.score < 50);
console.log(result);	// false
```

## reduce
``` javascript
// return value of the callback func is the accumulated result
// and is provided as an argument in the next call

const result = students.reduce((prev, curr) => {
	console.log(prev);	// 0 (initial param)
	console.log(curr);	// Student {name: "A", age: 29, 
						//			enrolled: true, score: 45}

	return prev + curr.score;
}, 0);

console.log(result);	// 369

const result2 = students.reduceRight((prev, curr) => {
	console.log(prev);	// 0
	console.log(curr);  // Student {name: "E", age: 18, 
						//			enrolled: true, score: 88}
	
	return prev + curr.score;
}, 0);
```

## sort
``` javascript
// sorts an array

const result = students.map(student => student.score)
.sort(a, b) => a - b)
.join();

console.log(result);	// 45, 66, 80, 88, 90 
