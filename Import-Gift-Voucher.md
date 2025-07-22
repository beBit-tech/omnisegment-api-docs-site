## API URL
* `https://api.omnisegment.com/api/import-gift-voucher/`

## Description
 - Import Audience Gift Voucher Data Endpoint

## API Method
* `POST`

## Request 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| data | 匯入購物金的資料 | **`"data": {...}` or `"data": [{..}, {..}, ..]`** | dict or list | &#10004; | See Note 1 |
| tid | 組織識別碼| **`"tid": "OA-xxxxxxx"`** | string | &#10004; | |
| api_key | 組織 api 金鑰 | **`"api_key": "xxxxx-xxxxx-xxxxx"`** | string | &#10004; | |
| site | multi sites 組織個別網站名稱 | **`"site": "Test Site"`** | string | | |
| identifier_field | string | | 會員mapping的欄位(***1**) |

***1** 指定用於查找會員的字段名稱。此欄位決定了API將根據哪一個字段來查找和關聯會員信息。若Request未帶入`identifier_field`則將透過`member_sn`進行查找及關連。`identifier_field`可用選項為：
 - `line_id`
 - `phone`
 - `email`
 - `messenger_psid`

> If Organization dose not have multi sites, site field can be None or null.

## data 欄位說明

| **Field** | **Description** | **Data Type** | **Required** | Note |
|:---:| --- | --- | :---: | --- |
| voucher_id| 購物金編碼 (Voucher ID) | string | &#10004; | Unique |
| member_sn/source_id | 會員編號 (Member ID) | string | &#10004; | 兩者其一必填，如果是打 source_id 並且有先透過 [Audience Mapping API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Audience-Mapping-API) 打資料進來，就會以 source_id 去找對應的 Audience，並且選填欄位 `source_system` 為必填，兩者都給的時候會以 member_sn 為主 |
| voucher_type| 名稱 (Voucher Type) | string | &#10004; | |
| amount| 金額/點數 (Amount) | int | &#10004; | |
| valid_from| 發放日 (Voucher start date) | string | &#10004; | See Note 2 |
| valid_util| 到期日 (Voucher expiration date) | string | &#10004; | See Note 2 |
| is_redeemed| 已使用 (Is redeemed or not) | boolean | :x: | |
| category| 分類 (Category) | string | :x: | e.g., giftvoucher, coupon... |
| source_system| source_id 的來源系統 | string | ▲ 當上面給 source_id 時為必填 | e.g., "offline", "CRM"... |
| custom_fields| 資料類型為「點金券」的自定義欄位 | object | | 範例 `{"voucher_custom_text": "text", "voucher_custom_number": 1, "voucher_custom_date": "2077-01-01", "voucher_custom_datetime": "2077-01-01T00:00:00+08:00"}` <br/><br/> 請注意，點金券自定義欄位的「文字格式」最多為 128 字元。|

### Note 1: Data Sample

#### single data example:
> Rate limit of single data request: 30 request/s.
```
curl --location --request POST 'https://api.omnisegment.com/api/import-gift-voucher/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "voucher_id": "111",
        "member_sn": "AAAAAA",
        "voucher_type": "birthday_gift",
        "amount": 999,
        "valid_from": "2020-03-03",
        "valid_util": "2021-03-03",
        "is_redeemed": false,
        "category": "coupon"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "site": "AAAA"
}'
```

#### batch data example:
> The batch data maximum size is 100. And rate limit is 10 request/s.

```
curl --location --request POST 'https://api.omnisegment.com/api/import-gift-voucher/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": [
        {
            "voucher_id": "111",
            "member_sn": "AAAAAA",
            "voucher_type": "birthday_gift",
            "amount": 999,
            "valid_from": "2020-03-03",
            "valid_util": "2021-03-03",
            "is_redeemed": false,
            "category": "coupon"
        },
        {
            "voucher_id": "222",
            "member_sn": "BBBBBB",
            "voucher_type": "welcome",
            "amount": 100,
            "valid_from": "2022-02-02",
            "valid_util": "2023-03-03",
            "is_redeemed": false,
            "category": "coupon"
        },
        ...
    ]
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx"
}'
```

### Note 2: Date Format


The `valid_from` and `valid_until` fields need to use the following format. Furthermore, if a date does not include a timezone, it will be stored with our system's timezone: TW: +08, JP: +09.

| **Type** | **Valid** |
| --- | --- |
| 2024-05-01 | &#10004; |
| 2024-05-01 12:00:00 | &#10004; |
| 2024-05-01 12:00:00+08 | &#10004; |
| 2024-05-01T12:00:00+08 | &#10004; |
| 2024-05-0112:00:00 | :x: |
| 2024-05-0112:00:00+08 | :x: |
| 2024-05-01-12:00:00 | :x: |
| 2024-05-01-12:00:00+08 | :x: |
