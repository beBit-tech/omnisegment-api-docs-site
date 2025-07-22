# Batch Import Audience API

> Maximum number of audience in a batch request should not be larger than 50.

```
POST https://api.omnisegment.com/api/v2/audiences/batch-import/
```

## Request headers

`Content-Type: application/json`

## Request body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid |
| api_key | string | &#10004; | 組織 api_key |
| data | array | &#10004; | Array of [data object](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Import-Audience-API#data-object) |
| ignore_empty_value | boolean | | - 當 ignore_empty_value 為 `true` 時，輸入資料為 `""` 或是 `null` 時，舊資料不會被清空；輸入資料為 `"none"` 時資料會被清空。<br>- 當 ignore_empty_value 為 `false` 時，輸入資料為 `""`、`null`、`"none"` 時資料會被清空。<br>無法被清空的欄位依舊無法被清空，否則會出現錯誤。 |
| merge_key | string | | 預設值為 `member_sn`，可接受之選項有 `line_id`, `email`, `phone`, `messenger_psid` |
| tag_mode | string | | 預設值為 `append`，可接受之選項有 `append`, `replace`<br><br>- 當 tag_mode 為 `append` 時，data 內 tag 欄位輸入的標籤會以 append 方式加到會員身上，例如會員A 原先有 `tag_a`, `tag_b` 標籤，若 data 內提供 ``"tags": "tag_b,tag_c"``，則會員A 會多出 `tag_c` 標籤。<br>- 當 tag_mode 為 `replace` 時，data 內 tag 欄位輸入的標籤會以 replace 方式取代會員身上原有標籤，例如會員A 原先有 `tag_a`, `tag_b` 標籤，若 data 內提供 ``"tags": "tag_c,tag_d"``，則會員A 身上標籤會變成 `tag_c`, `tag_d` 標籤，原本的 `tag_a`, `tag_b` 兩個標籤會被移除。|
|custom_fields_identifier_field|object||自定義欄位的識別key，適用於多個欄位的自定義欄位用來更新指定子欄位值。 <br> for example `{"root_key_1": "sub_field_key1", "root_key_2": "sub_field_key2"}`<br> 會根據`root_key_1` 內的 子欄位 `sub_field_key1`相同的去更新對應的資料。 <br/><br/> 請注意，顧客自定義欄位的「文字格式」最多為 1025 字元。||

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
    "ERR_MSG": "Missing Input Error: These values are required in post data : api_key, tid, data",
    "ERR_TYPE_KEY": "Missing Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}
```

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v2/audiences/batch-import/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": [
        {
            "member_sn": "1",
            "name": "Eason Lee",
            "first_name": "Eason",
            "last_name": "Lee",
            "email": "eason@example.com",
            "phone": "+886912345678",
            "member_level": "1",
            "sex": "female",
            "birthday": "1990-01-01",
            "register_date": "2020-06-04T08:30:37.235482+08:00",
            "register_type": "line",
            "facebook_id": "facebook_id",
            "google_id": "google_id",
            "line_id": "Uxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "fcm_token": "fcm_token",
            "fcm_tokens": [
                {
                    "token": "fcm_token",
                    "active": true,
                    "type": "android"
                }
            ],
            "is_subscriber": true,
            "is_subscriber_line": true,
            "is_subscriber_sms": true,
            "is_subscriber_pn": true,
            "is_active": true,
            "is_headless_account": false,
            "crm_pk": "1",
            "tags": "tag_a,tag_b,tag_c",
            "iso_code": "TW",
            "city": "Taipei",
            "country": "Taiwan",
            "province": "Natal",
            "zip_code": "30084",
            "address": "17F., No. 109, Sec. 3, Minsheng E. Rd., Songshan Dist., Taipei City 105402 , Taiwan (R.O.C.)",
            "email_channels": [
                {
                    "name": "email",
                    "subscription_status": false
                }
            ],
            "line_channels": [
                {
                    "name": "line",
                    "subscription_status": false
                }
            ]
        },
        {
            "member_sn": "2",
            "name": "Lebron James",
            "first_name": "Lebron",
            "last_name": "James",
            "email": "lebron@example.com",
            "phone": "+886912345677",
            "member_level": "2",
            "sex": "male",
            "birthday": "1990-01-01",
            "register_date": "2020-06-04T08:30:37.235482+08:00",
            "register_type": "line",
            "facebook_id": "facebook_id",
            "google_id": "google_id",
            "line_id": "Uxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "fcm_token": "fcm_token",
            "fcm_tokens": [
                {
                    "token": "fcm_token",
                    "active": true,
                    "type": "android"
                }
            ],
            "is_subscriber": true,
            "is_subscriber_line": true,
            "is_subscriber_sms": true,
            "is_subscriber_pn": true,
            "is_active": true,
            "is_headless_account": false,
            "crm_pk": "1",
            "tags": "tag_a,tag_b,tag_c",
            "iso_code": "TW",
            "city": "Taipei",
            "country": "Taiwan",
            "province": "Natal",
            "zip_code": "30084",
            "address": "17F., No. 109, Sec. 3, Minsheng E. Rd., Songshan Dist., Taipei City 105402 , Taiwan (R.O.C.)",
            "email_channels": [
                {
                    "name": "email",
                    "subscription_status": false
                }
            ],
            "line_channels": [
                {
                    "name": "line",
                    "subscription_status": false
                }
            ]
         }
    ],
    "tid": "OA-xxxxxx",
    "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "ignore_empty_value": true,
    "merge_key": "member_sn",
    "tag_mode": "replace"
}'
```