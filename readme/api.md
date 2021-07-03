|  STT  | Snippets                    | Link                                  |
| :---: | --------------------------- | ------------------------------------- |
|   1   | Express Function Controller | [link](#1Express-function-controller) |

[1.Express function controller](#1Express-function-controller)
### 2.Express function 1
dsfsdfs

dsfsdfs

dsfsdfs


dsfsdfs

dsfsdfs

dsfsdfs

dsfsdfs

dsfsdfs

dsfsdfs

### 1.Express function controller

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
