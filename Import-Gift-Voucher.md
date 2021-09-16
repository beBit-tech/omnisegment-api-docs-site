
* > api_key: xxxxx-xxxxx-xxxxx
* > tid: OA-xxxxxxx

##### example:

```
curl --location --request POST 'https://omnisegment.com/api/import-gift-voucher/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "voucher_id": "111",
        "member_sn": "AAAAAA",
        "voucher_type": "birthday_gift",
        "amount": 999,
        "valid_from": "2020-03-03",
        "valid_util": "2021-03-03"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "site": "AAAA"
}'
```
If Organization dose not have multi sites, site field can be None or null.

### data 欄位說明

|          欄位           | 說明                                     | 備註                                        |
|:-----------------------:| ---------------------------------------- | ------------------------------------------- |
|       voucher_id| 購物金的 id, string              | 此為唯一值，必填                                   |
|      member_sn| 會員的編碼, string                 | 必填                   |
|       voucher_type| 購物金類別, string|
|      amount| 購物金金額, int|  必填 |
|    valid_from| 發放日期, string |  |
|      valid_util| 購物金到期日, string| 必填|
