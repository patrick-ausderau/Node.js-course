<!DOCTYPE html>
<html>
  <head>
    <title>JS functional programming basics</title>
    <meta charset="utf-8">
    <style>
      @import url(https://fonts.googleapis.com/css?family=Yanone+Kaffeesatz);
      @import url(https://fonts.googleapis.com/css?family=Droid+Serif:400,700,400italic);
      @import url(https://fonts.googleapis.com/css?family=Ubuntu+Mono:400,700,400italic);

      body { font-family: 'Droid Serif'; }
      h1, h2, h3 {
        font-family: 'Yanone Kaffeesatz';
        font-weight: normal;
      }
      .remark-code, .remark-inline-code { font-family: 'Ubuntu Mono'; }
    </style>
  </head>
  <body>
    <textarea id="source">

class: center, middle

## Functional Javascript Basics with map / reduce / filter
#### Server-side scripting frameworks 
#### TX00CR77-3002 / Spring 2018
#### Olli Alm

---

# Contents

* Functional programming (FP)
* FP in Javascript
* Map / Reduce / Filter
* FP with ES6
* Chaining
* Arrays + next steps
* The assignments

---

# Functional programming & programming paradigms

* FP is a programming paradigm / discipline (not just style)
* Paradigms:
  * Object-oriented
  * Functional
  * Logic programming
  * Imperative 
  * ...
* [JS example (Sitepoint)](https://www.sitepoint.com/introduction-functional-javascript/)

---

# Functional programming

* [Wikipedia](https://en.wikipedia.org/wiki/Functional_programming) *"FP is a paradigm ...that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data"*
  * Key point 1: similar to mathematical functions
  * Key point 2: avoids changing state 
  * Key point 3: avoids mutable data

```javascript
const sentence = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.';
const words = sentence.split(' ');

const uppercase = words.map(function(word) {
  return word.toUpperCase();
});

```
* **words.map** transforms each word in array 
  * transformation is a function (a mapping from an input value to an output value)
  * there is no explicit state in the mapping, data "flows through"
  * data is transformed into different object

---

# Map / Reduce / Filter 

* Functions for processing arrays
* Implemented as methods in array class
* [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) transforms each object in the array
  * N items in --> N items out
* [Filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) removes values from an array
  * N items in --> N or less items out
* [Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) will accumulate values into one
  * N items in --> one item out
* Read this: [Map, reduce, filter in JS](http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/)

---

# Functional JS + ES6

ES6 function arrow syntax suits well for functional paradigm

Example, uppercasing words:

```javascript
const words = sentence.split(' ');

// ES5 
const uppercase = words.map(function(word) {
  return word.toUpperCase();
});

// ES6 
const uppercase = words.map( (word) => word.toUpperCase() );

// OR 
const uppercase = words.map( word => word.toUpperCase() );
```

* Notice that `return` [can be omitted](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Function_body) if block body is not used

---

# Functional JS + ES6: calculations

```javascript

// ES5
const numbers = [1, 2, 3, 4];
const newNumbers = numbers.map(function(number){
    return number * 2;
});

// ES6 
const newNumbers = numbers.map( number => number*2 );

```

[source](http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/)

---

# Chaining with map / filter / reduce

```javascript

// upper case each word
words.map( word => word.toUpperCase() );

// remove long words
words.filter( word => word.length < 5 );

// count words (Note: 0 initializes the variable sum), 
// finally sum is returned
const sum = words.reduce( (sum, word) => sum += 1, 0);

// chained
words.map( word => word.toUpperCase() )
     .filter( word => word.length < 5 )
     .reduce( (sum, word) => sum += 1, 0);


```
---

# Array iteration methods

* Note: Map, Filter and Reduce are part of the *[array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) iteration methods*
* In addition, there is
  * [entries()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)
  * [every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
  * [find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
  * [findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
  * [forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
  * [keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)
  * [reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight)
  * [some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
  * [values()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/values)
  * [@@iterator()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@iterator)

**--> Javascript arrays are having powerful tools for (functional) data processing**

---

# Further reading

* [Reduce examples](http://www.programwitherik.com/functional-javascript-with-reduce/)
* [Map, reduce, filter in JS](http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/)
* [Master the Javascript Interview: What is Functional Programming](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)
* [Awesome Functional Javascript](https://github.com/stoeffel/awesome-fp-js)
* [A Gentle Introduction to Functional Javascript](http://jrsinclair.com/articles/2016/gentle-introduction-to-functional-javascript-intro/)
* [Professor Frisby's Mostly Adequate Guide to Functional Programming](https://github.com/MostlyAdequate/mostly-adequate-guide)
* [Dan Martensen, Map, Reduce, Filter](https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter)

---

# Assignment 1: playing with text

Download texts by [Linus](https://gist.githubusercontent.com/OAlm/fc8d4c6eadb057ddbb68959743713c69/raw/4b3a7a1cbdecba5ed71fd49f9c651874067e65ad/linus.txt) and [Turing](https://gist.githubusercontent.com/OAlm/5cda155b75b048d9c82bc5fde5606d81/raw/e0dd59c8987ff8a0861f22d133d32ef83d751a80/turing.txt)

Try out following tasks, **using map, reduce, filter** approach in ES6 syntax

1. Remove punctuations from the text (! ? . , etc.) 
2. List words starting with uppercase 'A'
3. List words starting with letter 'a', incasesensitive
4. Count words
5. Remove all vowels from the text
6. Count all consonants
7. ...
  
---

# Assignment 2: playing with data

Download [Bond villains](https://en.wikipedia.org/wiki/List_of_James_Bond_villains) from [here](https://gist.githubusercontent.com/OAlm/027725f4d3d0e85338a51e6c29c3dfac/raw/091c7ddbb5abe4d21c30cdc3dfd777149a8f5915/bond_villains.json)

Try out following tasks, **using map, reduce, filter** approach in ES6 syntax

1. List all the villains from 1970s
2. Count the average time between the movies
3. Get all the villains who acted in a movie having letter 'e' in their name
4. List all entries with a villain name longer than 15 characters
5. Create a modified JSON without numbers and years
6. ...

[*](http://elijahmanor.com/reducing-filter-and-map-down-to-reduce/)

**Update: return a code sample of your achievements to Oma**

**Be ready to present your achievements on Thursday morning**

    </textarea>
    <script src="https://remarkjs.com/downloads/remark-latest.min.js">
    </script>
    <script>
      var slideshow = remark.create();
    </script>
  </body>
</html>
