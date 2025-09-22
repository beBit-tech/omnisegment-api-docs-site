# Get Purchase Data API

```
GET https://api.omnisegment.com/api/v1/orders
```

## Request Headers

| Key | Value |
| --- | --- |
| X-OmniSegment-Api-Key | Your API Key

## Query Params

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid，需請 beBit 團隊協助提供 |
| datetime_max | string | &#10004; | eg: 2025-12-01 00:00 |
| datetime_min | string | &#10004; | eg: 2025-12-01 00:00 |
| transaction_ids | string | | 可帶多個，邏輯為 OR (用 , 區隔) 上限30筆 |
| member_sns | string | | 可帶多個，邏輯為 OR (用 , 區隔) 上限30筆 |
| product_ids | string | | 可帶多個，邏輯為 OR (用 , 區隔) 上限30筆 |
| page | int | | (若沒帶，預設 response 是第一頁) |

## Response Body

| Key | Type | Description |
|------|------|----------|
| next | boolean | 是否有下一頁 |
| previous | boolean | 是否有上一頁 |
| page_count | int | 總頁數（一頁1000筆資料) |
| data | object | 訂單資料 |

### 訂單資料

| Key | Type | Description |
|------|------|----------|
| member_sn | string | 顧客編號 |
| datetime | string | 訂單時間 |
| transaction_id | string | 訂單編號 |
| transaction_revenue | string | 訂單金額 |
| transaction_status | string | 訂單狀態 |
| shipping_address | object | 配送地址 |
| products | object | 訂單商品 |

### 配送地址資料

| Key | Type |
|------|------|
| address1 | string |
| address2 | string |
| city | string |
| company | string |
| country | string |
| country_code | string |
| latitude | string |
| longitude | string |
| province | string |
| province_code | string
| zip | string |

### 商品資料

| Key | Type |
|------|------|
| product_id | string |
| product_name | string |
| product_price | float |
| product_quantity | float |


### Example

```json
{
    "next": false,
    "previous": false,
    "page_count": 1,
    "data": [
        {
            "member_sn": "664734989892e5000d0e86d4",
            "datetime": "2025-03-21T15:02:17.140000+0800",
            "transaction_id": "20250321070217521",
            "transaction_revenue": "1.00",
            "transaction_status": "SUCCESS",
            "shipping_address": {
                "address1": "測試系統中",
                "address2": "松山區",
                "city": "台北市",
                "company": null,
                "country": "台灣",
                "country_code": "TW",
                "latitude": null,
                "longitude": null,
                "province": null,
                "province_code": null,
                "zip": "105"
            },
            "products": [
                {
                    "product_id": "6422849b1438330010c2d5c2",
                    "product_name": "灰色毛衣",
                    "product_price": 1.0,
                    "product_quantity": 0
                }
            ]
        }
        ...
    ]
}
