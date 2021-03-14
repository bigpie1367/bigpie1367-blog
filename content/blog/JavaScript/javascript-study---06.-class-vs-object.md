---
title: JavaScript Study - 06. class vs object
date: 2021-03-03
category: JavaScript
thumbnail: { thumbnailSrc }
draft: false
---

# Warning
해당 글은 **JavaScript**를 개인적으로 공부하며 요약해둔 내용으로,
작성자의 이해를 바탕으로 작성되었기에 **틀린 내용**이 있을 수 있습니다.    

참고 문헌 : [Youtube 드림코딩](https://www.youtube.com/watch?v=_DLhUBWsRtw&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=6)

# Class
`class`란 연관성 있는 데이터(Data)들을 묶어두는 일종의 컨테이너(Container)로, 속성(field)과 행동(method)로 구성되어 있다. 다만 `class`는 실제 값이 들어가는 것이 아닌, 값이 들어가기 위한 공간을 제공해주는 역할로 청사진과 같은 개념이다.

``` javascript
class person {
	// 속성 (field)
	name;	
	age;
	
	// 행동 (method)
	speak();
}
```

# Object
`class`를 이용해 실제로 데이터를 넣어 만드는 것이 `object`이다. 이를 `class`를 이용해 새로운 인스턴스(instance)를 생성하면 `object`가 된다고 표현한다. 

## Class declarations
``` javascript
class Person {
	// constructor
	constructor(name, age) {
		// fields
		this.name = name;
		this.age = age;
	}
	
	// methods
	speak() {
		console.log(`${this.name}: hello!`);
	}
}

const suin = new Person('suin', 22);
console.log(suin.name)	// suin
console.log(suin.age)	// 22
suin.speak();			// suin: hello!
```

## Getter and Setter
``` javascript
class User {
	constructor(firstName, lastName, age) {
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}
	
	// for return value
	get age() {
		return this.age;	// error
	}
	
	// for set value
	set age(value) {
		this.age = value;	// error
	}
}

const user1 = new User('Steve', 'Job', -1);
console.log(user1.age);
```
    
getter를 선언하게 되면 변수들을 읽어들일 때 자동적으로 getter method를 실행한다. setter의 경우도 마찬가지로, 변수에 값을 할당할 때 자동적으로 setter method를 실행한다. 즉, constructor method 내의 `this.age = age;` 코드를 실행할 때, 값을 할당하기 위해 `set age(value)` method를 호출하게 된다. 
        
이로인해 `set age(value)` method 내의 `this.age = value;`를 통해 값을 할당하고자 하면, 다시 `set age(value)` method를 호출하게 되고 무한루프에 빠지게된다. 이를 방지하기 위함이 아래와 같다.

``` javascript
// for avoid loop

class User {
	constructor(firstName, lastName, age) {
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}
	
	// for return value
	get age() {
		return this._age;	// for avoid loop
	}
	
	// for set value
	set age(value) {
		this._age = value;	// for avoid loop
	}
}

const user1 = new User('Steve', 'Job', -1);
console.log(user1.age);
```

getter와 setter 내의 변수의 이름을 다르게 하여 무한루프에 빠지는 것을 방지한다. 일반적으로 변수앞에 `_`를 추가한다.

## public, private Fields
``` javascript
class Experiment {
	publicField = 2;
	#privateField = 0;
}

const experiment = new Experiment();
console.log(experiment.publicField);	// 2
console.log(experiment.privateField);	// undefined
```

## static proeprties
`static` 프로퍼티(properties)는 Object와 상관없이 Class 자체의 값을 선언하기 위함이다. 즉, `static`으로 선언된 데이터(Data)나 메소드(Method)를 사용하려면 Object가 아닌 Class를 통해 호출해야 한다.


``` javascript
class Article {
	static publisher = 'Dev.LogIn`;
	
	constructor(articleNumber) {
		this.article.Number = articleNumber;
	}
	
	static printPublisher() {
		console.log(Article.publisher);
	}
}

const article1 = new Article(1);
const article2 = new Article(2);
console.log(article1.publisher);	// undefined
console.log(Article.publisher);		// Dev.LogIn
Article.printPublisher();			// Dev.Login
```

## Inheritance
상속(Inheritance)이란 여러 Class들에서 반복되는 공통분모를 추출할 뒤, 이를 하나의 Class로 만드는 것이다. 이를 통해 코드의 재사용성을 높일 수 있고, 수정또한 간편하게 할 수 있다.

``` javascript
class Shape {
	constructor(width, height, color) {
		this.width = width;
		this.height = height;
		this.color = color;
	}
	
	draw() {
		console.log(`drawing ${this.color} color of`);
	}
	
	get Area() {
		return thus.width * this.height;
	}

// 상속(inheritance)
class Rectangle extends Shape {}
class Triangle extends Shape {}

// constructor와 method를 상속받음
const rectangle = new Rectangle(20, 20, 'blue');
rectangle.draw();	//drawing blue color of
console.log(rectangle.getArea());	// 400
const triangle = new Triangle(20, 20, 'red');
triangle.draw();	//drawing red color of
console.log(triangle.getArea());	// 400 ?
```

## Polymorphism
상속을 통한 메소드를 재정의 할 필요가 있을 시 수정할 수 있는데, 이를 오버라이딩(Overriding)이라 한다. 이 때, 부모 Class의 메소드를 다시 사용하고자 할 경우 `super` 키워드를 통해 사용가능하다. JavaScript의 이러한 특징을 다형성(Polymorphism)을 지닌다고 표현한다.

``` javascript
class Shape {
	constructor(width, height, color) {
		this.width = width;
		this.height = height;
		this.color = color;
	}
	
	draw() {
		console.log(`drawing ${this.color} color of`);
	}
	
	get Area() {
		return width * this.height;
	}


class Rectangle extends Shape {}
class Triangle extends Shape {
	// Overriding
	draw() {
		// 부모 class의 method 재사용
		super.draw();
		console.log('triangle');
	}
	
	getArea() {
		return (this.width * this.height) / 2;
	}
}

const triangle = new Triangle(20, 20, 'red');
triangle.draw();	// triangle
console.log(triangle.getArea);	// 200
```

## Class checking : instanceOf
`instanceOf` method는 Object가 해당 Class로 인해 instance화 된 Object인지를 확인하기 위한 method이다. 이 때 주의해야할 것은, 상속을 통해 만들어진 Class로 인한 Object인 경우 그 부모 Class의 instance이기도 하다. 또한 JavaScript에서 만든 모든 Class들은 `Object Class`를 상속한다.

``` javascript
console.log(rectangle instanceOf Rectangle);	// true
console.log(triangle instanceOf Rectangle);		// false
console.log(triangle instanceOf triangle);		// true
console.log(triangle instanceOf Shape);			// true
console.log(triangle instanceOf Object);		// true
```