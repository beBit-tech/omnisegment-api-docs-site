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

> If Organization dose not have multi sites, site field can be None or null.

## data 欄位說明

| **Field** | **Description** | **Data Type** | **Required** | Note |
|:---:| --- | --- | :---: | --- |
| voucher_id| 購物金編碼 (Voucher ID) | string | &#10004; | Unique |
| member_sn| 會員編號 (Member ID) | string | &#10004; | |
| voucher_type| 名稱 (Voucher Type) | string | &#10004; | |
| amount| 金額/點數 (Amount) | int | &#10004; | |
| valid_from| 發放日 (Voucher start date) | string | &#10004; | See Note 2 |
| valid_util| 到期日 (Voucher expiration date) | string | &#10004; | See Note 2 |
| is_redeemed| 已使用 (Is redeemed or not) | boolean | :x: | |
| category| 分類 (Category) | string | :x: | e.g., giftvoucher, coupon... |

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
