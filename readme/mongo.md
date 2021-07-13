## Table snippets
|  STT  | Snippets               | Link                              |
| :---: | :--------------------- | :-------------------------------- |
|   1   | Mongo config           | [link](#1Mongo-config)            |
|   2   | Mongo model            | [link](#2Mongo-model)             |
|   3   | Mongo model field      | [link](#3Mongo-model-field)       |
|   4   | Mongo db finding       | [link](#4Mongo-db-find)           |
|   5   | Mongo db find one      | [link](#5Mongo-db-find-one)       |
|   6   | Mongo db find by id    | [link](#6Mongo-db-find-by-id)     |
|   7   | Mongo db create        | [link](#7Mongo-db-create)         |
|   8   | Mongo db exclude       | [link](#8Mongo-db-exclude)        |
|   9   | Mongo db ref           | [link](#9Mongo-db-ref)            |
|  10   | Mongo db regExp        | [link](#10Mongo-db-regExp)        |
|  11   | Mongo db populate line | [link](#11Mongo-db-populate-line) |
|  12   | Mongo db populate obj | [link](#12Mongo-db-populate-obj) |

### *1.Mongo config*
[menu](#Table-snippets)

#### Prefix
```
!mongoConfig.js
```

#### Code generate

``` Javascript

const mongoose = require('mongoose');
const dbConfig = require('./dbConfig');
var link_db = "mongodb+srv://{username}:{password}@managecompany.wz3vd.mongodb.net/{database}?retryWrites=true&w=majority"
link_db = link_db.replace("{username} dbConfig.user_db);
link_db = link_db.replace("{password}", dbConfig.password);
link_db = link_db.replace("{database}", dbConfig.database_name);
mongoose.connect(link_db, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
    useFindAndModify: false,
    useCreateIndex: true
}, async (err) => {
    if (err) {
        console.log(err)
    } else {
        console.log('Connect database successfully!')
    }
});
// console.log(mongoose.connection)
mongoose.Promise = global.Promise;
var db = mongoose.connection;
// console.log(db)
db.on('error', console.error.bind(console, 'MongoDB connection error:'));
```

---
###

### *2.Mongo model*
[menu](#Table-snippets)

#### Prefix
```
!mongoModel
```

#### Table variables

|  STT  | Default / Choose type               | Description           |
| :---: | ----------------------------------- | --------------------- |
|   1   | schemaName                          | Schema var            |
|   2   | attribute                           | Attribute             |
|   3   | (String,Date,Number,Boolean, Array) | Type of attribute     |
|   4   | ( , required.true)                  | Required of attribute |
|   5   | model                               | Model name            |

#### Code generate

``` Javascript
const mongoose = require('mongoose');
            
mongoose.Promise = global.Promise;

const ${1:schemaName} = new mongoose.Schema({
    ${2:attribute}: { type: ${3|String,Date,Number,Boolean,Array|} , ${4| ,required:true|} },
}, { timestamps: { createdAt: 'created_at', updatedAt: 'updated_at' } });

const ${5:model} = mongoose.model('user', ${1:schemaName});

module.exports = ${5:model};
```

---
###

### *3.Mongo model field*
[menu](#Table-snippets)

#### Prefix
```
!mongoModelField
```

#### Table variables

|  STT  | Default / Choose type              | Description          |
| :---: | ---------------------------------- | -------------------- |
|   1   | attribue                           | Model attribute      |
|   2   | (String,Date,Number,Boolean,Array) | Type of attribue     |
|   3   | ( , required:true)                 | Required of attribue |

#### Code generate

``` Javascript
${1:attribute}: { type: ${2|String,Date,Number,Boolean,Array|} , ${3| ,required:true|} },
```

---
###

### *4.Mongo db find*
[menu](#Table-snippets)

#### Prefix
```
!mongoFind
```

#### Table variables

|  STT  | Default / Choose type        | Description                         |
| :---: | ---------------------------- | ----------------------------------- |
|   1   | model                        | Model                               |
|   2   | ( ,{})                       | Finding condition                   |
|   3   | ( ,'-attr1 -attr2', ex_attr) | Attribute exclude in finding result |
|   4   | ( ,{skip:10, limit:10})      | Pagination                          |

#### Code generate

``` Javascript
await ${1:model}.find(${2| ,{}|}, ${3| ,'-attr1 -attr2', ex_attr |}, ${4| ,{ skip: 10 , limit: 10}|}).exec();,

```

---
###

### *5.Mongo db find one*
[menu](#Table-snippets)

#### Prefix
```
!mongoFindOne
```

#### Table variables

|  STT  | Default / Choose type        | Description         |
| :---: | ---------------------------- | ------------------- |
|   1   | model                        | Model               |
|   2   | ( , {})                      | Condition           |
|   3   | ( ,'-attr1 -attr2', ex_attr) | exclude field model |


#### Code generate

``` Javascript
await ${1:model}.findOne(${2| ,{}|}, ${3| ,'-attr1 -attr2', ex_attr |}).exec();
```

---
###

### *6.Mongo db find by id*
[menu](#Table-snippets)

#### Prefix
```
!mongoFindById
```

#### Table variables

|  STT  | Default / Choose type        | Description         |
| :---: | ---------------------------- | ------------------- |
|   1   | model                        | Model               |
|   2   | id                           | Id object           |
|   3   | ( ,'-attr1 -attr2', ex_attr) | exclude field model |


#### Code generate

``` Javascript
await ${1:model}.findById(${2:id}, ${3| ,'-attr1 -attr2', ex_attr |}).exec();

```

---
###

### *7.Mongo db create*
[menu](#Table-snippets)

#### Prefix
```
!mongoCreate
```

#### Table variables

|  STT  | Default / Choose type | Description  |
| :---: | --------------------- | ------------ |
|   1   | Model                 | Model        |
|   2   | ( ,{},[])             | Create value |

#### Code generate

``` Javascript
await ${1:Model}.create(${2| ,{ },[]|});
```

---
###

### *8.Mongo db exclude*
[menu](#Table-snippets)

#### Prefix
```
!mongoExclude
```

#### Code generate

``` Javascript
let ex_attr = '-__v -created_at -updated_at';

```

---
###

### *9.Mongo db ref*
[menu](#Table-snippets)

#### Prefix
```
!mongoRefField
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | table                 | Table name  |

#### Code generate

``` Javascript
{
    type: Schema.Types.ObjectId,
    ref: '${1:table}'
},
```

---
###

### *10.Mongo db regExp*
[menu](#Table-snippets)

#### Prefix
```
!mongoRegExp
```

#### Code generate

``` Javascript
{ $regex: $1 }
```

---
###

### *11.Mongo db populate line*
[menu](#Table-snippets)

#### Prefix
```
!mongoPopulateLine
```

#### Table variables

|  STT  | Default / Choose type | Description           |
| :---: | --------------------- | --------------------- |
|   1   | attribute             | Attribute to populate |

#### Code generate

``` Javascript
.populate('${1:attribute}', ex_attr )
```

---
###

### *12.Mongo db populate obj*
[menu](#Table-snippets)

#### Prefix
```
!mongoPopulateObj
```

#### Table variables

|  STT  | Default / Choose type | Description         |
| :---: | --------------------- | ------------------- |
|   1   | path1                 | Path field 1        |
|   2   | path2                 | Child path populate |

#### Code generate

``` Javascript
{
    path: '${1:path1}',
    populate: { path: '${2:path2}', select: ex_attr },
    select: ex_attr 
}
```

---
###