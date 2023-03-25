key的範例

* api key : xxxxxx-xxxxxxx-xxxxxx 
* tid : OA-xxxxxxxx 

example:

# If your account support multi-site, you can use this curl.

```
curl --location --request POST 'https://api.omnisegment.com/ma_audience/import-audience/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "member_sn": "1",
        "name": "Eason Lee",
        "first_name": "Eason",
        "last_name": "Lee",
        "email": "eason@demo",
        "phone": "+886912345678",
        "member_level": "1",
        "sex": "female",
        "birthday": "1990-01-01",
        "register_date": "2020-6-4",
        "facebook_id": "facebook_id",
        "google_id": "google_id",
        "line_id": "line_id",
        "fcm_token": "fcm_token",
        "apns_token": "apns_token",
        "is_subscriber": true,
        "is_subscriber_line": true,
        "is_subscriber_sms": true,
        "is_subscriber_pn": true,
        "is_active": true,
        "crm_pk": "1",
        "tags": "tag_a,tag_b,tag_c",
        "sites": "site_a,site_b,site_c",
        "iso_code": "TW",
        "city": "Taipei",
        "country": "Taiwan",
        "province": 'Natal',
        "zip_code": '30084',
        "address": 'National Taiwan University No. 1, Sec. 4, Roosevelt Rd. Da'an Dist., Taipei City 10617 R.O.C.',
        "register_type": "line",
        "優惠券": [{"名稱":"V6","金額":1000,"是否":true,"到期日":"2023-03-31 13:47:06","時間":"2023-03-20 13:47:17"}]
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "ignore_empty_value": true
}'
```
# In this case, there should be a custom field named 優惠券 (JSON type) with 名稱 (Char), 金額 (Decimal), 是否 (Boolean), 到期日 (Date), 時間(Datetime) as its subfields
---------------------------------------

# If your account not support multi-site, please use this curl.
```
curl --location --request POST 'https://api.omnisegment.com/ma_audience/import-audience/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "member_sn": "1",
        "name": "Eason Lee",
        "first_name": "Eason",
        "last_name": "Lee",
        "email": "eason@demo",
        "phone": "+886912345678",
        "member_level": "1",
        "sex": "female",
        "birthday": "1990-01-01",
        "register_date": "2020-6-4",
        "facebook_id": "facebook_id",
        "google_id": "google_id",
        "line_id": "line_id",
        "fcm_token": "fcm_token",
        "apns_token": "apns_token",
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
        "province": 'Natal',
        "zip_code": '30084',
        "address": 'National Taiwan University No. 1, Sec. 4, Roosevelt Rd. Da'an Dist., Taipei City 10617 R.O.C.',
        "register_type": "line"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "ignore_empty_value": true
}'
```

