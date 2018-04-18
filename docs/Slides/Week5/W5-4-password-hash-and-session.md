# Security continued (3)

## bcrypt

* Never store user password in plain text
* Use a one way hash function with salt 
* Recomendation is to use [bcrypt](https://en.wikipedia.org/wiki/Bcrypt) hashing function
  * Why [not](https://codahale.com/how-to-safely-store-a-password/) md5, sha1, sha256,...?
* You can use NodeJS native [crypto](https://nodejs.org/api/crypto.html) or [bcrypt package](https://www.npmjs.com/package/bcrypt) 

* Installation: 

```shell
npm install bcrypt --save
```

* Basic usage:

```javascript
'use strict';

const bcrypt = require('bcrypt');

const saltRound = 12;
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

