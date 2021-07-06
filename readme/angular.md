## Table snippets
|  STT  | Snippets                      | Link                                     |
| :---: | :---------------------------- | :--------------------------------------- |
|   1   | Angular service               | [link](#1Angular-service)                |
|   2   | Angular cookie helper         | [link](#2Angular-cookie-helper)          |
|   3   | Angular url helper            | [link](#3Angular-url-helper)             |
|   4   | Angular service api           | [link](#4Angular-service-api)            |
|   5   | Angular dialog service        | [link](#5Angular-dialog-service)         |
|   6   | Angular RespnseData interface | [link](#6Angular-ResponseData-interface) |
|   7   | Angular Pagination interface  | [link](#7Angular-Pagination-interface)   |


### *1.Angular service*
[menu](#Table-snippets)

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
[menu](#Table-snippets)

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
[menu](#Table-snippets)

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

### *4.Angular service api*
[menu](#Table-snippets)

#### Prefix
```
!angApiService
```

#### Code generate

``` Typescript

apiServer: string = environment.apiServer;
constructor(private http: HttpClient) { }
            
/**
* REQUEST API
* METHOD POST
*
* @param {string} path
* @param {string} endpoint
* @param {*} [data={}]
* @returns {Observable<any>}
* @memberof ApiService
*/
get(path: string, endpoint: string, data: any = {}) {
    return this.http.get(url.merge(this.apiServer, path, endpoint, data));
}
/**
* 
* REQUEST API
* METHOD DELETE
* 
* @param {string} path
* @param {string} endpoint
* @param {*} [data={}]
* @returns {Observable<any>}
* @memberof ApiService
* 
* 
*/

delete(path: string, endpoint: string, data: any = {}) {
    return this.http.delete(url.merge(this.apiServer, path, endpoint, data));
}

/**
* REQUEST API
* METHOD POST
*
* @param {string} path
* @param {string} endpoint
* @param {*} [data={}]
* @param {*} [options={}]
* @returns
* @memberof ApiService
*/
post(path: string, endpoint: string, data: any = {}, options: any = null) :Observable<any>{
    let httpOptions;
    if (!options || options.type != 'multipart/form-data') {
        httpOptions = {
            headers: new HttpHeaders({
                'Content-Type': (options && options.type) ? options.type : 'application/json'
            }),
            responseType: 'json'
        };
    } else {
        httpOptions = {
            headers: new HttpHeaders({}),
            responseType: 'json'
        };
    }
    return this.http.post(url.merge(this.apiServer, path, endpoint), data, httpOptions);
}

/**
* REQUEST API
* METHOD PUT
* @param {string} path
* @param {string} endpoint
* @param {*} data
* @param {*} [options]
* @returns {Observable<any>}
* @memberof ApiService
*/
put(path: string, endpoint: string, data: any, options?: any): Observable<any> {
    const httpOptions = {
        headers: new HttpHeaders({
            'Content-Type': (options && options.type) ? options.type : 'application/json',
        })
    };
    return this.http.put(url.merge(this.apiServer, path, endpoint), data, httpOptions);
}

/**
* REQUEST API FOR FILE DATA
* METHOD POST
* @param {string} path
* @param {string} endpoint
* @param {*} data
* @param {*} options
* @returns {Observable<any>}
* @memberof ApiService
*/
file(path: string, endpoint: string, data: any, options: any): Observable<any> {
    return this.http.post(url.merge(this.apiServer, path, endpoint), data, options);
}
/**
* Convert json to urlencoded
* 
* @static
* @param {*} data
* @returns
* @memberof ApiService
*/
public static convertToFormUrlencoded(data) {
    return Object.keys(data).map(key => {
        return key + '=' + encodeURIComponent(data[key]);
        }).join('&');
}

/**
* Convert json to query string
*
* @static
* @param {string} url
* @param {*} data
* @returns
* @memberof ApiService
*/
public static convertToQueryString(url: string, data: any) {
    const query = Object.keys(data).map(key => key + '=' + encodeURIComponent(data[key])).join('&');
    return url + '?' + query;
}
```

---
###

### *5.Angular dialog service*
[menu](#Table-snippets)

#### Prefix
```
!angDlogService
```

#### Code generate

``` Typescript

export interface option {
    class?: string,
    initialState?: any,
}
            
@Injectable({
    providedIn: 'root'
})
export class DialogService {
    modalRef: BsModalRef;
    constructor(private modalService: BsModalService) { }
            
    // Bootstrap Dialog
    openModal(template: any, data: option = null) {
        this.modalRef = this.modalService.show(template, data);
    }
            
    hideModal() {
        this.modalRef.hide();
    }
}
```

---
###

### *6.Angular ResponseData interface*
[menu](#Table-snippets)

#### Prefix
```
!angResponseInter
```

#### Code generate

``` Typescript

export interface ResponseData {
    meta?: {
        current_page: number
        num_pages: number
        num_per_page: number
        total: number
    },
    data?: Array<any>,
    value?: any,
    messages?: string
}
```

---
###

### *7.Angular Pagination interface*
[menu](#Table-snippets)

#### Prefix
```
!angPageInter
```

#### Code generate

``` Typescript

export interface PaginationOption {
    total: number,
    num_pages: number,
    current_page: number,
    num_per_page: number
}
```

---
###

### *8.Angular modal component*
[menu](#Table-snippets)

#### Prefix
```
!angModalCom
```

#### Table variables

#### Code generate

``` Javascript

```

---
###