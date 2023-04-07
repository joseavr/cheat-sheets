# JS Classes

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---
# 🎬 Intro to Classes

Classes are a relatively new feature added in ES6 (ECMAScript 2015) that provide a way to define objects and their behavior using a syntax that is similar to classes in other object-oriented programming languages like Java, Python, and C++. The new feature is well used in  modern frameworks such as React, Node.js, etc.

The features of the object-oriented programming language include 
-   Inheritance
-   Polymorphism
-   Data Encapsulation
-   Data Abstraction


# 🗳️ Class
- Describes in general what an `object` is with methods and variables.
- <mark style="background: #FF5582A6;">Class declarations are NOT HOISTED</mark>
	- Meaning declare class first and then access it  
	- Otherwise, code like the following will throw a ReferenceError
- Functions are HOISTED
	- You can call function first and then declare it
	- No Error Thrown
```js
class Person {
    name;
    age;
    
	// methods
    sayHello() {
        console.log(`Hello, my name is ${this.name} and 
	                 I am ${this.age} years old.`);
    }
}

```


# 📝 Constructor
- Useful when creating an `object` to specify default values of this instance
- <mark style="background: #FF5582A6;">In inheritance, if child class does not provide a constructor, one will be created by default</mark>
```js
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}

class Student extends Person{
    // No constructor provided then this is created by default
    constructor(...args){
        super(...args);
    }
}
```


# 📃 Objects
- `objects` are instances of the `class`.
- An instance means that objects (`child`) are created based on their class (`parent`).
- Use keyword `new` to create a new instance of the class
- Only one constructor is allowed

## Creating an Instance with Constructor
```js
let person = new Person('John', 30);
person.sayHello(); 
// output: "Hello, my name is John and I am 30 years old."
```


# 📦 Variables in Classes

## Instance Variables
- `Instance Variables` are available across all objects but unique for each object.
- In other words, an instance variable from one object differs from another object. For instance:
```js
student_1.name = "Jose"
student_2.name = "Kevin"
```
- Instance Variables has **NO TYPES**
```js
class Class {
	id;
	name;
	age;
}
```


## Class Variables
- `Class Variable` are shared between all objects.
- If the class variable from a object is modified, another object of the same class also updates it.
- Instance variables are preceded by the `static` keyword.
- All `static` needs to be called with their `Class` name, instead of `this`.
```js
class Car {
    static dealership = "Terp Cars"; // static public
    static #instances = 0; // static private 

    info() {
        return `${Car.#printDealer()}`
    }

    static #printDealer(){ //static-private function
	    Car.#instance++;
		return `${Car.dealership}`;
    }
}
```


## Public vs Private Variables

`Public`
- In Javascript, **methods** and **data** are public by default
	- Public: can be accessed outside of class
- Public variables are accessible from outside the class and can be accessed using the dot notation (`<instance>.dataField`)
- Public keyword not required.
```js
class Person { 
    name; // public member
    constructor(name) { 
        this.name = name; // Allowed access
    }
}
let person = new Person("Jose")
student_1.name // Allowed access
```

`Private`
- Private: cannot be accessed outside of class, only accessible from inside the clas
- Defined using the (`#`) symbol before the ***variable*** or ***function*** name.
```js
class Person { 
    #age; // private member
    constructor(age) { 
        this.#age = age; // Allowed access
    }
    
    #sayHello() {
        console.log(`Hello, I am ${this.#age} years old.`);
    }
}
let person = new Person(30);
console.log(person.age); // No Allowed since outside of class, Error
person.constructor() // No Allowed since private, Error
```


## Java toString

`toString()`
- Like toString in Java, returns default info when object is printed
- `Symbol` is a primitive data type, called special symbol
- This is a way to add `properties` to an object
```js
[Symbol.toPrimitive]() {
    return `Dealership: ${Car.dealership}`;
}

let new_car = new Car()
console.log(new_car) // Dealership: Terp Cars
```

## Wrap Up
- **Public** - by default
- **Private** - add `#`

- **Instance member** (non static) - only instances objects can call these members
- **Static member** - add `static`, only the ***Class*** can call these members

# 👨‍👦 Inheritance
- Inheritance is a way to create a new class that is a modified version of an existing class.
- In JavaScript, inheritance can be achieved using the `extends` keyword.
- **Rule**: `child` extends `parent` class
```js
class Car {
    model;
    year;
    wheels;
    static dealership = "Toyota";
    static #carSold = 0; // shared all instances, no access outside

    constructor(model, year, wheels){
        this.model = model;
        this.year = year;
        Car.#carSold++;
    }
	
    // Java's toString()
    [Symbol.toPrimitive]() {
        return `
            Car sold: ${this.model}, ${this.year},
            Car sold by: ${Car.dealership}
        `;
    }

    info(){
        document.writeln(`
            ${this.model}, ${this.year}, ${this.wheels}, 
            ${Car.dealership}, ${Car.#carSold}`
        )    
    }

    // getter
    get model(){
        return this.model
    }

    // setter
    set model(newModel) {
        this.model = newModel;
    }
}
```

```js
class SportsCar extends Car {
    #engine;
    
    constructor(model, year, wheels engine) {
        super(model, year, wheels);
        this.#engine = engine;
    }
    
    get engine(){ return this.#engine; }

    set engine(newEngine){ this.#engine = newEngine; }

    // Overrides info() from Car
    info() {
        super.info(); // call parent Class method
        document.writeln(this.#engine);
    }

	// Overrides toString()
    [Symbol.toPrimitive]() {
        return `
            ${super[Symbol.toPrimitive]()}, Engine: ${this.#engine}
        `;
     }
}
```


# 👥 Polimorphism
- Polymorphism is a concept in object-oriented programming that allows objects of different classes to be treated as if they were objects of the same class, as long as they share a common interface or inheritance hierarchy. 
- This means that a method can behave differently depending on the object it is called on.
- This can be achieved through method overriding. 
- In the example above, the `SportsCar` class overrides the `info` method inherited from the `Car` class to provide a different implementation specific to sport car. This method behaves differently depending on the object it is called on, even though the method has the same name.
```js
function carInfo(car) {
  car.info();
}

let car = new Car('Corolla', '2001', 4);
let sport = new SportsCar('Camaro', '2023', 6);

// Polimorphism
carInfo(car); // output: "Corolla, 2001, 4, Toyota, 1"
carInfo(sport); // output: "Camaro, 2023, 6, Toyota, 2"
```

In this way, **polymorphism** allows us to write more flexible and reusable code by creating classes that share a common interface but can have different implementations for their methods.