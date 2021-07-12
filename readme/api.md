## Table snippets
|  STT  | Snippets                    | Link                                  |
| :---: | :-------------------------- | :------------------------------------ |
|   1   | Express app.js              | [link](#1Express-appjs)               |
|   2   | Express server.js           | [link](#2Express-serverjs)            |
|   3   | Express Function Controller | [link](#3Express-function-controller) |


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