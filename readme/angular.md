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
|   8   | Angular Modal Component       | [link](#8Angular-modal-component)        |
|   9   | Angular service function      | [link](#9Angular-service-function)       |
|  10   | Angular form object           | [link](#10Angular-form-object)           |
|  11   | Angular routing layout        | [link](#11Angular-route-layout)          |
|  12   | Angular routing common        | [link](#12Angular-route-common)          |
|  13   | Angular routing component     | [link](#13Angular-route-component)       |
|  14   | Angular routing module        | [link](#14Angular-route-module)          |
|  15   | Angular ngFor                 | [link](#15Angular-ngFor)                 |
|  16   | Angular ngIf                  | [link](#16Angular-ngIf)                  |
|  17   | Angular ngClass               | [link](#17Angular-ngClass)               |
|  18   | Angular ngStyle               | [link](#18Angular-ngStyle)               |
|  19   | Angular router link           | [link](#19Angular-router-link)           |
|  20   | Angular attribute             | [link](#20Angular-attribute)             |
|  21   | Angular formgroup             | [link](#21Angular-formgroup)             |
|  22   | Angular form control name     | [link](#22Angular-formcontrol-name)      |
|  23   | Angular pipe                  | [link](#23Angular-pipe)                  |
|  24   | Angular router link active    | [link](#24Angular-router-link-active)    |
|  25   | Angular modal html            | [link](#25Angular-modal-html)            |
|  26   | Angular pagination option     | [link](#26Angular-pagination-option)     |
|  27   | Angular using modal           | [link](#27Angular-using-modal)           |
|  28   | Angular template pagination   | [link](#28Angular-template-pagination)   |
|  29   | Angular jwt interceptor       | [link](#29Angular-jwt-interceptor)       |
|  30   | Angular error interceptor     | [link](#30Angular-error-interceptor)     |
|  31   | Angular import main module    | [link](#31Angular-import-module)         |
|  32   | Angular input var             | [link](#32Angular-input-var)             |
|  33   | Angular ouput var             | [link](#33Angular-output-var)            |


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

|  STT  | Default / Choose type | Description   |
| :---: | --------------------- | ------------- |
|   1   | any                   | Type of value |
|   2   | service               | Service var   |
|   3   | Service               | Service class |

#### Code generate

``` Typescript
 
value: ${1:any};
            
submitCall: any;

constructor(
    private bsModalRef: BsModalRef,
    private _${2:service}: ${3:Service}
) { }

closeModal() {
    this.bsModalRef.hide();
}
```

---
###

### *9.Angular service function*
[menu](#Table-snippets)

#### Prefix
```
!angServiceFnct
```

#### Table variables

|  STT  | Default / Choose type      | Description         |
| :---: | -------------------------- | ------------------- |
|   1   | functionname               | Function name       |
|   2   |                            | Variables functions |
|   3   | (get,delete,post,put,file) | Http method         |
|   4   | name                       | End point           |
|   5   |                            | Data post if need   |

#### Code generate

``` Typescript
${1:functcionname}($2}) {
    return this._api.${3|get,delete,post,put,file|}(this.path, this.endpoints.${4:name}$5);
}
```

---
###

### *10.Angular form object*
[menu](#Table-snippets)

#### Prefix
```
!angFormObj
```

#### Table variables

|  STT  | Default / Choose type  | Description        |
| :---: | ---------------------- | ------------------ |
|   1   | nameForm               | Form variable      |
|   2   | control1               | Form control field |
|   3   | ( ,'')                 | Default value      |
|   4   | ( ,Validator.required) | Validators field   |

#### Code generate

``` Typescript
${1:nameForm}: FormGroup = new FormGroup({
    ${2:control1}: new FormControl(${3| ,''|},${4| ,Validators.required|}),
});
```
---
###

### *11.Angular route layout*
[menu](#Table-snippets)

#### Prefix
```
!angRouteLayout
```

#### Table variables

|  STT  | Default / Choose type | Description                          |
| :---: | --------------------- | ------------------------------------ |
|   1   | component1            | Component view layout                |
|   2   | component2            | Child component layout               |
|   3   | path1                 | Path routing for child layout        |
|   4   | path2                 | Path routing for child module layout |
|   5   | module                | Path to module                       |
|   6   | module                | Module to import                     |

#### Code generate

``` Typescript
import { RouterModule, Routes } from '@angular/router';
const routes: Routes = [
    {
        path: '',
        component: ${1:component1},
        children: [
            {
                path: '',
                pathMatch: 'full',
                component: ${2:component2}
            },
            {
                path: '${3:path1}',
                component: ${2:component2}
            },
            {
                path: '${4:path2}',
                loadChildren: () => import('${5:module}').then(m => m.${6:module})
            },
            {
                path: '**',
                redirectTo: '${3:path1}'
            }
        ]
    }
]
```

---
###

### *12.Angular route common*
[menu](#Table-snippets)

#### Prefix
```
!angRouteCommon
```

#### Table variables

|  STT  | Default / Choose type | Description        |
| :---: | --------------------- | ------------------ |
|   1   | component1            | Component 1 layout |
|   2   | path1                 | Path rout child    |
|   3   | component2            | Component 2        |


#### Code generate

``` Typescript
import { RouterModule, Routes } from '@angular/router';
const routes: Routes = [
    {
        path: '',
        component: ${1:component1}
    },
    {
        path: '${2:path1}',
        component: ${3:component2}
    }
]
```

---
###

### *13.Angular route component*
[menu](#Table-snippets)

#### Prefix
```
!angRouteComponent
```

#### Table variables

|  STT  | Default / Choose type | Description       |
| :---: | --------------------- | ----------------- |
|   1   | path                  | Path routing      |
|   2   | component             | Component routing |

#### Code generate

``` Typescript
{
    path: '${1:path}',
    component: ${2:component}
}
```

---
###

### *14.Angular route module*
[menu](#Table-snippets)

#### Prefix
```
!angRouteModule
```

#### Table variables

|  STT  | Default / Choose type | Description      |
| :---: | --------------------- | ---------------- |
|   1   | path                  | Path to module   |
|   2   | module                | Module to import |
|   3   | module                | Module           |

#### Code generate

``` Typescript
{
    path: '${1:path}',
    loadChildren: () => import('${2:module}').then(m => m.${3:module})
},
```

---
###

### *15.Angular ngFor*
[menu](#Table-snippets)

#### Prefix
```
!angNgFor
```

#### Table variables

|  STT  | Default / Choose type | Description   |
| :---: | --------------------- | ------------- |
|   1   | item                  | Item in array |
|   2   | items                 | Array         |
|   3   | i                     | index         |

#### Code generate

``` Typescript
*ngFor="let ${1:item} of ${2:items}; index as ${3:i};"
```

---
###

### *16.Angular ngIf*
[menu](#Table-snippets)

#### Prefix
```
!angNgIf
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | condition             | Condition   |

#### Code generate

``` Typescript
*ngIf="${1:condition}"
```

---
###

### *17.Angular ngClass*
[menu](#Table-snippets)

#### Prefix
```
!angNgClass
```

#### Table variables

|  STT  | Default / Choose type | Description         |
| :---: | --------------------- | ------------------- |
|   1   | class1                | Style class         |
|   2   | condition             | Condition for class |
|   3   | class2                | Style class         |
|   4   | condition             | Condition for class |

#### Code generate

``` Typescript
[ngClass]="{'${1:class1}': ${2:condition}, '${3:class2}':  ${4:condition} }"
```

---
###

### *18.Angular ngStyle*
[menu](#Table-snippets)

#### Prefix
```
!angNgStyle
```

#### Table variables

|  STT  | Default / Choose type | Description         |
| :---: | --------------------- | ------------------- |
|   1   | attr1                 | Attribute style     |
|   2   | condition             | Condition for style |
|   3   | op1                   | Option 1 condition  |
|   4   | op2                   | Option 2 condtion   |

#### Code generate

``` Typescript
[ngStyle]="{${1:attr1}: ${2:condition}? ${3:op1}: ${4:op2}}"
```

---
###

### *19.Angular router link*
[menu](#Table-snippets)

#### Prefix
```
!angRouterLink
```

#### Table variables

|  STT  | Default / Choose type | Description   |
| :---: | --------------------- | ------------- |
|   1   | route                 | Routing link  |
|   2   | param1                | Param routing |

#### Code generate

``` Javascript
[routerLink]="['${1:route}',${2:param1}]"
```

---
###

### *20.Angular attribute*
[menu](#Table-snippets)

#### Prefix
```
!angAttr
```

#### Table variables

|  STT  | Default / Choose type | Description     |
| :---: | --------------------- | --------------- |
|   1   | attributename         | Attribute name  |
|   2   | value                 | Value attribute |

#### Code generate

``` Typescript
[attr.${1:attributename}]="${2:value}"
```

---
###

### *21.Angular formgroup*
[menu](#Table-snippets)

#### Prefix
```
!angFormGroup
```

#### Table variables

|  STT  | Default / Choose type | Description     |
| :---: | --------------------- | --------------- |
|   1   | formname              | Form group name |

#### Code generate

``` Typescript
[formGroup]="${1:formname}"
```

---
###

### *22.Angular formcontrol name*
[menu](#Table-snippets)

#### Prefix
```
!angFormControl
```

#### Table variables

|  STT  | Default / Choose type | Description       |
| :---: | --------------------- | ----------------- |
|   1   | name                  | Form control name |

#### Code generate

``` Typescript
formControlName="${1:name}"
```

---
###

### *23.Angular pipe*
[menu](#Table-snippets)

#### Prefix
```
!angPipe
```

#### Table variables

|  STT  | Default / Choose type | Description |
| :---: | --------------------- | ----------- |
|   1   | value                 | Value       |
|   2   | translate             | Pipe value  |

#### Code generate

``` Typescript
{{${1:value}|${2:translate}}}
```

---
###

### *24.Angular router link active*
[menu](#Table-snippets)

#### Prefix
```
!angRouteActive
```

#### Table variables

|  STT  | Default / Choose type | Description              |
| :---: | --------------------- | ------------------------ |
|   1   | active                | Active class for routing |

#### Code generate

``` Typescript
routerLinkActive="${1:active}"
```

---
###

### *25.Angular modal html*
[menu](#Table-snippets)

#### Prefix
```
!angModalHtml
```

#### Code generate

``` Html
<div class="modal-header">
    <button (click)="closeModal()" type="button" class="close" data-dismiss="modal" aria-label="Close">
        <span aria-hidden="true">×</span>
    </button>
    <h4 class="modal-title">
        $1
    </h4>
</div>
<div class="modal-body">
    $2 
</div>
<div class="modal-footer">
    <button (click)="closeModal()" type="button" class="btn btn-default" data-dismiss="modal">Close</button>
</div>
```

---
###

### *26.Angular pagination option*
[menu](#Table-snippets)

#### Prefix
```
!angPaginationOption
```

#### Code generate

``` Typescript
paginationOption: PaginationOption = {
    current_page: 1,
    num_pages: 10,
    num_per_page: 10,
    total: 1000
};
handleChangePage(data: PaginationOption){}
```

---
###

### *27.Angular using modal*
[menu](#Table-snippets)

#### Prefix
```
!angUseModal
```

#### Table variables

|  STT  | Default / Choose type | Description           |
| :---: | --------------------- | --------------------- |
|   1   | Component             | Modal component       |
|   2   |                       | Place to inital state |

#### Code generate

``` Typescript
this._modal.openModal(${1:Component}, {initialState: {$2}});
```

---
###

### *28.Angular template pagination*
[menu](#Table-snippets)

#### Prefix
```
!angPageTemplate
```

#### Code generate

``` Html
<app-pagination [paginationOption]="paginationOption" (onPageChange)="handleChangePage($event)">
```

---
###

### *29.Angular jwt interceptor*
[menu](#Table-snippets)

#### Prefix
```
!angJwtInterceptor
```

#### Code generate

``` Typescript
exclude: Array<string> = ['auth/login', 'auth/refresh'];
constructor(
    // private authService: AuthService,
    private jwtService: JwtService,
    private router: Router
) { }

intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {

    if (this.exclude.filter(path => request.url.indexOf(path) > -1).length == 0) {
        if (this.jwtService.getCookieToken("accessToken")) {
            if (request.headers.has('Content-Type')) {
                request = request.clone({
                    headers: new HttpHeaders({
                        'x-access-token': this.jwtService.getToken(),
                        'Content-Type': request.headers.get('Content-Type'),
                    })
                });
            }else{
                request = request.clone({
                    headers: new HttpHeaders({
                        'x-access-token': this.jwtService.getToken(),
                    })
                });
            }
        }
    }
    return next.handle(request);
}
```

---
###

### *30.Angular error interceptor*
[menu](#Table-snippets)

#### Prefix
```
!angErrorInterceptor
```

#### Code generate

``` Typescript
constructor(
    private router: Router,
    private _jwt: JwtService,
    private _auth: AuthService,
) { }
            
intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    return next.handle(request).pipe(
        retry(0),
        catchError((error)=> {
            
            if(error.status == 401 ) {
                if(this._jwt.getCookieToken("refreshToken")){
                    let data = { refreshToken: this._jwt.refreshToken }
            
                        this._auth.refresh(data).subscribe(
                            res =>{
                                this.router.navigate(['/']);
                            }, err =>{
                                this._jwt.removeToken("accessToken");
                            this._jwt.removeToken("refreshToken");
                                this.router.navigate(['sign-in']);
                            }
                        );
                }else{
                    this.router.navigate(['sign-in']);
                }
            }else if(error.status == 403) {
                this.router.navigate(['home']);
            }
            return throwError(error.error);
        })
    );
}
```

---
###

### *31.Angular import module*
[menu](#Table-snippets)

#### Prefix
```
!angImportModule
```

#### Code generate

``` Typescript
HttpClientModule,
ReactiveFormsModule,
```

---
###

### *32.Angular input var*
[menu](#Table-snippets)

#### Prefix
```
!ang@Input
```

#### Table variables

|  STT  | Default / Choose type | Description            |
| :---: | --------------------- | ---------------------- |
|   1   | var                   | Variable input         |
|   2   | type                  | Type of input variable |

#### Code generate

``` Typescript
@Input() ${1:var}: ${2:type};
```

---
###

### *33.Angular output var*
[menu](#Table-snippets)

#### Prefix
```
!ang@Output
```

#### Table variables

|  STT  | Default / Choose type | Description        |
| :---: | --------------------- | ------------------ |
|   1   | var                   | Variable of output |

#### Code generate

``` Typescript
@Output() ${1:var}: EventEmitter<any> = new EventEmitter();
```

---
###