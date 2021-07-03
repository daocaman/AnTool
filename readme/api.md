## Table snippets
|  STT  | Snippets                    | Link                                  |
| :---: | :-------------------------- | :------------------------------------ |
|   1   | Express app.js              | [link](#1Express-appjs)              |
|   2   | Express server.js           | [link](#2Express-serverjs)           |
|   3   | Express Function Controller | [link](#3Express-function-controller) |

### *1.Express app.js*

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
            "Origin, X-Requested-With, Content-Type, Accept, Authorization,  X-Access-Token",
        );
        if (req.method === 'OPTIONS') {
            res.header('Access-Control-Allow-Methods', 'PUT, POST, PATCH, DELETE, GET');
            return res.status(200).json({});
        }
        next();
    });

    // config sequelize, db
    const sequelize = require("./configurations/Squelize-config");
    sequelize.sync();

    module.exports = app;
```

---

### *2.Express server.js*

#### Prefix
```
!exp
```

### *3.Express function controller*

#### Prefix : 
```
!expFnctCon
```

#### Table variable

 |  STT  | Default / Choose type       | Description              |
 | :---: | --------------------------- | ------------------------ |
 |   1   | function1                   | Function name            |
 |   2   | (String,number,Date,Object) | Choose type of parameter |
 |   3   | param1                      | Parameter                |
 |   4   | object                      | Return type              |
 |   5   | object                      | Function description     |
 |   6   | controller                  | Controller               |
 |   7   |                             | Writing code place       |

#### Code generate

``` Javascript
    /**
    * @name ${1:function1}
    * @param {${2|String,number,Date,Object|}} ${3:param1}
    * @returns ${4:object}
    * @description ${5:object}
    */
    ${6:controller}.${1:function1} = async(${3:param1} = null) => {,

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
