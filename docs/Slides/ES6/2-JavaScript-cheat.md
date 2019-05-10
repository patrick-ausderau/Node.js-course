#JavaScript cheatsheet

### Variables
#### Old way
```javascript
var name = 'Jeppe';
var age = 10:
```

#### ES6
```javascript
// if value stays constant
const name = 'Jeppe';
// if value can change later
let age = 10;
```

### Functions
#### Really old way (unless you want to add method to class)
```javascript
function myFunction(param1, param2) {
  // do something... 
}
```
#### Old way
```javascript
var myFunction = function(param1, param2) {
  // do something...
}
```
#### ES6
```javascript
const myFunction = (param1, param2) => {
  // do something...
}
```

### Selecting HTML elements
```html
<p id="btn">Click me!</p>
```
```javascript
const element = document.querySelector('#btn');
```

### Event handling
#### Really old way
```html
<p onclick="// do something...">Click me!</p>
```
#### Old way
```javascript
element.onclick = function(evt){
  // do something...
};
```
#### ES6
```javascript
element.addEventListener('click',  (evt) => {
  // do something...
});
```

### AJAX get method
#### Old way
```javascript
const xhr = new XMLHttpRequest();
xhr.open('get', 'someUrl');
xhr.onreadystatechange = function(){
   if (xhr.readyState == 4 && xhr.status == 200) {
         const result = JSON.parse(xhr.responseText);
         console.log(result);
      }
}
xhr.send();
```
#### New way
```javascript
fetch('someUrl')
  .then( (response) => {
    return response.json();
  })
  .then( (result) => {
    console.log(result);
  });
```

### AJAX post method
#### Old way
```javascript
// get data from e.g. form
const myForm = document.querySelector('form');
const fData = new FormData(myForm);
const xhr = new XMLHttpRequest();
xhr.open('post', 'someUrl');
xhr.onreadystatechange = function(){
   if (xhr.readyState == 4 && xhr.status == 200) {
         const result = JSON.parse(xhr.responseText);
         console.log(result);
      }
}
xhr.send(fData);
```
#### New way
```javascript
// some data
const data = {
  username: 'someuser',
  password: 'somepassword'
};
// settings object for fetch 
const settings = {
  method: "POST", // *GET, POST, PUT, DELETE, etc.
  mode: "cors", // no-cors, cors, *same-origin
  cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
  credentials: "same-origin", // include, *same-origin, omit
  headers: {
      "Content-Type": "application/json",
      // "Content-Type": "application/x-www-form-urlencoded",
  },
  redirect: "follow", // manual, *follow, error
  referrer: "no-referrer", // no-referrer, *client
  body: JSON.stringify(data), // body data type must match "Content-Type" header  
};
fetch('someUrl', settings)
  .then( (response) => {
    return response.json();
  })
  .then( (result) => {
    console.log(result);
  });
```
