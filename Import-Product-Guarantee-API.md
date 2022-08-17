# Import Product Guarantee API
* An API endpoint for import product's guarantee data

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**: product guarantee data content.

  - Necessary fields: `campaign_id`, `member_sn`, `products`, `registration_datetime`
  - Optional fields: `campaign_name`, `product_name`, `purchase_source`, `purchase_city`, `purchase_datetime`, `is_available`

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| campaign_id | 活動編號 | **`"campaign_id": "qqq123"`**<br> | string | &#10004; | |
| member_sn | 會員編號 | **`"member_sn": "www123"`**<br> | string | &#10004; | |
| products | 表示該商品在各個不同系統中的 id | **```"products": {"default": ["item_group_id1","item_group_id2"], "sku": ["sku_id1","sku_id2"]}"```** | object | &#10004; | **default** 指的是 item_group_id<br>**sku** 指的是 sku_id<br>兩者可以不用同時給，但如果只給 sku 的話，Omnisegment 會自動建立一個對應的 item_group_id<br>若同時給的話 default 和 sku 內的順序和數量要一致|
| registration_datetime | 登錄日期 | **`"registration_datetime": "2022-08-17T12:00:00+08:00"`**<br> | datetime | &#10004; | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> |
| campaign_name | 活動編號 | **`"campaign_name": "buy1get1"`**<br> | string | | |
| product_name | 商品名稱 | **`"product_name": ["bag","cloth"]`**<br> | object | | 順序和數量要和參數 **products** 一致|
| purchase_source | 購買通路 | **`"purchase_source": "supermarket"`**<br> | string | | |
| purchase_city | 購買縣市 | **`"purchase_city": "taipei"`**<br> | string | | |
| purchase_datetime | 購買日期 | **`"purchase_datetime": "2022-08-17T12:00:00+08:00"`**<br> | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a>|
| is_available | 是否可以使用 | **`"is_available": true`**<br> | bool | | 沒給的話預設是 `true` |


## Example

```
curl --location --request POST 'https://omnisegment.com/api/import-proudct-guarantee-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "campaign_id": "qqq123",
      "member_sn": "www123",
      "products": {"default": ["item_group_id1","item_group_id2"], "sku": ["sku_id1","sku_id2"]}",
      "registration_datetime": "2022-08-17T12:00:00+08:00",
      "campaign_name": "buy1get1",
      "product_name": ["bag","t-shirt"],
      "purchase_source": "supermarket",
      "purchase_city": "taipei",
      "purchase_datetime": "2022-08-17T12:00:00+08:00",
      "is_available": true
   }
}'
```