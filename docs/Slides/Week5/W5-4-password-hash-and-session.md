# Security continued (3)

## bcrypt

* never store user password in plain text
  * avoid returning password and salt in results from DB queries
* use a one way hash [key stretching](https://en.wikipedia.org/wiki/Key_stretching) function with random salt like [bcrypt](https://en.wikipedia.org/wiki/Bcrypt) (or scrypt, argon2, etc.)
  * why [not](https://codahale.com/how-to-safely-store-a-password/) md5, sha1, sha256,...? 
  * try to be slow when computing hashes
* you can use NodeJS native [crypto](https://nodejs.org/api/crypto.html) or [bcrypt package](https://www.npmjs.com/package/bcrypt) 

---

* Installation: 

```shell
npm install bcrypt --save
```

---

* Basic usage:

```javascript
'use strict';

const bcrypt = require('bcrypt');

const saltRound = 12; //okayish in 2018
const myPwd = 'Secret123?';

bcrypt.hash(myPwd, saltRound, (err, hash) => {
  // Store hash in the database
});

// Load hash from your database
bcrypt.compare(myPwd, hash, (err, res) => {
    // res == true (hopefully)
});
```

---

## session

* HTTP is a staless protocol; session is a way to remember your users over multiple requests
* after user logged in, store some user info (e.g. id) in two main ways with cookies
  * on the server
    * stores only a session identifier on the client within a cookie and stores the session data on the server's memory or in a database
    * require more processing on the server
    * if not well managed, risk of leaking memory
  * on the client
    * limited amount of data from browser's max cookie size 
    * if you have multiple cookies, they are sent in every request
    * all data will be visible on user's browser
    * if an attacker find your encrytion secret key, s/he will be able to read all the data 
* NEVER persist user sensitive data in sessions, like password and salt

---


