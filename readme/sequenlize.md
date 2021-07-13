## Table snippets
|  STT  | Snippets                | Link                             |
| :---: | :---------------------- | :------------------------------- |
|   1   | Sequenlize config       | [link](#1Sequenlize-config)      |
|   2   | Sequenlize MySQL config | [link](#2Sequenlie-mysql-config) |
|   3   | Sequenlize model        | [link](#3Sequenlize-model)       |
|   4   | Sequenlize model field  | [link](#4Sequenlize-model-field) |
|   5   | Sequenlize finding      | [link](#5Sequenlize-finding)     |
|   6   | Sequenlize delete       | [link](#6Sequenlize-delete)      |
|   7   | Sequenlize create       | [link](#7Sequenlize-create)      |
|   8   | Sequenlize op           | [link](#8Sequenlize-op)          |


### *1.Sequenlize config*
[menu](#Table-snippets)

#### Prefix
```
!seqConfig
```

#### Code generate

``` Javascript
const dbConfig = require("./Db-config");
            
const Sequelize = require("sequelize");
            
const sequelize = new Sequelize(dbConfig.DB, dbConfig.USER, dbConfig.PASSWORD, {,
    host: dbConfig.HOST,
    dialect: dbConfig.dialect,
    operatorsAliases: false,
    logging: false,
    pool: {
        max: dbConfig.pool.max,
        min: dbConfig.pool.min,
        acquire: dbConfig.pool.acquire,
        idle: dbConfig.pool.idle
    }
});
            
module.exports = sequelize;
```

---
###


### *2.Sequenlie mysql config*
[menu](#Table-snippets)

#### Prefix
```
!seqMSQLConfig
```

#### Table variables

|  STT  | Default / Choose type | Description           |
| :---: | --------------------- | --------------------- |
|   1   | localhost             | Mysql host            |
|   2   | root                  | user                  |
|   3   | root                  | password              |
|   4   | dbname                | Database name connect |

#### Code generate

``` Javascript
// MySQL configuration
module.exports = {
   HOST: "${1:localhost}",
   USER: "${2:root}",
   PASSWORD: "${3:root}",
   DB: "${4:dbname}",
   dialect: "mysql",
   pool: {       max: 5,
       min: 0,
       acquire: 30000,
       idle: 10000
   }
};
```

---
###

### *3.Sequenlize model*
[menu](#Table-snippets)

#### Prefix
```
!seqModel
```

#### Table variables

|  STT  | Default / Choose type         | Description         |
| :---: | ----------------------------- | ------------------- |
|   1   | DBModel                       | Model               |
|   2   | tablename                     | Table name          |
|   3   | mapField1                     | Field model         |
|   4   | (INTEGER,STRING,DATE,BOOLEAN) | Type of model field |
|   5   | attribute1                    | Field of table      |

#### Code generate

``` Javascript
const { Sequelize, DataTypes, DATE } = require('sequelize');

const sequelize = require("../configurations/Squelize-config");

const ${1:DBModel} = sequelize.define(${2:tablename}, {
    ${3:mapField1}: { type: DataTypes.${4|INTEGER,STRING,DATE,BOOLEAN|}, autoIncrement: true, primaryKey: true, field: '${5:attribute1}' },
}, {
    timestamps: false,
    freezeTableName: true
});

module.exports =  ${1:DBModel};
```

---
###

### *4.Sequenlize model field*
[menu](#Table-snippets)

#### Prefix
```
!seqModelField
```

#### Table variables

|  STT  | Default / Choose type         | Description    |
| :---: | ----------------------------- | -------------- |
|   1   | field                         | Field of model |
|   2   | (INTEGER,STRING,DATE,BOOLEAN) | Type of field  |
|   3   | attribute                     | Table field    |

#### Code generate

``` Javascript
${1:field}: { type: DataTypes.${2|INTEGER,STRING,DATE,BOOLEAN|}, field: '${3:attribute}' },

```

---
###

### *5.Sequenlize finding*
[menu](#Table-snippets)

#### Prefix
```
!seqFinding
```

#### Table variables

|  STT  | Default / Choose type                                   | Description                |
| :---: | ------------------------------------------------------- | -------------------------- |
|   1   | data                                                    | Data result                |
|   2   | model                                                   | Model                      |
|   3   | (findAll,findByPk,findOne,findOrCreate,findAndCountAll) | Function for model finding |
|   4   |                                                         | Condition                  |

#### Code generate

``` Javascript
let ${1:data} = await ${2:model}.${3|findAll,findByPk,findOne,findOrCreate,findAndCountAll|}($4);

```

---
###

### *6.Sequenlize delete*
[menu](#Table-snippets)

#### Prefix
```
!seqDelete
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | model                 | Model obj   |
|   2   |                       | Type more   |

#### Code generate

``` Javascript
await  ${1:model}.destroy($2)
```

---
###

### *7.Sequenlize create*
[menu](#Table-snippets)

#### Prefix
```
!seqCreate
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | model                 | Model       |
|   2   |                       | Type more   |

#### Code generate

``` Javascript
await  ${1:model}.create($2)
```

---
###

### *8.Sequenlize op*
[menu](#Table-snippets)

#### Prefix
```
!seqOp
```

#### Table variables

|  STT  | Default / Choose type                                        | Description |
| :---: | ------------------------------------------------------------ | ----------- |
|   1   | (eq,ne,and,or,gt,gte,lt,lte,between,notBetween,like,notLike) | Option      |
|   2   | sth                                                          | value       |


#### Code generate

``` Javascript
[Op.${1|eq,ne,and,or,gt,gte,lt,lte,between,notBetween,like,notLike|}] = ${2:sth}
```

---
###
