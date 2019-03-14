# Security continued

## Helmet

* [Helmet](https://www.npmjs.com/package/helmet) secures Express.js application by modifying multiple headers. 
* "It's not a silver bullet, but it can help!"

* Installation: 

```shell
npm install helmet --save
```

* Basic usage:

```javascript
const helmet = require('helmet');
app.use(helmet());
```

* `helmet()` applies all default measures. To use only some, enable only those:

```javascript
app.use(helmet.noCache())
app.use(helmet.frameguard())
```

* or disable some:

```javascript
app.use(helmet({
  frameguard: false
}));
```

---

### Exercise

Enable every default module of Helmet but the `X-Download-Options` header setting (`ieNoOpen`)

---

## CORS

* AJAX calls to other domains are forbidden by default by the [same-origin security policy](https://en.wikipedia.org/wiki/Same-origin_policy)
* Implemented by basically all browsers
* Can be relaxed by enabling `Access-Control-*` headers

* [Flow](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Flowchart_showing_Simple_and_Preflight_XHR.svg/2000px-Flowchart_showing_Simple_and_Preflight_XHR.svg.png)

### CORS with Express.js

* To enable Cross-Origin Resource Sharing (CORS), [cors package](https://www.npmjs.com/package/cors) can be used
* It supports enabling CORS for all routes, for single routes, and for pre-flight requests

* Installation:

```shell
npm install --save cors
```

* Enable for all requests:

```javascript
const cors = require('cors');
app.use(cors());
```

---

### Exercise

Implement CORS so that your application only allows CORS for POST on path `/cors-enabled`.

---

## Dependency security

* "Security of your app is only as strong as the “weakest link” in your dependencies."
* To check your dependencies for known vulnerabilities, [nsp](https://www.npmjs.com/package/nsp) can be used

```shell
npm i nsp -g
nsp check
```

---

### Exercise
Check your project for known vulnerabilities

---

## Update Local Packages

It's a good practice to periodically update the packages your application depends on. Then, if the original developers have improved their code, your code will be improved as well (Hopefully).

In the same directory as the package.json file of the application that you want to update:

```shell
npm update
npm outdated
# There should not be any results....
```

---

### Major update

* By default, ``npm update`` only updates minor versions (e.g. ``mongoose  ^5.0.11  →  ^5.0.13`` or ``body-parser      ^1.17.1  →  ^1.18.2``). 
* Major version (e.g. ``dotenv    ^4.0.0  →  ^5.0.1`` or ``passport  ^0.3.2  →  ^0.4.0``) can bring nice new features; but DO NOT GUARANTEE BACKWARD COMPATIBILITY! Double check change logs, readme, etc. to know what changes you might need in your code.
  * Option 1: manually update package.json (or package-lock.json)
  * Option 2: [npm-check-updates](https://www.npmjs.com/package/npm-check-updates)

```shell
npm install -g npm-check-updates
ncu
```

Upgrade a project's package file:

**Make sure your package file is in version control and all changes have been committed. This will overwrite your package file.**

```shell
ncu -u
```

---

### Exercise

Check if your packages are up to date (at least minor version)

---

# Use TLS

* TLS is the new progression of SSL
* Express.js can handle HTTPS [relatively simply](../Week2/W3-4-https-passport.md)
* Generally better to implement TLS in reverse-proxy such as Nginx (as implemented in jelastic)

