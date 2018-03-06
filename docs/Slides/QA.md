# Multiple local environments

E.g. flipping between 2 local databases. Note that it is [NOT](https://www.npmjs.com/package/dotenv#should-i-have-multiple-env-files) recommended!

* .env
```javascript
APP_PORT=3000
```

* .env.test
```javascript
APP_PORT=3002
```

* index.js
```javascript
'use strict';
const express = require('express');
const app = express();

app.listen(process.env.APP_PORT);

app.get('/', (req, res) => {
  res.send('Hello World!');
});
```

* run .env
```shell
$  node -r dotenv/config index.js 
```

* run .env.test
```shell
$  node -r dotenv/config index.js dotenv_config_path=.env.test
```

# Logging to file

* `console.log` limitations:
  * outputs only to single place: stdout
  * No possibility to set logging level (debug, info, warning, etc.)
  * No support for metadata

## morgan (access logs)

[morgan](https://www.npmjs.com/package/morgan) is an HTTP request logger middleware for node.js

* index.js
```javascript
'use strict';
const express = require('express')
const fs = require('fs')
const morgan = require('morgan')
const path = require('path')
 
const app = express()
 
// create a write stream (in append mode) 
const accessLogStream = fs.createWriteStream(path.join(__dirname, 'access.log'), {flags: 'a'})
 
// setup the logger 
app.use(morgan('combined', {stream: accessLogStream}))
 
app.get('/', (req, res) => {
  res.send('hello, world!')
})
```

## Winston (application logs)

[Winston](https://www.npmjs.com/package/winston) is designed to be a simple and universal logging library.
* Available loggers: console, file, http and memory. Custom ones allowed too.

* Usage:
```javascript
const winston = require('winston');
winston.log('info', 'Hello distributed log files!');
winston.info('Hello again distributed logs');

winston.level = 'debug';
winston.log('debug', 'Now my debug messages are written to console!');
```

* Default logger is console, to change for file use winston.configure:
```javascript
winston.configure({
    transports: [
        new (winston.transports.File)({ filename: 'somefile.log' })
    ]
});
```

# Authentication and Authorization

* Authorization for you app, check [acl](https://www.npmjs.com/package/acl)
* Authentication for an API, I would go for [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken). First search result gives this [example](https://scotch.io/tutorials/authenticate-a-node-js-api-with-json-web-tokens).
