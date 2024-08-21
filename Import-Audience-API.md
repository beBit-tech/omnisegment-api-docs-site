# Import Audience API

> 如需一次匯入多筆顧客資料，請參考 [Batch Import Audience API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Batch-Import-Audience-API)

```
POST https://api.omnisegment.com/ma_audience/import-audience/
```

## Request headers

`Content-Type: application/json`

## Request body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid，需請 beBit 團隊協助提供 |
| api_key | string | &#10004; | 組織 api_key，需請 beBit 團隊協助提供 |
| data | object | &#10004; | [data object](#data-object) |
| ignore_empty_value | boolean | | - 當 ignore_empty_value 為 `true` 時，輸入資料為 `""` 或是 `null` 時，舊資料不會被清空；輸入資料為 `"none"` 時資料會被清空。<br>- 當 ignore_empty_value 為 `false` 時，輸入資料為 `""`、`null`、`"none"` 時資料會被清空。<br>無法被清空的欄位依舊無法被清空，否則會出現錯誤。 |
| merge_key | string | | 預設值為 `member_sn`，可接受之選項有 `line_id`, `email`, `phone`, `messenger_psid`, `source_id` |
| tag_mode | string | | 會員標籤新增方式，預設值為 `append`，可接受之選項有 `append`, `replace`<br><br>- 當 tag_mode 為 `append` 時，data 內 tag 欄位輸入的標籤會以 append 方式加到會員身上，例如會員A 原先有 `tag_a`, `tag_b` 標籤，若 data 內提供 ``"tags": "tag_b,tag_c"``，則會員A 會多出 `tag_c` 標籤。<br>- 當 tag_mode 為 `replace` 時，data 內 tag 欄位輸入的標籤會以 replace 方式取代會員身上原有標籤，例如會員A 原先有 `tag_a`, `tag_b` 標籤，若 data 內提供 ``"tags": "tag_c,tag_d"``，則會員A 身上標籤會變成 `tag_c`, `tag_d` 標籤，原本的 `tag_a`, `tag_b` 兩個標籤會被移除。|

### data object

