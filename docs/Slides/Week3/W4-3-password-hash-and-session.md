# Security continued

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
const myPwd = 'Secret123😉';

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

* HTTP is a stateless protocol; session is a way to remember your users over multiple requests
* after user logged in, store some user info (e.g. id) in two main ways with cookies
  * on the server with [express-session](https://www.npmjs.com/package/express-session)
    * stores only a session identifier on the client within a cookie and stores the session data on the server's memory or in a database
    * require more processing on the server
    * if not well managed, risk of leaking memory
  * on the client with [cookie-session](https://www.npmjs.com/package/cookie-session)
    * limited amount of data from browser's max cookie size 
    * if you have multiple cookies, they are sent in every request
    * all data will be visible on user's browser
    * if an attacker find your encryption secret key, s/he will be able to read all the data 
* NEVER persist user sensitive data in sessions, like password and salt

---

### example with express-session and passport-session

* Installation:

```shell
npm install express-session --save
```

---

* Basic usage:
  * Note: to have the secure cookie to work, you must use [https](../Week2/W3-4-https-passport.html) and in production environment behind a proxy (like in jelastic) you have to [enable trust proxy](../Week2/W3-4-https-passport.html#express-jelastic).

```javascript
'use strict';
const session = require('express-session');
const passport = require('passport');
// require express, bcrypt, https, helmet, ssl certicates, etc.

const LocalStrategy = require('passport-local').Strategy;
passport.use(new LocalStrategy(
  (username, password, done) => {
    // prefer asynchronous bcrypt.compare(pwd, hash, (err, res) => {})
    if (username === process.env.username 
        && bcrypt.compareSync(password, process.env.pwdhash)) {
      return done(null, { username: username });
    } else {
      done(null, false, {message: 'Incorrect credentials.'});
      return;
    }
  })
);

// data put in passport cookies needs to be serialized
passport.serializeUser((user, done) => {
  done(null, user);
});

passport.deserializeUser((user, done) => {
  done(null, user);
});

app.use(session({
  secret: 'some s3cr3t value',
  resave: true,
  saveUninitialized: true,
  cookie: { secure: true, // only over https
    maxAge: 2 * 60 * 60 * 1000} // 2 hours
}));
app.use(passport.initialize());
app.use(passport.session());

https.createServer(sslstuff, app).listen(3000);

app.get('/', (req, res) => {
  if(req.user !== undefined)
    return res.send(`Hello ${req.user.username}!`);
  res.send('Hello Secure World!');
});

app.post('/login', 
  passport.authenticate('local', { 
    successRedirect: '/', 
    failureRedirect: '/failed' 
  })
);
```

---

### Session store

* memory databases
  * [redis](https://redis.io/) is popular, store your session with [connect-redis](https://www.npmjs.com/package/connect-redis)
  * [memcached](https://memcached.org/) is another and is available on jelastic, use [connect-memcached](https://www.npmjs.com/package/connect-memcached)
* mongo database with [connect-mongodb-session](https://www.npmjs.com/package/connect-mongodb-session)
* [etc.](https://www.npmjs.com/package/express-session#compatible-session-stores)

---

* Install:

```shell
npm install connect-memcached --save
```

---

* Basic usage:

```javascript
const MemcachedStore = require('connect-memcached')(session);

app.use(session({
      secret  : 'CatOnKeyboard'
    , key     : 'test'
    , proxy   : 'true'
    , store   : new MemcachedStore({
        hosts: ['127.0.0.1:11211'],
        secret: '123, easy as ABC. ABC, easy as 123'
    })
}));
```

---

## Rest API session

* consider [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token)
* a popular implementation in node is [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)

