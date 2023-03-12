---
title: "InDepth Explanation of .map() , .reduce(), .filter() and .sort() methods"
datePublished: Sat Aug 13 2022 23:41:53 GMT+0000 (Coordinated Universal Time)
cuid: cl6sjlm530c2xfdnv7otqa8kc
slug: indepth-explanation-of-map-reduce-filter-and-sort-methods
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/VPmMy8YA_cU/upload/v1660211880930/TQBdkTnci.jpeg
tags: blog, javascript, software-engineering, frontend-development, array-methods

---

**Introduction**
In this article, We will take a look at the most used javascript methods for array transformations: filter(), map() and reduce() sort(). We will also take a look at in which condition these methods should be used.

## 1) .map()
***Map is used to create a new array from an existing array***. Like create every string in the uppercase form, and make a new array with those. Just like forEach. It calls that callback with every element in the array, but it builds a new array with those values and the map does not modify the original value of an array. So here's a simple example here I have an array called text.

**Syntax**

```
const new_array = arr.map(function callback(element, index, array) {
    // Return value for new_array
}[, thisArg])
``` 

> **In the callback, only the array element is required.** 


```
const text = ["Hello", "world", "Welcome", "JavaScript"];
const caps = text.map(function (t) {
      return t.toUpperCase();
})

//The above function can be written in the arrow function
const caps = text.map(t => {
    return t.toUpperCase()
})

console.log(text) //[ 'Hello', 'world', 'Welcome', 'JavaScript' ]
console.log(caps) //[ 'HELLO', 'WORLD', 'WELCOME', 'JAVASCRIPT' ]
``` 

> **when a function returns nothing, the value you get is undefined.
So it will create an array of four undefined.**


```
const text = ["Hello", "world", "Welcome", "JavaScript"];
const caps = text.map(function (t) {
       t.toUpperCase();
})
console.log(caps) // [ undefined, undefined, undefined, undefined ]

``` 

*If we look at a text, it's an array full of undefined. Because Map doesn't care what the return value is, it's going to take whatever is returned from our function and add it into a new array four times because it ran our function four times. There are four elements here and each time nothing was returned.*

## 2) .filter() 
A filter allows us to filter out subsets of an array. Basically, we pass in a function that returns true or false, a test function. And if an element passes that function, it will be added to the returned or the result array. If no elements pass the test, an empty array will be returned.

So if we had an array of a bunch of numbers, we want to create a new array with only the even numbers.
**It doesn't update the original, it doesn't mutate it**. So filtering it out makes it sound like we're removing them. We're really just creating a copy with specific targeted information or elements.

**Syntax**


```
const new_array = arr.filter(function callback(element, index, array) {
    // Return true or false
}[, thisArg])
``` 

> **The syntax for filter is similar to map, except the callback function should return true to keep the element, or false otherwise. In the callback, only the element is required.**


> **Let's see an example**


```
const numbers = [9, 8, 7, 6, 5, 4, 3, 2, 1];

const even = numbers.filter(n => {
    return n % 2 == 0 // our callBack returns true or false,
    //if it is true then n is added to the new filtered array
});

const odd = numbers.filter(n => {
    return n % 2 == 1 // our callback returns true or false,
    //if it is true then n is added to the new filtered array
});

console.log(even); //[ 8, 6, 4, 2 ]
console.log(odd); //[ 9, 7, 5, 3, 1 ]
console.log(numbers); //[ 9, 8, 7, 6, 5, 4, 3, 2, 1 ]
``` 

> **So it starts with an empty array, filter() calls a provided callbackFn function once for each element in an array whenever an element passed the function it gets added to the array.**

**let's see an example**


```
const numbers = [9, 8, 7, 6, 5, 4, 3, 2, 1];

const nothing = numbers.filter(n => {
    return n % 2 == 4 // our callBack returns true or false,
    //if it is false then n is not added to the filtered array
});

console.log(nothing); //[]
console.log(numbers); //[ 9, 8, 7, 6, 5, 4, 3, 2, 1 ]

``` 

