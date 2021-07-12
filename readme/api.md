## Table snippets
|  STT  | Snippets                    | Link                                  |
| :---: | :-------------------------- | :------------------------------------ |
|   1   | Express server.js           | [link](#1Express-serverjs)            |
|   2   | Express app.js              | [link](#2Express-appjs)               |
|   3   | Express new controller      | [link](#3Express-new-controller)      |
|   4   | Express route module        | [link](#4Express-route-module)        |
|   5   | Express function controller | [link](#5Express-function-controller) |
|   6   | Express attribute object    | [link](#6Express-attribute-object)    |
|   7   | Express return promise      | [link](#7Express-return-promise)      |


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
    res.header("Access-Control-Allow-Origin "*");
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

### *4.Express route module*
[menu](#Table-snippets)

#### Prefix
```
!expRoute
```

#### Table variables

|  STT  | Default / Choose type | Description     |
| :---: | --------------------- | --------------- |
|   1   | controllername        | Controller name |

#### Code generate

``` Javascript
// lib
const express = require('express');
const router = express.Router();

// controllers
const ${1:controllername} = require('../controllers/${1:controllername}');

// middleware

// helpers

module.exports = router;
```

---
###

### *5.Express function controller*
[menu](#Table-snippets)

#### Prefix
```
!expFnctCon
```

#### Table variables

|  STT  | Default / Choose type         | Description          |
| :---: | ----------------------------- | -------------------- |
|   1   | function1                     | Function name        |
|   2   | ( ,String,number,Date,Object) | Param type           |
|   3   | param1                        | Pram var             |
|   4   | object                        | Return object        |
|   5   | description                   | Function description |
|   6   | controller                    | Controller           |
|   7   |                               | Place to type code   |


#### Code generate

``` Javascript

/**
* @name ${1:function1}
* @param {${2| ,String,number,Date,Object|}} ${3:param1}
* @returns ${4:object}
* @description ${5:description}
*/
${6:controller}.${1:function1} = async(${3:param1}) => {

    console.log("\\x1b[34m function ${1:function1} : \\x1b[0m" + nameController);
    let responseData = { messages: "", code: 500 };

    let flag = false;

    try {
        $7
    } catch (error) {
        flag = true;
        if(error.code){
            responseData.messages = error.messages ? error.messages: error;
            responseData.code = error.code ? error.code: responseData.code;
        }else{
            responseData.messages = error;
        }
    }

    if (flag) {
        throw(responseData);
    } else {
        return responseData;
    }

}
```

---
###

### *6.Express attribute object*
[menu](#Table-snippets)

#### Prefix
```
!expAttr
```

#### Table variables

|  STT  | Default / Choose type | Description       |
| :---: | --------------------- | ----------------- |
|   1   | field                 | Field object name |
|   2   | ( ,null,'',{})        | Value field       |

#### Code generate

``` Javascript
${1:field}: ${2| ,null,'',{}|},
```

---
###

### *7.Express return promise*
[menu](#Table-snippets)

#### Prefix
```
!expReturnPromise
```

#### Code generate

``` Javascript
return new Promise((resolve, reject) => {
    $1
});
```

---
###

### *8.Express if-else async*
[menu](#Table-snippets)

#### Prefix
```
!expReturn
```

#### Code generate

``` Javascript
if (flag) {
    throw(responseData);
} else {
    return responseData;
}
```

---
###