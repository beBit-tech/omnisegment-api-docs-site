## API URL
* `https://api.omnisegment.com/api/v2/voucher/batch-import/`

## Description
 - Batch Import Audience Gift Voucher Data Endpoint

## API Method
* `POST`

## Request 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| data | 匯入購物金的資料 | **`"data": [{..}, {..}, ..]`** | list | &#10004; | 請看下方範例 |
| tid | 組織識別碼| **`"tid": "OA-xxxxxxx"`** | string | &#10004; | |
| api_key | 組織 api 金鑰 | **`"api_key": "xxxxx-xxxxx-xxxxx"`** | string | &#10004; | |
| site | multi sites 組織個別網站名稱 | **`"site": "Test Site"`** | string | | |

> If Organization dose not have multi sites, site field can be None or null.

## data 欄位說明

|          欄位           | 說明                                     | 備註                                        |
|:-----------------------:| ---------------------------------------- | ------------------------------------------- |
|       voucher_id| 購物金編碼 | string，此為唯一值，必填                                   |
|      member_sn| 會員編號| string，必填                   |
|       voucher_type| 名稱|string
|      amount| 金額/點數|  int，必填 |
|    valid_from| 發放日期| string |
|      valid_util| 到期日| string，必填|
|      is_redeemed| 已使用| boolean，選填|
|      category| 分類（Ex: giftvoucher, coupon......）| string，選填|


#### batch data example:
> The batch data maximum size is 100. And the rate limiter is 10 request/s.

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
