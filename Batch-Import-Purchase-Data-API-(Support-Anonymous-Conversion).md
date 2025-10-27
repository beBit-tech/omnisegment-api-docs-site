# Batch Import Purchase Data API

> Maximum number of purchase data in a batch request should not be larger than 50.

```
POST https://api.omnisegment.com/api/v2/purchase/batch-import/
```

## Request headers

`Content-Type: application/json`

## Request body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid，需請 beBit 團隊協助提供 |
| api_key | string | &#10004; | 組織 api_key，需請 beBit 團隊協助提供 |
| data | array | &#10004; | Array of [data object](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Import-Purchase-Data-API#data-object) |
| is_anonymous(***4**) | boolean | | 是否為匿名訂單(***3**) |
| identifier_field | string | | 會員mapping的欄位(***1**) |

***1** 指定用於查找會員的字段名稱。此欄位決定了API將根據哪一個字段來查找和關聯會員信息。若Request未帶入`identifier_field`則將透過`member_sn`進行查找及關連。`identifier_field`可用選項為：
 - `line_id`
 - `phone`
 - `email`
 - `messenger_psid`


## Response

Returns status `200` and a JSON object with the following information.

```json
{
    "SUCCESS": true,
    "PAYLOAD": null
}
```

## Error Response

Returns the following HTTP status code and an error response:

- `400 Bad Request`
- `403 Forbidden`

```json
{
    "SUCCESS": false,
    "ERR_MSG": "Missing Input Error: Request should includes tid, api_key and data",
    "ERR_TYPE_KEY": "Missing Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}
```

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v2/purchase/batch-import/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": [
     {
       "member_sn": "1",
       "datetime": "2020-01-01T00:00:00+0800",
       "transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb1",
       "transaction_revenue": 5000.0,
       "transaction_status": "SUCCESS",
       "quantities": 2,
       "products": "P001,P002",
       "products_name": "Product1,Product2",
       "products_quantity": "1,1",
       "physical_store_name": "Fake Store",
       "shipping_address": {
         "address1": "123 Shipping Street",
         "address2": null,
         "city": "Shippington",
         "company": "Shipping Company",
         "country": "United States",
         "country_code": "US",
         "latitude": null,
         "longitude": null,
         "province": "Kentucky",
         "province_code": "KY",
         "zip": "40003"
       },
       "voucher": [
         {"voucher_name" : "birthday_gift"}
       ],
       "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1"
     },
     {
       "member_sn": "1",
       "datetime": "2020-01-01T00:00:00+0800",
       "transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb2",
       "transaction_revenue": 5000.0,
       "transaction_status": "SUCCESS",
       "quantities": 2,
       "products": "P001,P002",
       "products_name": "Product1,Product2",
       "products_quantity": "1,1",
       "physical_store_name": "Fake Store",
       "shipping_address": {
         "address1": "123 Shipping Street",
         "address2": null,
         "city": "Shippington",
         "company": "Shipping Company",
         "country": "United States",
         "country_code": "US",
         "latitude": null,
         "longitude": null,
         "province": "Kentucky",
         "province_code": "KY",
         "zip": "40003"
       },
       "voucher": [
         {"voucher_name" : "birthday_gift"}
       ],
       "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1"
     }
   ]
}'
```