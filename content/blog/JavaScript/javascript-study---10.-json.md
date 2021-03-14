---
title: JavaScript Study - 10. JSON
date: 2021-03-11
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=FN_D4Ihs3LE&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=10)

# JSON
JSON은 JavaScript Object Notatin의 약자로, HTTP(Hypertext Transfer Protocol) 통신간에 XML을 대체하는 데이터 포맷이다. 오브젝트(Object)와 마찬가지로 `{Key: Value}`로 이루어져 있다. 일반적으로 오브젝트의 정보를 직렬화(Serialize)하여 JSON 형태로 저장한다.

## stringify
`stringify` method는 JavaScript 오브젝트를 JSON 파일 형식으로 변환하기 위해 사용한다.
     
``` javascript
// convert a javascript value to json string

let json = JSON.stringify(true);
console.log(json);	// true

json = JSON.stringify(['apple', 'banana']);
console.log(json);	// ["apple", "banana"]

const rabbit = {
	name: 'tori',
	color: 'white',
	size: null,
	birthDate: new Date(),
	jump: () => {
		console.log(`${name} can jump!`);
	},
};

// method doesn't convert to json
json = JSON.stringify(rabbit);
console.log(json);	
// {"name":"tori","color":"white","size":null, "birthDate":"2021-03-11T22:26:31.943Z"}
					
json = JSON.stringify(rabbit, ["name"]);
console.log(json);	// {"name":"tori"}

json = JSON.stringify(rabbit, (key, vaule) => {
	return key === 'name' ? 'suin' : value;
})
console.log(json);	
// {"name":"suin","color":"white","size":null, "birthDate":"2021-03-11T22:26:31.943Z"}
```

## parse
`parse` method는 JSON 파일을 오브젝트로 변환하기 위해 사용된다. 이 때, JSON 파일은 모두 String으로 이루어져 있으므로 변환된 오브젝트 역시 String 형태이다.
    
``` javascript
// convert json string to javascript object

const rabbit = {
	name: 'tori',
	color: 'white',
	size: null,
	birthDate: new Date(),
	jump: () => {
		console.log(`${name} can jump!`);
	},
};

json = JSON.stringify(rabbit);

const obj = JSON.parse(json);
console.log(obj);	// {"name":"tori","color":"white","size":null
					// "birthDate":"2021-03-11T22:26:31.943Z"}
					
// method doesn't recover
rabbit.jump();	// tori can jump!
obj.jump();		// obj.jump is not a function

// every elements are all string
console.log(rabbit.birthData.getDate());	// 11
console.log(obj.birthDate.getDate());		// obj.birthDate.getDate is not a function
console.log(obj.birthDate);	// {"birthDate":"2021-03-11T22:26:31.943Z"}
```