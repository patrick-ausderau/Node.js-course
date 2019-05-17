## HTTP headers and messaging
#### Server-side scripting frameworks 
#### Olli Alm

---

## Hands-on experiments with HTTP messaging

---

# HTTP Inspector

```javascript
'use strict';
const express = require('express');
const app = express();

app.get('/*', (req, res) => {
  const param1 = req.path;
  const queryparams = req.query;
  res.send('Got to the root with path: '+param1+' with query params: '+
        JSON.stringify(queryparams));
});

console.log('inspector started');
app.listen(3000);

```
* Use the code above as a template 
* Use [HTTP Header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) as reference

---

## Task 1: Send request parameters back in response

---

## Task 2: Create a cookie and send back in response

---

# Further information about cookies

* [Cookies, Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie) 
* [Cookie uses, Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie#Uses)
* Cookies are domain-specific: *"If a cookie's Domain and Path attributes are not specified by the server, they default to the domain and path of the resource that was requested"* (from [Wikipedia / Domain and Path](https://en.wikipedia.org/wiki/HTTP_cookie#Domain_and_Path))
* [Cookie-session library, Express-middleware](https://github.com/expressjs/cookie-session)

---

## Task 3: Send timestamp in response
### (hint: moment.js)

---

## Task 4: Send user agent information in response

---

## Task 5: Send user IP-address in response

---

## Task 6: Do conditional formatting for the content

* Conditional formatting, based on request.headers *accept*-field
* See [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) and [Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)
* use *res.format*, formats (Mime-types), e.g.
  * text/plain
  * text/html
  * text/pdf
  * application/json

---

## Further inspections

* Measure connection speed: https://github.com/ddsol/speedtest.net
* Location based on IP-address?
* Previous web page
* Browser fingerprinting ([Am I unique?](https://amiunique.org) or [panopticlick](https://panopticlick.eff.org/))
* Keystroke identification of the user: https://en.wikipedia.org/wiki/Keystroke_dynamics

For further inspections, see also [List of HTTP header fields in Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) 
