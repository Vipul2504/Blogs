---
title: "! Everything in JavaScript is an Object"
seoTitle: "javascript data types, primitive data types,"
datePublished: Thu Jun 16 2022 13:50:51 GMT+0000 (Coordinated Universal Time)
cuid: cl4h2y4vd05gng1nvgbhidwm6
slug: everything-in-javascript-is-an-object
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/jG8nlwLRZTM/upload/v1655374891823/gt-geaTpc.jpeg
tags: javascript, objects, primitive, data-type

---


Programming languages all have built-in data structures, but these often differ from one language to another. There is a lot of confusion out there as to whether JavaScript is an Object-Orientated programming (OOP) language or a functional language. Indeed, JavaScript can work as either. 
This article will clear all this up.



### Dynamic typing
JavaScript is a loosely typed and dynamic language. Variables in JavaScript are not directly associated with any particular value type, and any variable can be assigned (and re-assigned) values of all types:
``` 
let foo = 42;    // foo is now a number
foo = 'bar'; // foo is now a string
foo = true;  // foo is now a boolean
console.log(foo); // It will show last value that assigned i.e True.

``` 

### Let's start at the start
In JavaScript, there are *six primitive data types*:

1. Number(double-precision 64-bit float. ***There are no integers in JavaScript.***)

2. Null

3. Undefined

4. String

5. Boolean

6. Symbol(new in **ES6**)

**All types except objects define immutable values (that is, values which can't be changed). For example, Strings are immutable. We refer to values of these types as "primitive values".**

```
1.3.14;
2. null;
3. undefined;
4. "hello";
5. true;

// Primitive types
true instanceof Object; // false
null instanceof Object; // false
undefined instanceof Object; // false
0 instanceof Object; // false
'bar' instanceof Object; // false
``` 

In addition to these six primitive types, the ECMAScript standard also defines an object type, which is simply a key-value store.


```
const object = {
  key: "value"
}
``` 

> *So, in short, anything that is not a primitive type, is an Object, and this includes functions and arrays.*


```
// Non-primitive types
const foo = function () {}
foo instanceof Object; // true
``` 

### Primitive types
Primitive types have no methods attached to them; so you'll never see undefined.toString(). Also because of this, primitive types are immutable, because they have no methods attached that can mutate them. You can re-assign a primitive type to a variable, but it will be a new value, the old one is not, and cannot, be mutated.


```
const num = 42
num.foo = "bar";
num.foo; // undefined

``` 
> Primitive types are immutable

Furthermore, the primitive types are stored as the value themselves, unlike objects, which are stored as a reference. This has implications when performing equality checks.

```
"Java" === "Java"; // true
29 === 29; // true

{} === {}; // false
[] === []; // false
(function () {}) === (function () {}); // false

``` 
> Primitive types are stored by value, objects are stored by reference

### Objects 
An object in JavaScript is a collection of key-value pairs. Each key-value pair is called as a property. A property can be a function, an array, an object itself or any primitive data type i.e. integer, string, etc. Functions in objects are called methods.


```
var human = {
	firstName: "Vipul",
	lastName: "Vishwakarma",
	age: 20,
	fullName: function(){
		return this.firstName + " " + this.lastName		
	}
}
```

 **Properties of the object can be accessed using the following two notations:**

  *Dot notation:*

```
human.firstName; //Output: Vipul
``` 

**New properties can be added using the dot notation as shown below:**

```
human.age = 23
human.getAge = function(){
	return this.age;
}
``` 

***Square bracket notation:***

```
human["firstName"]; //Output: Vipul

human["fullName"](); //Output: Vipul Vishwakarma
``` 
**New properties can be added using the Square bracket notation as shown below:**

```
human["weight"] = 65
human.getWeight = function(){
	return this.weight;
}
```


### Function 
A function is a special type of object, with some special properties, such as *constructor* and *call*.


```
const xyz = function (arg) {};
xyz.name; // "hello"
xyz.length; // 1

``` 
And just like a normal object, you can add new properties to the object:

```
foo.bar = "Hello";
foo.bar; // "Hello"

``` 
### Wrapper Object
The confusion arises because of functions like String, Number, Boolean, Function, etc. which, when called with new, create wrapper objects for these primitive types.

 a string is a global function that creates a primitive string when passed in an argument; it will try to convert that argument into a string.


```
String(23); // "23"
String(true); // "true"
String(null); // "null"
``` 

 you can also use the String function as a constructor function.


```
const animal = new String("dog")
typeof animal; // "object"
animal === "dog"; // false

``` 

And this will create a new object (often referred to as a wrapper object) representing the string "dog", with the following properties:


```
{
  0: "d",
  1: "o",
  2: "g",
  length: 3
}
``` 



```
let foo = "abc"; //Primitive 
console.log("abc".length) // 3

``` 

**Q. If primitives have no properties, why does "abc".length return a value?**

**→** Because JavaScript will readily coerce between primitives and objects. In this case, the string value is coerced to a String object in order to access the property length. The string object is only used for a fraction of a second after which it is sacrificed to the Gods of garbage collection.***What's happening is a process called autoboxing. ***

In the above example, to access the property length, JavaScript autoboxed an into a wrapper object, access the wrapper object's length property, and discards it afterward. This is done without affecting foo(foo is still a primitive string).


```
const foo = 42;
foo.ab = "baz"; // Assignment done on temporary wrapper object
foo.ab; // undefined
``` 

This also explains why JavaScript doesn't complain when you try to assign a property to a primitive type because the assignment is done on that temporary wrapper object, not the primitive type itself.

It will complain if you try this with a primitive type that does not have a wrapper object, such as undefined or null.


```
const foo = null;
foo.ans = "baz"; // Uncaught TypeError: Cannot set property 'bar' of null.

```
**In the next part, we will deep dive into each data type.**

**If you enjoyed the article and want updates about my new article✍, follow me on** [Hashnode](https://hashnode.com/@Vipul25)

**All My 👉 [Socials](https://vipul25.bio.link/)**



















- 
