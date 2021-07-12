## Table snippets
|  STT  | Snippets                    | Link                                   |
| :---: | :-------------------------- | :------------------------------------- |
|   1   | Express server.js           | [link](#1Express-serverjs)             |
|   2   | Express app.js              | [link](#2Express-appjs)                |
|   3   | Express new controller      | [link](#3Express-new-controller)       |
|   4   | Express route module        | [link](#4Express-route-module)         |
|   5   | Express function controller | [link](#5Express-function-controller)  |
|   6   | Express attribute object    | [link](#6Express-attribute-object)     |
|   7   | Express return promise      | [link](#7Express-return-promise)       |
|   8   | Express if-else async       | [link](#8Express-if-else-async)        |
|   9   | Express HTTP API            | [link](#9Express-HTTP-API)             |
|  10   | Express using route         | [link](#10Express-using-route)         |
|  11   | Express require             | [link](#11Express-require)             |
|  12   | Express request data        | [link](#12Express-request-data)        |
|  13   | Express response data       | [link](#13Express-response-data)       |
|  14   | Express response custom     | [link](#14Express-response-custom)     |
|  15   | Express response error data | [link](#15Express-response-error-data) |
|  16   | Debug                       | [link](#16Debug)                       |
|  17   | Debug break                 | [link](#17Debug-break)                 |
|  18   | Comment function            | [link](#18Comment-function)            |
|  19   | Type doc                    | [link](#19Type-doc)                    |
|  20   | Generate prop doc           | [link](#20Generate-prop-doc)           |
|  21   | Debug on/off                | [link](#21Debug-on-off)                |
|  22   | Express multer storage      | [link](#22Express-multer-storage)      |
|  23   | Express multer              | [link](#23Express-multer)              |
|  24   | Express install             | [link](#24Express-install)             |
|  25   | Express copy object         | [link](#25Express-copy-object)         |


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

app.use(logger('dev'));

app.use(bodyParser.json()) // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded
            
app.use((req, res, next) => {
    res.header(Access-Control-Allow-Origin "*");
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

### *9.Express HTTP API*
[menu](#Table-snippets)

#### Prefix
```
!expCRUD
```

#### Table variables

|  STT  | Default / Choose type | Description     |
| :---: | --------------------- | --------------- |
|   1   | description           | API description |
|   2   | (get,post,put,delete) | Http method     |
|   3   | path                  | API path        |

#### Code generate

``` Javascript
//${1:decription}
router.${2|get,post,put,delete|}('${3:path}', ((req, res, next) => {
    console.log('\\x1b[44m====== ~ ${3:path} api ~ ===================================\\x1b[0m');
    ${4:controller}.${5:function}.then(
        data => {
            res.status(200).json(data);
            console.log('\\x1b[44m====== ~ end ${3:path} api ~ ===================================\\x1b[0m');
        }, err => {
            if(err.code){
                res.status(err.code).json({messages: err.messages});
            }else{
                res.status(500).json(err);
            }
            console.log('\\x1b[41m====== ~ end Error ${3:path} api ~ ===================================\\x1b[0m');
        }
    )
}));
```

---
###

### *10.Express using route*
[menu](#Table-snippets)

#### Prefix
```
!expUseRoute
```

#### Table variables

|  STT  | Default / Choose type | Description      |
| :---: | --------------------- | ---------------- |
|   1   | route1                | Route in comment |
|   2   | route1                | Var route        |
|   3   | route1                | Path to route    |
|   4   | route1                | Link to route    |


#### Code generate

``` Javascript
// routing ${1:route1}
const ${2:route} = require('./routes/${3:route1}');
app.use('/${4:route}', ${2:route});
            
```

---
###

### *11.Express require*
[menu](#Table-snippets)

#### Prefix
```
!expRequire
```

#### Table variables

|  STT  | Default / Choose type | Description    |
| :---: | --------------------- | -------------- |
|   1   | link                  | Link to module |
|   2   | var1                  | Var module     |

#### Code generate

``` Javascript
const ${2:var1} = require('${1:link}');
```

---
###

### *12.Express request data*
[menu](#Table-snippets)

#### Prefix
```
!expReqData
```

#### Table variables

|  STT  | Default / Choose type        | Description |
| :---: | ---------------------------- | ----------- |
|   1   | (params,body,query,{},'',[]) | Req data    |

#### Code generate

``` Javascript
let reqData = req.${1|params,body,query,{},'',[]|};
```

---
###

### *13.Express response data*
[menu](#Table-snippets)

#### Prefix
```
!expResponseData
```

#### Code generate

``` Javascript
responseData = {messages: 'Success.'};
```

---
###

### *14.Express response custom*
[menu](#Table-snippets)

#### Prefix
```
!expReponseCustom
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | (messages,data,value) | Field       |
|   2   | data                  | Field value |

#### Code generate

``` Javascript
responseData={${1|messages,data,value|}: ${2:data} };
```

---
###

### *15.Express response error data*
[menu](#Table-snippets)

#### Prefix
```
!expErrResponse
```

#### Table variables

|  STT  | Default / Choose type | Description      |
| :---: | --------------------- | ---------------- |
|   1   | (500,404,400,403)     | Error code       |
|   2   | Missing value.        | Messages reponse |

#### Code generate

``` Javascript
flag = true;
responseData = { code:  ${1|500,404,400,403|}, messages: '${2:Missing value.}' };
```

---
###

### *16.Debug*
[menu](#Table-snippets)

#### Prefix
```
debug
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | item                  | Item flag   |
|   2   | item                  | Item var    |

#### Code generate

``` Javascript
//debug
console.log('\\x1b[33m ${1:item} :\\x1b[0m',${2:item});
        
```

---
###

### *17.Debug break*
[menu](#Table-snippets)

#### Prefix
```
debugBreak
```

#### Table variables

|  STT  | Default / Choose type | Description       |
| :---: | --------------------- | ----------------- |
|   1   | information           | Information break |

#### Code generate

``` Javascript
console.log('\\x1b[42m\\x1b[30m====== ~ ${1:information} ~ ===================================\\x1b[0m');

```

---
###

### *18.Comment function*
[menu](#Table-snippets)

#### Prefix
```
cmtFunct
```

#### Table variables

|  STT  | Default / Choose type | Description          |
| :---: | --------------------- | -------------------- |
|   1   | function1             | Function name        |
|   2   | param1                | Param1 in function   |
|   3   | param2                | Param2 in function   |
|   4   |                       | Return in function   |
|   5   |                       | Function description |

#### Code generate

``` Javascript
/**
* @name ${1:function1}
* @param {object} ${2:param1}
* @param {object} ${3:param2}
* @returns $4
* @description $5
*/
```

---
###

### *19.Type doc*
[menu](#Table-snippets)

#### Prefix
```
!genTypeDoc
```

#### Table variables

|  STT  | Default / Choose type    | Description      |
| :---: | ------------------------ | ---------------- |
|   1   | description              | Type doc         |
|   2   | nameType                 | Type name        |
|   3   | (String, number, object) | Type of property |
|   4   | nameProp                 | Name of property |

#### Code generate

``` Javascript
/** ${1:description}
* @typedef {Object} ${2:nameType}
* @property {${3|String,number,object|}} ${4:nameProp}
*/
```

---
###

### *20.Generate prop doc*
[menu](#Table-snippets)

#### Prefix
```
!genPropDoc
```

#### Table variables

|  STT  | Default / Choose type    | Description |
| :---: | ------------------------ | ----------- |
|   1   | (String, number, object) | Type prop   |
|   2   | nameProp                 | Prop name   |

#### Code generate

``` Javascript
@property {${1|String,number,object|}} ${2:nameProp}
```

---
###

### *21.Debug on-off*
[menu](#Table-snippets)

#### Prefix
```
debugOnOff
```

#### Code generate

``` Javascript
require('dotenv').config();
            
let DEBUG = true;

if (process.env.MY_DEBUG != null) {
    DEBUG = process.env.MY_DEBUG.toLocaleLowerCase() == "true";
}

if (!DEBUG) {
    console.log = function() {}
}
```

---
###

### *22.Express multer storage*
[menu](#Table-snippets)

#### Prefix
```
!expMulterStorage
```

#### Code generate

``` Javascript
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        return cb(null, dir)
    },
    filename: (req, file, cb) => {
        cb(null, filename);
    }
})
```

---
###

### *23.Express multer*
[menu](#Table-snippets)

#### Prefix
```
!expMulter
```

#### Code generate

``` Javascript
const uploadAvatar = multer({
    fileFilter: async(req, file, cb) => {
        cb(null, true);
    }
    storage: storage
});
```

---
###

### *24.Express install*
[menu](#Table-snippets)

#### Prefix
```
!expInstallModule
```

#### Code generate

``` Javascript
npm i body-parser
npm i cors
npm i crypto-js
npm i express
npm i jsonwebtoken
npm i morgan
npm i multer
npm i node-static
npm i nodemon
npm i dotenv
```

---
###

### *25.Express copy object*
[menu](#Table-snippets)

#### Prefix
```
!expCopyObj
```

#### Table variables

|  STT  | Default / Choose type | Description      |
| :---: | --------------------- | ---------------- |
|   1   | data                  | Var new data     |
|   2   | data1                 | Var data to copy |

#### Code generate

``` Javascript
let ${1:data} = Object.assign({},${2:data1});
```

---
###