| Name | Type | Description | Required |可於編輯器中帶入個人化資訊 | 「顧客資料」節點中的應用 |
|------|------|-------------|----------|-----------------------|------------------------|
| name | string | 姓名<br><br>若沒有給 name 這個 key, 則會以 first_name + last_name 的值代替 ||&#10004; ||
| first_name | string | 名字 || &#10004; ||
| last_name | string | 姓氏 || &#10004; ||
| email | string | 信箱 || &#10004; | - 電子信箱<br>- 是否有 Email 地址 |
| phone | string | 手機 || &#10004; | - 電話<br>- 是否有電話號碼 |
| member_sn/source_id | string | member_sn: 電商會員編號, source_id: 其他來源 id．如果是打 source_id 並且有先透過 [Audience Mapping API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Audience-Mapping-API) 打資料進來，就會以 source_id 去找對應的 Audience，並且選填欄位 source_system 為必填 | &#10004; | | |
| source_system | string | source_id 的來源系統，只有當上面選擇 source_id 時才需要帶此資料 || | |
| member_level | string | 會員等級 || | - 會員等級 |
| sex | string | 性別<br><br>男: `male`<br>女: `female` || | - 性別 |
| birthday | string | 生日<br><br>格式: `YYYY-MM-DD`<br>範例: `2020-06-04` || | - 年齡 |
| register_date | string | 註冊日期<br><br>格式: `YYYY-MM-DDTHH:mm:ss+z`<br>範例: `2020-06-04T08:30:37.235482+08:00` || | - 註冊日期 |
| register_type | string | 註冊管道 || | - 註冊管道 |
| facebook_id | string | || | |
| google_id | string | || | |
| line_id | string | || | - 是否有 LINE ID |
| messenger_psid | string | || | - 是否有 Messenger PSID |
| fcm_token | string | 顧客在 APP 上的 token<br>如果有多個，請帶入 `fcm_tokens` || | - 是否有 PN token |
| fcm_tokens | object | [fcm_tokens object](#fcm_tokens-object) || | - 是否有 PN token |
| is_subscriber | boolean | 是否訂閱 Email || | - 是否訂閱 |
| is_subscriber_sms | boolean | 是否訂閱 SMS || | - 是否訂閱 SMS |
| is_subscriber_line | boolean | 是否訂閱 LINE || | - 是否訂閱 LINE |
| is_subscriber_pn | boolean | 是否訂閱推播通知 || | - 是否訂閱推播通知 |
| is_active | boolean | 啟用狀態 || | |
| is_headless_account | boolean | 是否為無電商會員編號之會員(簡稱`無頭會員`)<br><br>無頭會員有可能被合併到有頭會員 || | - 是否為無頭會員 |
| crm_pk | string | || | |
| tags | string | 需匯入的會員標籤<br><br>若有多個標籤則以 `,` 分隔 || | |
| iso_code | string | [國碼](https://zh.wikipedia.org/wiki/國家地區代碼) || | - 國碼 |
| sites | string | 網站<br><br>產品自動帶入也與此欄位有關聯 || | - 網站 |
| city | string | 城市 || | - 城市 |
| country | string | 國家 || | - 國家 |
| province | string | 省/州 || | - 省/州 |
| zip_code | string | 郵遞區號 || | - 郵遞區號 |
| address | string | 地址 || | - 地址 |
| 自定義欄位(CustomField) | object | [CustomField object](#CustomField-object) || | `CustomField` is not available by default. Please contact us to have this feature set up.|

#### fcm_tokens object

| Name | Type | Description | Required |
|------|------|-------------|----------|
| token | string | 裝置 ID | &#10004; |
| active | boolean | 啟用狀態，預設為 `true` | |
| type | string | 裝置類型<br><br>iOS: `ios`<br>Android: `android` | |

#### CustomField object

- Single Field Type

  若該自定義欄位的 `欄位格式` **非** `多個欄位`, 如`文字`, `數字`, `布林`, `日期`, `日期與時間`，則和一般會員欄位的放入方式相同。

  If the `field_type` of the custom field **is not** `json`, such as `text`, `number`, `boolean`, `date`, or `datetime`, the input method is the same as for other fields in the Audience object.

  ```json
  // A field where field_type is datetime
  "last_login_date": "2020-06-04T08:30:37.235482+08:00"
  
  // A field where field_type is text
  "nickname": "Nick"
  ```
  
- Multiple Field Type (JSON)

  若該自定義欄位的 `欄位格式` **為** `多個欄位`, 則以下方方式放入：

  If the `field_type` of the custom field **is** `json`, then input the key-value pairs as shown below:

  ```json
  // `bonus` is the field_name and it contains sub_fields `bonus_point` and `bonus_expire_date`
  "bonus": [
              {
                  "bonus_point": "678", // A sub_field where field_type is number
                  "bonus_expire_date": "2025-06-04T08:30:37.235482+08:00" // A sub_field where field_type is datetime
              },
              // You can insert multiple items if needed
              {
                  "bonus_point": "123", 
                  "bonus_expire_date": "2025-06-04T08:30:37.235482+08:00"
              }
          ]
  ```


## Response

Returns status `200` and a JSON object with the following information.

```json
{
    "SUCCESS": true,
    "PAYLOAD": {
        "status": "OK",
        "error_msg": ""
    }
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
curl --location --request POST 'https://api.omnisegment.com/ma_audience/import-audience/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "member_sn": "1",
        "name": "Eason Lee",
        "first_name": "Eason",
        "last_name": "Lee",
        "email": "eason@example.com",
        "phone": "+886912345678",
        "member_level": "1",
        "sex": "female",
        "birthday": "1990-01-01",
        "register_date": "2020-6-4",
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
        "address": "17F., No. 109, Sec. 3, Minsheng E. Rd., Songshan Dist., Taipei City 105402 , Taiwan (R.O.C.)"
    },
    "tid": "OA-xxxxxx",
    "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "ignore_empty_value": true,
    "merge_key": "member_sn"
}'
```