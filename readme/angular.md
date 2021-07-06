## Table snippets
|  STT  | Snippets              | Link                            |
| :---: | :-------------------- | :------------------------------ |
|   1   | Angular service       | [link](#1Angular-service)       |
|   1   | Angular cookie helper | [link](#2Angular-cookie-helper) |
|   1   | Angular cookie helper | [link](#3Angular-url-helper) |

### *1.Angular service*

#### Prefix
```
!angService
```

#### Table variables

|  STT  | Default / Choose type | Description    |
| :---: | --------------------- | -------------- |
|   1   |                       | Path api       |
|   2   |                       | End points api |

#### Code generate

``` Typescript
path: string = '$1';
            
endpoints = {
    $2
};
            
constructor(private _api: ApiService) { }
```
###

### *2.Angular cookie helper*

#### Prefix
```
!angCookie
```

#### Code generate

``` Typescript
/**
* Get cookie by key
*
* @export
* @param {*} key
* @returns
*/
export function get(key) {
    let cookies = document.cookie;
    let array = cookies.split(';').filter(
        str => {
            let arr = str.trim().split('=');
            return arr[0] == key;
        });
    if (!array || array.length <= 0) {
        return '';
    }
    return decodeURIComponent(array[0].trim().split('=')[1]);

}
/**
* Set cookie with key = value;expires=times
*
* @export
* @param {*} name
* @param {*} value
* @param {number} [seconds=0]
*/
export function set(name, value, seconds = 0) {
    let cookie = `${name}=${encodeURIComponent(value)}`;
    let expires = (seconds) ? `; expires=${seconds.toString()}` : '';
    let path = `; path =/`;
    document.cookie = (`${cookie}${expires}${path}`);
}

/**
* Remove cookie by key
*
* @export
* @param {*} key
*/
export function remove(key) {
    document.cookie = `${key}=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;`
}
```

---
###

### *3.Angular url helper*

#### Prefix
```
!angUrlHelper
```

#### Code generate

``` Typescript
/**
* Object to Query String
*
* @export
* @param {*} [params={}]
* @returns
*/
export function query(params: any = {}) {
    if (params && Object.keys(params).length > 0) {
        return `?${Object.keys(params).filter(key => {
            return (params[key] && params[key] != 'null');
        }).map(key => {
            return [key, encodeURIComponent(params[key])].join('=');
        }).join('&')}`;
    } else {
        return '';
    }
}

/**
* return url: domain/path/endpoint?query
*
* @export
* @param {*} domain
* @param {*} path
* @param {*} endpoint
* @param {*} [queryParams=null]
* @returns
*/
export function merge(domain, path, endpoint, queryParams = null) {
    if (path) {
        return `${domain}/${path}/${endpoint}${query(queryParams)}`;
    } else {
        return `${domain}/${endpoint}${query(queryParams)}`;
    }
}
```

---
###