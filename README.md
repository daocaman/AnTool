

### Angular snippets

*1. Express function controller*

#### Prefix : 
```
!expFnctCon
```

#### Table variable

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