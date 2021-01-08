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
|sdate| string| |當日日期 |異動日-起 (yyyy/MM/dd)|
|edate| string| |當日日期 |異動日-迄 (yyyy/MM/dd)|
|member_sn| string| | |會員編號|

## Respond Field

|**Field**|**Data Type**|**Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
|sdate| string| |當日日期 |異動日-起 (yyyy/MM/dd)|
|edate| string| |當日日期 |異動日-迄 (yyyy/MM/dd)|
|member_sn| string| | |會員編號|

## Example:

```
[區間查詢回應欄位][Sample - Success]

{
   "status":"ok",
   "message":"",
   "data":{
      "sdate":"2020/10/04",
      "edate":"2020/10/04",
      "count":112,
      "members":"SG2gy6s8C9G0Kz45C............................"
   }
}
[會員編號查詢回應欄位][Sample - Success]{
   "status":"ok",
   "message":"",
   "data":{
      "sdate":"2020/10/04",
      "edate":"2020/10/04",
      "member_sn":12345,
      "count":1,
      "members":"SG2gy6s8C9G0Kz45C............................"
   }
}
```