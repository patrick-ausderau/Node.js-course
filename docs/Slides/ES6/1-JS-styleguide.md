## Javascript Style Guide
#### Server-side scripting frameworks 
#### TX00CR77-3001 / Spring 2017
#### Olli Alm

---

# Contents

* Coding conventions
* Style guides for Javascript
* Linting 

---

# Coding conventions & style guides /1

* Coding conventions define *how* to write your code
* Conventions are about **syntax**: naming, closures, spaces, tabs, comments
* Conventions might also be about **semantics**: the good practices, what structures to avoid and what to prefer
* Conventions **improve readability**
  * Good readability, easy to understand
  * More efficient / faster to write and refactor
  * A team (in a company) follows a certain **style guide**
  * Style guide defines one way to write the code 

---

# Coding conventions & style guides /2

* For programming languages allowing much variance, **conventions are important**
  * Javascript, Python (!)
* **Coding conventions enhance good coding practices**
* A style guide describes a specific set of rules to follow
* **Note:** Coding conventions doesn't have an effect to the application behavior straight
  * With bad conventions, you might have the same functionalities and performance
  * However, testing, maintenance, team work and refactoring of the code might be more difficult
---

# Style guides for Javascript

* [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) ([ES5](https://github.com/airbnb/javascript/tree/es5-deprecated/es5))
* [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html) ([ES5](https://google.github.io/styleguide/javascriptguide.xml))
* [Awesome JS style guides](https://github.com/kciter/awesome-style-guide#javascript)

---

# Linting 

```
"lint was the name originally given to a particular program that flagged 
some suspicious and non-portable constructs (likely to be bugs) 
in C language source code. The term is now applied generically to 
tools that flag suspicious usage in software written in any computer language."

"The term was derived from the name of the undesirable 
bits of fiber and fluff found in sheep's wool."
(Wikipedia)
```
## Linting in JS

* [Comparison of JS Linting tools](https://www.sitepoint.com/comparison-javascript-linting-tools/)
* Recommended: [ESLint](http://eslint.org/) 
* Demonstrations: [ESlint](http://eslint.org/), [JSLint](http://www.jslint.com/), [JSHint](http://jshint.com/)
* Lint tools are integrated in every JS IDE

---

# ESLint 

* Set of rules to be enabled / disabled
* Environments-specific settings
  * [Environment](http://eslint.org/docs/user-guide/configuring): the platform and / or configuration where Javascript is executed
  * browser, node.js, web worker, Jquery, PhantomJS 
  * environment defines which global variables exist, are known
  * [Node.js vs. browser](http://voidcanvas.com/node-vs-browsers/)

