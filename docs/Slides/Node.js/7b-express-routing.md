## Assignment: Express routing
#### Server-side scripting frameworks 
#### Olli Alm

---

# Assignment 1: Rest revisited

* Get familiar with [Express Routing](https://expressjs.com/en/guide/routing.html)

```javascript
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
```

* Use the above example and implement a route for *user*, with methods:
  * get a user by id, identified by *route parameter*
  * update a user, identified by *route parameter*
  * add a user into a collection (no identifier given)
  * delete a user
* dummy implementation is fine, no need for much content
* See also [Rest slide from last week](https://ilkkamtk.github.io/SSSF-course/Slides/Week3/W3-3-rest-and-express.html#10)

---

# Assignment 2: Middleware

* Get familar with [Express Middleware](https://expressjs.com/en/guide/writing-middleware.html)
* Implement a middleware-function that prints into the console
  * timestamp
  * requested path
  * IP-address
  * browser name

---

# Assignment 3: Error handling

* Get familar with [Error handling Middleware](https://expressjs.com/en/guide/error-handling.html)
* Implement an error handler 
  * Error handler should write the event on the screen
  * Error handler should send a meaningful [HTTP Status Code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_error) to user
  * Try to also figure out how to log the errors into user specified file (e.g. error.log)
  
---

# Assignment 4: Middleware libraries

* Get familar with [custom middleware](https://expressjs.com/en/resources/middleware.html)
* Choose a library you didn't know before and tell how you could utilize it in your project?

---

# Assignment 5: Routes in separate modules

* Read a blog entry about [Express Routes](https://www.terlici.com/2014/09/29/express-router.html)
* Implement at least two different route-modules (files) into *routes* folder (same as controllers in blog)
  * Create a separate routes folder (use [Express Generator](https://expressjs.com/en/starter/generator.html) if you like)
  * Route-modules can be e.g. books and cars or something related to your project or weekly task
  * For each module, implement at least two routes
* ** For extra points (if you didn't return last week's weekly task) Return your assignments to Readme.md of this weeks weekly task**
* **Grading: 0-100%, 20% for each correct solution.**