>  **If no elements pass the test, an empty array will be returned. **

## 3) .reduce()
It takes an array of values and reduces them down to a single value. 

**Syntax**

```
arr.reduce(callback, [initialValue])
``` 

reduce is an array method we passed in a callback and that callback needs to follow a particular format.
That format looks like this.


![reduce3x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660425145316/NXTtAr2lK.png align="center")

** the first parameter here will store the total or the accumulated value that we're reducing down to. And then the current value or just the second parameter here stores each individual element. So this example sums all numbers in this array. If we take a look at this table, I think it helps explain how it works.**

> **here an example of .reduce()**

```
const numbers = [ 5, 4, 3, 2, 1];

//sum of an array
const sum = numbers.reduce((accumulator, currentValue) =>{
    return accumulator + currentValue;
});

console.log(sum); // 15
console.log(numbers); //[ 5, 4, 3, 2, 1 ]
``` 


> *The accumulator variable is going to start as the first element in the array and the current value starts as the next element. And if you look at what we're returning, accumulator plus current value. So take the current total, which is initialized to the first element 5. Add it to the next value 4. *

> *The current value gives us 9. So we return 9 which is then used as an accumulator in the next iteration. So Accumulator now remembers the last time, the last sum, which was 9. So now Accumulator is 9 and current value is the next element 3. This iteration will go until it gets a single value answer. i.e 15.
*

** We can also do things like finding the maximum value in an array where the accumulator is really just tracking the max. It's not being added to or multiplied or anything like that. It's simply referring to the current maximum value. And then we potentially update max if we find a larger value. So let me show you a quick example here.**

> **max using reduce**


```
const grades = [65, 34, 78, 98, 84, ,69, 45, 59, 47,,96];
const Maxgrades = grades.reduce((max, currVal) => {
    if(max < currVal){
        return currVal
    }
    return max;
})

console.log(Maxgrades)
``` 


![methodreduce.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660428242325/5ZmZ45Hi3.png align="center")

*We can also optimize our above code using **Math.max()***


```
const grades = [65, 34, 78, 96, 84, ,69, 45, 59, 99];
const Maxgrades = grades.reduce((max, currVal) => {
    return Math.max(max, currVal)
})

console.log(Maxgrades)// 99
``` 


> **Min using reduce**


```
const grades = [65, 34, 78, 96, 84, ,69, 45, 59, 99];
const Mingrades = grades.reduce((min, currVal) => {
    return Math.min(min, currVal)
})

console.log(Mingrades)// 34
``` 


*So there's one extra argument we haven't learned. When you use reduce, you can actually pass in an initial starting value. So after your callback, the format would be something reduce. After your function, you can add a comma and then an initial value.**When we don't specify an initial value, it will just use the first element.***

> **let's see by an example**


```
const numbers = [ 5, 4, 3, 2, 1];
const sum = numbers.reduce((sum, currentValue) => {
    return sum + currentValue;
}, 100);

console.log(sum); //115
``` 

 **As you see we have passed the 100 as an initial value it means that the accumulator(first index) starts with 100 the second index(i.e 5) will be the first index of an array and it gets added to the total sum.**

## 4) .Sort() 
In JavaScript, the sorting behaves differently than in other languages.  The default sort order is ascending. It covert elements into strings and then compares their sequences of UTF-16 code unit values.

> **see example below**


```
const array = [1, 30, 4, 21, 10000];
array.sort();
console.log(array);//[ 1, 100000, 21, 30, 4 ]
//expected output:-[1,4,21,30,10000]

```
> I have no idea why this decision was made, but the default, as we've already seen, is to convert all of these numbers to strings and sort them as strings. And that leads to some very odd behavior.

**This is How JavaScript developer Feels**
![5m4o.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1660150146963/qgVfBHksZ.gif align="center")

**Here is Syntax** 

***sort(function compareFn(a, b) { /* … */ })*** 

**Q) What is compareFn function?**

