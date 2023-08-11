# Import Product API

* > api_key: xxxxx-xxxxx-xxxxx
* > tid: OA-xxxxxxx

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/products/import/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "id": "1",
        "title": "一件普通衣服",
        "link": "http://test.com/products/normal-shirt",
        "availability": "in stock",
        "image_link": "https://test.com/media/widGh1bWIiLCI2MDB4NjAwIl1d.png?sha=0e0ad71b5e5ccaf7",
        "price": "999",
        "sale_price": "1",
        "sale_price_effective_date": "2020-08-01T00:00:00+08:00/2020-08-31T23:59:59+08:00",
        "product_type": "T-shirt"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "site": "AAAA"
}'
```

## Example with multiple ids

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/products/import/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "id": {"default": "1", "CRM": "crm_id", "ERP": "erp_id"},
        "title": "一件普通衣服",
        "link": "http://test.com/products/normal-shirt",
        "availability": "in stock",
        "image_link": "https://test.com/media/widGh1bWIiLCI2MDB4NjAwIl1d.png?sha=0e0ad71b5e5ccaf7",
        "price": "999",
        "sale_price": "1",
        "sale_price_effective_date": "2020-08-01T00:00:00+08:00/2020-08-31T23:59:59+08:00",
        "product_type": "T-shirt"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx",
    "site": "AAAA"
}'
```

> If Organization dose not have multi sites, site field can be None or null.

### data 必填欄位說明


|          欄位           | 說明                                     | 備註                                        |
|:-----------------------:| ---------------------------------------- | ------------------------------------------- |
|       id   | 商品的 id，可以是一個字串，也可以是一個 object，當 id 為 object 時，可以帶入多組 id 表示該商品在各個不同系統中的 id。                | 此為唯一值，可以是 SKU                                     |
|      title       | 商品的名稱                               | e.g. 普通 T 恤                   |
|       link       | 商品的網址 |連結必須是有效且開頭為 http:// 或 https:// 的網址。|
|      availability       | 商品目前提供的狀態|  e.g. `in stock`、`available for order`, `preorder`，其餘值皆視為False。 |
|    image_link    | 商品主要圖像的網址。圖像必須為 JPEG 或 PNG 格式，至少 500 x 500 像素，最大 8 MB。 | e.g. http://www.test.com/products/shirt.jpg |
|      price      | 商品的價錢| 將價格的格式設定為數字，後面接一個空格和 3 個字母的 ISO 4217 幣別代碼。一律使用句點 (.) 作為小數點，不要使用逗點 (,)。 e.g. 999 TWD|



### data 選填欄位說明


| 欄位 | 說明 | 備註 |
| -------- | -------- | -------- |
|      sale_price      | 商品特價 (有特價時)。 | 與 price 欄位相同。 e.g. 100 TWD |
| sale_price_effective_date | 商品特價開始和結束的日期、時間和時區。| 如果未新增此欄位，所有 sale_price 的商品都會維持特價促銷狀態，直到移除商品的促銷價格為止。 格式為 YYYY-MM-DDT23:59:59+00:00/YYYY-MM-DDT23:59:59+00:00。 e.g. 2020-04-30T09:30:00+08:00/2020-05-31T09:30:00+08:00|
| product_type | 商品的標籤。 | 一個商品貼多個標籤用 `>`分隔。e.g. "tagA>tagB>tagC" |