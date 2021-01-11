This guideline describes how to implement the API interface for API communication between Omniscient-Cloud and your services. Please follow the interface for simplifying and speeding the programming.

#Get Access Token
[Method] POST/GET
[URL] https://xxx.com/OmniSegment/token/

## Fields:
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



## Header Fields
|**Field**|**Data Type**|**Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
| token | string | **v**|Get from token api|Access token|


## Fields

|**Field**|**Data Type**|**Required**|**Default**|**Note**|
| :------: | ------ | ------ | ------ | ------ | 
|sdate| string| |當日日期 |異動日-起 (yyyy/MM/dd)|
|edate| string| |當日日期 |異動日-迄 (yyyy/MM/dd)|
|member_sn| string| | |會員編號|

## Respond Fields

|**Field**|**Data Type**|**Note**|
| :------: | ------ | ------ |  
|status| string| ok/error|
|message| string|Return message|
|data| json object||

## Respond Data Object Fields

|**Field**|**Data Type**|**Note**|
| :------: | ------ | ------ |  
|sdate| string|異動日-起 (yyyy/MM/dd)|
|edate |string |異動日-迄 (yyyy/MM/dd)|
|member_sn| string| 會員編號(單筆查詢顯示)|
|count |integer |資料筆數|
|members |string |JSON Array encrypted by JWT, JWT Secret provided by Omniscient-Cloud \n Example: \n import jwt\n  jwt.encode(  {"some": "payload"}, "secret",   algorithm="HS256",) |


## Respond Data Members Array Fields

|**Field**|**Data Type**|**Note**|
| :------: | ------ | ------ |  
|member_sn| string| 會員編號|
|name |string |姓名 (null=無)|
|email| string |Email|
|phone |string |手機 (null=無)|
|member_level| string| 會員等級|
|sex |string|男: male,女: female|
|birthday| string| 生日 (null=無)|
|register_date| string |註冊日期|
|is_subscriber| string |是否訂閱電子報|

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


## Decrypted Example:

```
[Sample - failure]

{
   "status":"error",
   "message":"錯誤訊息",
   "data":null
}
[members - 解密後的格式]

members:[
   {
      "member_sn":671243,
      "name":"test",
      "email":"test@gmail.com",
      "phone":"+886987654321",
      "member_level":0,
      "sex":"male",
      "birthday":"2000-01-01",
      "register_date":"2016-06-30",
      "is_subscriber":false
   },
   {
      "member_sn":99999,
      "name":"test2",
      "email":"test2@gmail.com",
      "phone":"+886987654322",
      "member_level":0,
      "sex":"male",
      "birthday":"2000-01-01",
      "register_date":"2016-06-30",
      "is_subscriber":false
   }
]
```