-> a function that defines the sort order. If omitted, the array elements are converted to strings, then sorted according to each character's Unicode code point value.

**Q) What is a? ** 

-> *The first element for comparison.*

**Q) What is b?**

->*The second element for comparison.*

**Q) So How can we resolve this issue?**

  -> there is some rule for sorting according to your preference.

**Rule 1) if CompareFn(a, b) returns less than 0 **

*sort a before b*

**Rule 2) if if CompareFn(a, b) returns greater than 0**

*sort b before a*

**Rule 3) if CompareFn(a, b) returns 0**

*leave a and b unchanged with respect to each other*


![Screenshot (49).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660154684058/bO2ChU084.png align="left")

> **So this is always kind of confusing to explain when you look at it this way. It may not make a lot of sense, but let me show you how we would use it here**



```
const array = [1, 30, 4, 21, 10000];
array.sort((a, b) => a - b);
console.log(array);//[ 1, 4, 21, 30, 10000 ]

``` 


![sort.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660156721083/bjZKyEcVZ.png align="left")


> So if we walk through this with a simple example, the first time this callback is executed, we have A 1 and 
B 30. And the way our compare function is set up is that it returns A minus B, so 1 - 30 is going to be a negative number. So what does it do with a negative number? It sorts A before B, so that means that it's going to sort 1 before 30.
and the value of new A will be 30 and b will be iterated throughout the array until all the value got sorted.

***The value of A it's taken from the last element of endResult and B is taken from the original array to compare and sort.***


> **let's see an example of descending order**


```
const array = [1, 30, 4, 21, 10000];
array.sort((a, b) => b - a);
console.log(array);//[ 10000, 30, 21, 4, 1 ]
``` 


**The sort() method returns a reference to the original array, so mutating(changing) the returned array will mutate(change) the original array as well.**

**Q) How can you save your original array in *.sort()* ?**

-> So if I wanted to just have two clearly different results where I was not sorting the same array, I could either declare two variables array one and then make a duplicate of prices with the same data. Or I could use a method to copy the data into a new array, we can return a shallow-copied array like other array methods (e.g. map()) do, you can do a shallow copy before calling **sort(),** using the **spread syntax **or **.slice().**

> **here is an example using spread syntax**


```
const numbers = [3, 1, 4, 1, 5];
// [...numbers] creates a shallow copy, so sort() does not mutate the original
const sorted = [...numbers].sort((a, b) => a - b);
console.log(sorted) //[ 1, 1, 3, 4, 5 ]
console.log(numbers) //[ 3, 1, 4, 1, 5 ]

``` 

>** here is an example using slice()**


```
const numbers = [3, 1, 4, 1, 5];
// [.slice()] creates a shallow copy because there is no argument in slice, 
//so sort() does not mutate the original.
const sorted = numbers.slice().sort((a, b) => a - b);
console.log(sorted) //[ 1, 1, 3, 4, 5 ]
console.log(numbers) //[ 3, 1, 4, 1, 5 ]

``` 

> **If we do not pass any argument in Slice. It returns a shallow copy of elements from the original array and It does not change the original array.**

**Ohh You are reached here.🥳**

![im-so-excited-freaking-cant-wait.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1660433241591/aBSz_kbkR.gif align="center")

*In this article, we saw how map(), filter() reduce() and sort() can ease the life of a developer by reducing the number of unnecessary Forloops and empty array declarations. The end result of this is that our code is made more functional and easy to comprehend.The next article will discuss how to use this method together and how to make own map reduce filter and sort methods *

*So Far We have learned a lot. Do ask questions for clarifications and make corrections & suggestions, I expect them. That is all from my end, please share your views in the comment section, and thanks for reading it. Check out my other article [here](https://vipulvishwakarma.hashnode.dev/). Also, Subscribe to my newsletter. Follow me on [Social](https://vipul25.bio.link/). Happy Learning and Coding*


![ty-eee.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1660433348262/n4rVPK9D0.gif align="center")




















