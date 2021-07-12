## Table snippets
|  STT  | Snippets               | Link                             |
| :---: | :--------------------- | :------------------------------- |
|   1   | Express server.js      | [link](#1Express-serverjs)       |
|   2   | Express app.js         | [link](#2Express-appjs)          |
|   3   | Express new controller | [link](#3Express-new-controller) |


### *1.Express server.js*
[menu](#Table-snippets)

#### Prefix
```
!expServer.js
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | 3000                  | Port API    |

#### Code generate

``` Javascript
const http = require('http');
const app = require('./app');

const port = process.env.PORT || ${1:3000};

const server = http.createServer(app);

server.listen(port);
```

---
###

### *2.Express app.js*
[menu](#Table-snippets)

#### Prefix
```
!expApp.js
```

#### Code generate

``` Javascript
const express = require('express');
const app = express();
const bodyParser = require('body-parser');
const logger = require('morgan');

app.use(bodyParser.json()) // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded
            
app.use((req, res, next) => {
    res.header("Access-Control-Allow-Origin", "*");
    res.header(
        "Access-Control-Allow-Headers",
        "Origin, X-Requested-With, Content-Type, Accept, Authorization,  X-Access-Token"
    );
    if (req.method === 'OPTIONS') {
        res.header('Access-Control-Allow-Methods', 'PUT, POST, PATCH, DELETE, GET');
        return res.status(200).json({});
    }
    next();
});

module.exports = app;
```

---
###

### *3.Express new controller*
[menu](#Table-snippets)

#### Prefix
```
!expCon
```

#### Table variables

|  STT  | Default / Choose type | Description     |
| :---: | --------------------- | --------------- |
|   1   | tb                    | Model db        |
|   2   | nameController        | Controller name |

#### Code generate

``` Javascript
const ${1:tb} = require("../models/${1:tb}"); //${1:tb} tablename
            
let nameController = "${2:nameController}";

${2:nameController} = {

};


module.exports = ${2:nameController}
```

---
###