## data內欄位說明
| **必填欄位** | **說明** | **備註** | **『使用者資料』節點當中的應用** |
| :------: | ------ | ------ | ------ |
| member_sn | **`"member_sn": 1`**<br>會員編號 |||
| **<br>選填欄位<br><br>** | | ||
| name | **`"name": "Eason Lee"`**<br>姓名 | - 若沒有給name這個Key, 則會以first_name + last_name 的值代替<br>- 可於editor中帶入個人化資訊 | |
| first_name | **`"first_name": "Eason"`**<br>名字 | 可於editor中帶入個人化資訊 ||
| last_name | **`"last_name": "Lee"`**<br>姓氏 | 可於editor中帶入個人化資訊 ||
| email | **`"email": "eason@demo.com"`**<br>信箱| 可於editor中帶入個人化資訊 | - 電子信箱<br>- 是否有Email地址 |
| phone | **`"phone": "+886912345678"`**<br>手機 | 可於editor中帶入個人化資訊 | - 電話<br>- 是否有電話號碼 |
| member_level | **`"member_level": "1"`**<br>會員等級 | | 會員等級 |
| sex | **`"sex": "male"`**<br>**`"sex": "female"`**<br>性別<br>男: male<br>女: female | | 性別 |
| birthday | **`"birthday": "1990-01-01"`**<br>生日 | | 年齡 |
| register_date | **`"register_date": "2020-6-4"`**<br>註冊日期 | | 註冊日期 |
| facebook_id | **`"facebook_id": "facebook_id"`**<br> facebook id | | |
| google_id | **`"google_id": "google_id"`**<br> google id | | |
| line_id | **`"line_id": "line_id"`**<br> line id | | 是否有Line id |
| messenger_psid | **`"messenger_psid": "messenger_psid"`**<br> messenger psid | | 是否有Messenger PSID |
| fcm_token | **`"fcm_token": "fcm_token"`**<br>顧客在APP上的token (support Android & iOS) | | 是否有PN token |
| apns_token | **`"apns_token": "apns_token"`**<br>顧客在iOS APP 上的token (only for iOS) | | 是否有PN token |
| is_subscriber | **`"is_subscriber": true`**<br>是否訂閱 Email | | 是否訂閱 |
| is_subscriber_sms | **`"is_subscriber_sms": true`**<br>是否訂閱 SMS | | 是否訂閱 SMS |
| is_subscriber_line | **`"is_subscriber_line": true`**<br>是否訂閱 LINE | | 是否訂閱 LINE |
| is_subscriber_pn | **`"is_subscriber_pn": true`**<br>是否訂閱 推播通知 | | 是否訂閱 推播通知 |
| is_active | **`"is_active": true`**<br> | | |
| is_headless_account | **`"is_headless_account: false"`** | 無頭會員有可能被合併到有頭會員 | 是否為無頭會員 |
| crm_pk | **`"crm_pk": "1"`**<br> | | |
| tags | **`"tags": "tag_a,tag_b,tag_c"`**<br>標籤 | 若有多個標籤則以`,`分隔 | 標籤 |
| iso_code | **`"iso_code": "TW"`**<br>國碼, 國碼遵循 <a href="https://zh.wikipedia.org/wiki/國家地區代碼">國家地區代碼</a> | | 國碼 |
| sites | **`"sites": "site_a,site_b,site_c"`**<br>網站 | 產品自動帶入也與此欄位有關聯 | 網站 |
| city | **`"city": "Taipei"`**<br>城市 | | 城市 |
| country | **`"country": "Taiwan"`**<br>國家 | | 國家 |
| province| **`"province": "Natal"`**<br>省/州 | | 省/州 |
| zip_code| **`"zip_code": "30084"`**<br>郵遞區號| | 郵遞區號 |
| address| **`"address": "National Taiwan University No. 1, Sec. 4, Roosevelt Rd. Da'an Dist., Taipei City 10617 R.O.C."`**<br>地址| | 地址|
| register_type | **`"register_type": "line"`**<br>註冊管道 | | 註冊管道 |

## 其他欄位說明
| **必填欄位** | **說明** | **備註** | **『使用者資料』節點當中的應用** |
| :------: | ------ | ------ | ------ | 
| tid | **`"tid": "OA-xxxxxxxx"`**<br>組織 tid |
| api_key | **`"api_key": "xxxxxx-xxxxxxx-xxxxxx"`**<br>組織 api key |
| **<br>選填欄位<br><br>** | | |
| ignore_empty_value | **`"ignore_empty_value": true`**<br>由 `true` 或 `false` 判斷是否忽略空字串及空值 | - 當 `ignore_empty_value` 為 `true` 時，輸入資料為 `""` 或是空值時，舊資料不會被清空；輸入資料為 `"none"` 時資料被清空。<br> - 當 `ignore_empty_value` 為 `false` 時，輸入資料為 `""` 、空值、`"none"` 時資料被清空。<br> - 無法被清空的欄位依舊無法被清空，否則會出現錯誤。
| merge_key | **`"merge_key": "line_id"`** | 預設值為 null，可接受之選項有<br>"line_id", "email", "phone", "messenger_psid" |