This guideline describes how to implement the API interface for API communication between Omniscient-Cloud and your services. Please follow the interface for simplifying and speeding the programming.

#Get Access Token
[Method] POST/GET
[URL] https://xxx.com/OmniSegment/token/

## Field:
|**Field**|**Data type**|** Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
| apikey | string | **v**||Provided by Omniscient-Cloud|

## Example:

```
[Sample - Success]
{
 "status": "ok",
 "message": "",
 "data": {
 "token":
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcGlrZXk......."
 }
}
[Sample - failure]
{
 "status": "error",
 "message": "錯誤訊息",
 "data": null
}
```



#Get member data
[Method] POST
[URL] https://xxx.com/OmniSegment/getMember/



## Header Field
|**Field**|**Data Type**|**Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
| token | string | **v**|Get from token api|Access token|


## Field

|**Field**|**Data Type**|**Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
| token | string | **v**|Get from token api|Access token|


## Example:

```
[Sample - Success]
{
 "status": "ok",
 "message": "",
 "data": {
 "token":
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcGlrZXk......."
 }
}
[Sample - failure]
{
 "status": "error",
 "message": "錯誤訊息",
 "data": null
}
```