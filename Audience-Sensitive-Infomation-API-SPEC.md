
## 場景：請客戶提供 api endpoint 供 OmniSegment 索取多個 audience 的 email or sms 資料



## Request

### HTTP Method
* `POST`

### Headers
```
X-OmniSegment-ASI-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
> Provided by the customer.

### Body

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| member_sn | member_sn list | **`"member_sn": ["sn1", "sn2", ...]`** | list | &#10004; | |
| fields | Ｗe want to obtain the keys from the response. | **`"fields": ["email", "phone", ...]`** | list | &#10004; | |

### Example
```
curl --location --request POST '<your api endpoint>' \
--header 'X-OmniSegment-ASI-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--header 'Content-Type': 'application/json' \
--data-raw '{
   "member_sn": [
       "sn1",
       "sn2",
       "sn3",
       ...
   ],
   "fields": ["email", "phone", "is_subscriber_email", ...]
}'
```

## Response

### Success 

#### status_code: 200

| **Parameter** | **Description** | **Data Type** | **Required** | Note |
| -------- | -------- | -------- | -------- | ------ |
| member_sn     | memeber_sn     | string     | &#10004; | |
| email     | Text     | string     | | |
| phone     | Text     | string     | | plz give the phone number with country code, like +886|
| is_subscriber_email     | Text     | bool     | | Optional. If the `ignore subscriber` option is checked in the workflow node, the value of this parameter will be ignored, and the message will be sent regardless. If the `ignore subscriber` option is not checked, the decision to send will be based on this parameter, with a default value of True.|
| is_subscriber_sms     | Text     | bool    | | Optional. If the `ignore subscriber` option is checked in the workflow node, the value of this parameter will be ignored, and the message will be sent regardless. If the `ignore subscriber` option is not checked, the decision to send will be based on this parameter, with a default value of True.|
#### Example
```json
\\ JSON
{
    "userInfos": [
        {
            "member_sn": "sn1",
            "email": "sn1@gmail.com",
            "phone": "+886987654321",
            "is_subscriber_email": true,
            "is_subscriber_sms": false
        },
        {
            "member_sn": "sn2",
            "email": null,
            "phone": "+886987654322",
            "is_subscriber_email": false,
            "is_subscriber_sms": true
        },
        {
            "member_sn": "sn3",
            "email": "sn3@gmail.com",
            "phone": null,
            "is_subscriber_email": false,
            "is_subscriber_sms": false
        },
        ...
    ]
}
```

### Fail

#### status_code: 4xx or 5xx

#### Example
```json
{
    "ErrMsg": "STH wrong~~~"
}
```


## SetUp Data

### API endpoint
> The endpoint from which we can obtain audience-sensitive information data.

### API Key
> Plz gen API Key by yourself.

### Rate Limit
> 預期一秒至少 10 次
> Tell me how many requests per second your server can handle.

### Batch size 
> 預期每次至少 500 筆
> How many data can we get at once?

### Is Nat
> Does your server require whitelist configuration?

### 加密方式：AES-256
> Optional
> 請提供 32 位元的 key
> 目前只有預期 email 跟 phone 有被加密（解密）的需求