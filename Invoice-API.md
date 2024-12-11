## Description
* Retrieve e-invoice data by each action.

## API URL
* `https://api.omnisegment.com/api/v1/invoices/einvoice/`

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

---

## Request (查詢發票表頭)
> 利用電子發票證明聯上的二維條碼(QR Code)或者一維條碼(BarCode)，查詢該電子發票證明聯表頭資訊，其回應資訊含：發票號碼、發票開立日期、賣方名稱及發票狀態等資訊。

### Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | **Note** |
| :------: | ------ | ------ | ------ | :------: | ------ |
| oa_id | The LINE official account ID | "1655555555" | string | &#10004; | |
| line_uid | The user's LINE identity ID | "U123457789" | string | &#10004; | |
| campaign_id | Campaign ID | "123" | string | &#10004; | |
| version | 版本號碼 | "0.5" | string | &#10004; | 請參考財政部電子發票應用 API |
| action | 查詢發票表頭 | "invoice_header" | string | &#10004; | 帶入範例值就好 |
| type | 發票查詢時使用的號碼別 | "Barcode" | string | &#10004; | 請參考財政部電子發票應用 API |
| invNum | 發票號碼 | "AB12345678" | string | &#10004; | 請參考財政部電子發票應用 API |
| invDate | 發票日期 | "2024/10/01" | string | &#10004; | 請參考財政部電子發票應用 API |
| generation |  |  | string | &#10004; | 請參考財政部電子發票應用 API |

* Note: 

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "code": "<訊息回應碼>",
        "msg": "<系統回應訊息>",
        "invNum": "<發票號碼>",
        "invDate": "<發票開立日期 yyyyMMdd>",
        "sellerName": "<賣方名稱>",
        "sellerBan": "<賣方營業人統編(文字)>",
        "invoiceTime": "<發票開立時間(HH:mm:ss)>"
    }
}
```

---

## Request (查詢發票明細)
> 利用電子發票證明聯上的二維條碼(QR Code)或者一維條碼(BarCode)，查詢該電子發票證明聯消費明細資料，至多查詢 99 次。

### Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | **Note** |
| :------: | ------ | ------ | ------ | :------: | ------ |
| oa_id | The LINE official account ID | "1655555555" | string | &#10004; | |
| line_uid | The user's LINE identity ID | "U123457789" | string | &#10004; | |
| campaign_id | Campaign ID | "123" | string | &#10004; | |
| version | 版本號碼 | "0.5" | string | &#10004; | 請參考財政部電子發票應用 API |
| action | 查詢發票明細 | "invoice_detail" | string | &#10004; | 帶入範例值就好 |
| type | 發票查詢時使用的號碼別 | "Barcode" | string | &#10004; | 請參考財政部電子發票應用 API |
| invNum | 發票號碼 | "AB12345678" | string | &#10004; | 請參考財政部電子發票應用 API |
| generation |  |  | string | &#10004; | 請參考財政部電子發票應用 API |
| invTerm | 發票期別 | "10108" | string | Type 為 Barcode 時為必填 | 請參考財政部電子發票應用 API |
| invDate | 發票日期 | "2024/10/01" | string | &#10004; | 請參考財政部電子發票應用 API |
| encrypt | 發票檢驗碼 |  | string | type為 QRCode 時為必填 | 請參考財政部電子發票應用 API |
| sellerID | 商家統編 |  | string | type為 QRCode 時為必填 | 請參考財政部電子發票應用 API |
| randomNumber | 商家統編 | "0000" | string | &#10004; | 請參考財政部電子發票應用 API |

* Note: 

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "code": "<訊息回應碼>",
        "msg": "<系統回應訊息>",
        "invDate": "<發票開立日期 yyyyMMdd>",
        "invNum": "<發票號碼>",
        "sellerName": "<賣方名稱>",
        "sellerBan": "<賣方營業人統編(文字)>",
        "invoiceTime": "<發票開立時間(HH:mm:ss)>",
        "amount": "<總金額>",
        "details": [
            {
                "rowNum": "<第 1 筆明細編號>",
                "description": "<品名 1>",
                "quantity": "<數量 1>",
                "unitPrice": "<單價 1>",
                "amount": "<小計 1>"
            },
            {
                "rowNum": "<第 2 筆明細編號>",
                "description": "<品名 2>",
                "quantity": "<數量 2>",
                "unitPrice": "<單價 2>",
                "amount": "<小計 2>"
            }
            // ...更多明細資料
        ]
    }
}
```

---

## Request (載具發票表頭查詢)
> 可依載具卡別及載具隱碼查詢載具內所持有的雲端發票。最早查詢起始時間為查詢當日前 6 個月 1 日起(例如 9 月 5 日時,最早查詢起始時間為 3 月 1 日起)。

### Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | **Note** |
| :------: | ------ | ------ | ------ | :------: | ------ |
| oa_id | The LINE official account ID | "1655555555" | string | &#10004; | |
| line_uid | The user's LINE identity ID | "U123457789" | string | &#10004; | |
| campaign_id | Campaign ID | "123" | string | &#10004; | |
| version | 版本號碼 | "0.5" | string | &#10004; | 請參考財政部電子發票應用 API |
| action | 載具發票表頭查詢 | "carrier_invoice_check" | string | &#10004; | 帶入範例值就好 |
| cardType | 卡別 | "3J0002" | string | &#10004; | 請參考財政部電子發票應用 API |
| cardNo | 手機條碼/卡片(載具)隱碼 | "/AB56P5Q" | string | &#10004; | 請參考財政部電子發票應用 API |
| expTimeStamp | 有效存續時間戳記 | "2147483647" | string | &#10004; | 請參考財政部電子發票應用 API |
| timeStamp | 時間戳記| 1344102065 | int | &#10004; | 請參考財政部電子發票應用 API |
| startDate | 查詢起始時間 | "2012/07/01" | string | &#10004; | 請參考財政部電子發票應用 API |
| endDate | 查詢結束時間 | "2012/07/31" | string | &#10004; | 請參考財政部電子發票應用 API |
| onlyWinningInv | 僅回傳中獎資訊 | "Y" | string | &#10004; | 請參考財政部電子發票應用 API |
| cardEncrypt | 手機條碼驗證碼/卡片(載具)驗證碼 |  | string | &#10004; | 請參考財政部電子發票應用 API |

* Note: 

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "v": "<版本號碼>",
        "code": "<訊息回應碼>",
        "msg": "<系統回應訊息>",
        "details": [
            {
                "rowNum": "<第一筆發票>",
                "invNum": "<發票號碼 1>",
                "cardNo": "<手機條碼/卡片(載具)隱碼>",
                "sellerName": "<發票 1 賣方名稱>",
                "amount": "<發票 1 總金額>",
                "sellerBan": "<發票 1 賣方營業人統編(文字)>",
                "invoiceTime": "<發票 1 發票開立時間(HH:mm:ss)>",
                "invDate": {
                    "year": "<發票 1 開立年>",
                    "month": "<發票 1 開立月>",
                    "date": "<發票 1 開立日>",
                    "day": "<發票 1 開立星期>",
                    "hours": "<發票 1 開立時>",
                    "minutes": "<發票 1 開立分>",
                    "seconds": "<發票 1 開立秒>",
                    "time": "<發票 1 開立時間戳記>",
                    "timezoneOffset": "<發票 1 開立時區>"
                }
            },
            {
                "rowNum": "<第二筆發票>",
                "invNum": "<發票號碼 2>",
                "cardNo": "<手機條碼/卡片(載具)隱碼>",
                "sellerName": "<發票 2 賣方名稱>",
                "amount": "<發票 2 總金額>",
                "sellerBan": "<發票 2 賣方營業人統編(文字)>",
                "invoiceTime": "<發票 2 發票開立時間(HH:mm:ss)>",
                "invDate": {
                    "year": "<發票 2 開立年>",
                    "month": "<發票 2 開立月>",
                    "date": "<發票 2 開立日>",
                    "day": "<發票 2 開立星期>",
                    "hours": "<發票 2 開立時>",
                    "minutes": "<發票 2 開立分>",
                    "seconds": "<發票 2 開立秒>",
                    "time": "<發票 2 開立時間戳記>",
                    "timezoneOffset": "<發票 2 開立時區>"
                }
            }
            // ...更多發票資料
        ]
    }
}

```

---

## Request (載具發票明細查詢)
> 查詢載具內所持有的雲端發票消費明細。

### Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | **Note** |
| :------: | ------ | ------ | ------ | :------: | ------ |
| oa_id | The LINE official account ID | "1655555555" | string | &#10004; | |
| line_uid | The user's LINE identity ID | "U123457789" | string | &#10004; | |
| campaign_id | Campaign ID | "123" | string | &#10004; | |
| version | 版本號碼 | "0.5" | string | &#10004; | 請參考財政部電子發票應用 API |
| action | 載具發票明細查詢 | "carrier_invoice_detail" | string | &#10004; | 帶入範例值就好 |
| cardType | 卡別 | "3J0002" | string | &#10004; | 請參考財政部電子發票應用 API |
| cardNo | 手機條碼/卡片(載具)隱碼 | "/AB56P5Q" | string | &#10004; | 請參考財政部電子發票應用 API |
| expTimeStamp | 有效存續時間戳記 | "2147483647" | string | &#10004; | 請參考財政部電子發票應用 API |
| timeStamp | 時間戳記| 1344102065 | int | &#10004; | 請參考財政部電子發票應用 API |
| invNum | 發票號碼 | "AB12345678" | string | &#10004; | 請參考財政部電子發票應用 API |
| invDate | 發票日期 | "2012/07/12" | string | &#10004; | 請參考財政部電子發票應用 API |
| sellerName | 開立賣方名稱 | "統一超商" | string |  | 請參考財政部電子發票應用 API |
| amount | 金額 | "25" | string |  | 請參考財政部電子發票應用 API |
| cardEncrypt | 手機條碼驗證碼/卡片(載具)驗證碼 |  | string | &#10004; | 請參考財政部電子發票應用 API |

* Note: 

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "code": "<訊息回應碼>",
        "msg": "<系統回應訊息>",
        "invDate": "<發票開立日期>",
        "sellerName": "<賣方名稱>",
        "amount": "<總金額>",
        "sellerBan": "<發票 1 賣方營業人統編(文字)>",
        "invoiceTime": "<發票 1 發票開立時間(HH:mm:ss)>",
        "details": [
            {
                "rowNum": "<第一筆明細編號>",
                "description": "<品名 1>",
                "quantity": "<數量 1>",
                "unitPrice": "<單價 1>",
                "amount": "<小計 1>"
            },
            {
                "rowNum": "<第二筆明細編號>",
                "description": "<品名 2>",
                "quantity": "<數量 2>",
                "unitPrice": "<單價 2>",
                "amount": "<小計 2>"
            }
            // ...更多明細資料
        ]
    }
}

```