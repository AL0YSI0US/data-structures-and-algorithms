<h1 align="center">Array Index</h1>

> Copied from class Repository [supporting docs for code challenges]

## 👾 array.sort()

### Overview

`array.sort( [compareFunction] )` sorts an array in place -- mutating the array. There is no return value.

The `compareFunction` is a function that is used by sort to evaluate sibling values in turn, and sort in the appropriate order.

* If compareFunction(a, b) is less than 0, sort a to an index lower than b, i.e. a comes first.
* If compareFunction(a, b) returns 0, leave a and b unchanged with respect to each other, but sorted with respect to all different elements.
* If compareFunction(a, b) is greater than 0, sort b to an index lower than a, i.e. b comes first.

### Compare Function Setup

```js
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

### Sample Compare Function

```
function compareNumbers(a, b) {
  return a - b;
}
```

### In actual code ...

```
function compareNumbers(a, b) {
  return a - b;
}

let array = [1,6,4,2,8,11,4,99,129];
array.sort(compareNumbers);

// Or all in line:
array.sort( (a,b) => { 
  return a-b; 
});

```

#### Caveats and Notes

* The speed and technique of the sort functionality internally is determined by JavaScript, so you can't depend on a consistent "complexity" or "time"
* compareFunction(a, b) must always return the same value when given a specific pair of elements a and b as its two arguments. If inconsistent results are returned then the sort order is undefined.

#### Reference

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

---

## 👾 array.map()

### Overview

`array.map( fn(v,i) {} )` Much like`array.forEach()`, the `array.map()` function iterates over an array and runs a call back for each element. The callback receives the value and the index of the array element as a parameter.

The difference is that `.map()` will always return you a **new array** of the **same length** as the original array comprised of your return values

### Squaring a number

```js
  let numbers = [2,3,4,5];
  
  let squares = numbers.map( function(n,i) {
    return n * n;
  });
  
  // or as a snazzy arrow function ...
  // let squares = numbers.map( n => n * n );
  
  console.log(squares); // [ 4, 9, 16, 25 ]
```

### Changing the data shape

```js
  let people = [
    { name: "John", role: "Dad" },
    { name: "Cathy", role: "Mom" },
    { name: "Zach", role: "Kid" },
    { name: "Allie", role: "Kid" },
  ];
  
  let folks = people.map( (person,i) => {
    return person.name;
  });
  
  console.log(folks); // [ "John", "Cathy", "Zach", "Allie" ]
```

**If you do nothing...**

```js
  let numbers = [2,3,4,5];
  
  let squares = numbers.map( function(n,i) {
  });
  
  console.log(squares); // [undefined, undefined, undefined, undefined]
  
```

### Caveats and Notes

* The original array is never mutated
* You always get back a new array
* The array returned is always the same length as the original

### Reference

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* [Medium](https://medium.com/@JeffLombardJr/understanding-foreach-map-filter-and-find-in-javascript-f91da93b9f2c)

---

### 👾 Array.forEach

### Overview

`Array.forEach` allows you to iterate through an array. Where a normal `for` loop is "iterative", forEach is more declarative or functional in nature.

It is implemented as a method on your array instance.

```
  let myArray = ['a', 'b', 'c'];
  myArray.forEach( ... )
```

It takes a callback as a parameter, which in turn receives the value and the iterator, and runs it on every element.

```
  let myArray = ['a','b','c'];

  myArray.forEach( function(value, i) {
    console.log(i);       // 0, 1, 2
    console.log(value);   // a, b, c
  })
```

#### Caveats and Notes

* Applies the callback to each element
* You cannot "Return" a value
* You cannot "break" or "continue" as you can with a for loop
* By default, forEach does not mutate the array
* If you mutate it in process, you will have interesting issues

#### Reference

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
* [ForEach vs For](https://codeburst.io/javascript-the-difference-between-foreach-and-for-in-992db038e4c2)

---

## 👾 array.reduce()

### Overview

`arr.reduce( (accumulator,value,index) => {...}, initialvalue)`

### Basics

`.reduce()` iterates over an array and returns the last version of the "accumulator" ... in each iteration, based on the value and/or idx of the current element in the array, you have the opportunity to modify and return the accumulator. After the last iteration of the array, that accumulator value is returned to the caller. `initialvalue` represents the value of the accumulator in the first iteration.

**Add up all the numbers in an array** In this example, the accumulator starts out as 0 (the initial value) and for each iteration, we simply add onto it, and then return it. That return value gets fed into the next iteration so that you can continually operate on it and return the final value.

```js
let numbers = [1,2,3,4];
let sum = numbers.reduce( function(accumulator,value,idx) {
  accumulator = accumulator + value;
  return accumulator;
}, 0);

// sum would be 10
```

**Change the shape of you data** In this example, we'll take an array of objects and return back an object, keyed by the 'name' property. The initial value is an empty object, and as we iterate, we create a new entry in it, returning it as we build on.

```js
  let people = [
    {name:'Fred', role:'Developer'},
    {name:'Suzy', role:'Developer'},
    {name:'Gina', role:'Manager'},
    {name:'Jim', role:'Support'}
  ];
  
  let folks = people.reduce( (accumulator, person, idx) => {
    accumulator[person.name] = person.role;
    return accumulator;
  }, {} );
  
  // folks:
  {
    Fred: 'Developer',
    Suzy: 'Developer',
    Gina: 'Manager',
    Jim: 'Support'
  }
```

### Reference

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
* [Medium](https://medium.com/@JeffLombardJr/understanding-foreach-map-filter-and-find-in-javascript-f91da93b9f2c)
