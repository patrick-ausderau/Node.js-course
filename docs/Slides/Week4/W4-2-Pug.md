# PUG
  * templating engine used for server-side templating
  * example: 
  ```jade
    div
      h1 My heading
      ul
        li Some list item
        li Some other list item
      p This here is a paragraph.
  ```
  * result:
      ```html
      <div>
        <h1>My heading</h1>
        <ul>
          <li>Some list item</li>
          <li>Some other list item</li>
        </ul>
        <p>This here is a paragraph.</p>
      </div>
      ```

## Use in Express.js
  * [Instructions](https://expressjs.com/en/guide/using-template-engines.html)
  * Excercise 1
    * Create a simple web page using instructions above
  
## Features
  * [Doctype](https://pugjs.org/language/doctype.html)
  * [Attributes](https://pugjs.org/language/attributes.html)
  * [Includes](https://pugjs.org/language/includes.html)
  * Excercise
    * Modify the template of excercise 1 so that the result is [valid HTML](https://validator.w3.org/)
  * [Template inheritance](https://pugjs.org/language/inheritance.html)
  * [Interpolation](Interpolation)
  * [Iteration](https://pugjs.org/language/iteration.html)
  * Excercise
      * Create a UI for your cat-app.
        * Make at least two templates:
            * Add cats
            * List cats
      * Version 1:
              * Use pug to create all HTML; read the data from database and print using pug     
      * Version 2:
        * Use pug just for the UI, add cats and list cats by using front-end JavaScript and REST calls; 
      * Make the UI in two languages
        * user should be able to change between the languages
        * you can add the UI texts to database or use a separate JSON files
