# Import Product Guarantee API
* An API endpoint for import product's guarantee data

## API URL
* `https://api.omnisegment.com/api/v1/products/import-product-guarantee-data/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**: product guarantee data content.

  - Necessary fields: `warranty_id`, `member_sn`, `products`, `registration_datetime`, `purchase_datetime`
  - Optional fields: `warranty_name`, `purchase_source`, `purchase_city`, `purchase_receipt`, `product_quantity`, `is_available`, `warranty_start_datetime`, `warranty_end_datetime`

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| warranty_id | 保固編號 | **`"warranty_id": "qqq123"`** | string | &#10004; | |
| member_sn | 會員編號 | **`"member_sn": "www123"`** | string | &#10004; | |
| product | 表示該保固對應到的商品 | **```"products": {"default": "item_group_id1", "sku": "sku_id1"}```** | dict | &#10004; | **default** 指的是 item_group_id<br>**sku** 指的是 sku_id<br>兩者可以不用同時給<br>|
| registration_datetime | 登錄日期 | **`"registration_datetime": "2022-08-17T12:00:00+08:00"`** | datetime | &#10004; | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> |
| purchase_datetime | 購買日期 | **`"purchase_datetime": "2022-08-17T12:00:00+08:00"`** | datetime | &#10004; | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a>|
| warranty_name | 保固名稱 | **`"warranty_name": "buy1get1"`** | string | | |
| purchase_source | 購買通路 | **`"purchase_source": "supermarket"`** | string | | |
| purchase_city | 購買縣市 | **`"purchase_city": "taipei"`** | string | | |
| purchase_receipt | 購買憑證 | **`"purchase_receipt": https://example.com/receipt/1.png"`** | string | | |
| product_quantity | 購買數量 | **`"product_quantity": 1`** | integer | | |
| is_available | 是否可以使用 | **`"is_available": true`**<br> | bool | | 沒給的話預設是 `true` |
| warranty_start_datetime | 商品保固起始日 | **`"warranty_start_datetime": 2022-08-17T12:00:00+08:00`** | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a><br>**warranty_end_datetime** 時間要大於 **warranty_start_datetime**，且兩者要同時賦值 |
| warranty_end_datetime | 商品保固結束日 | **`"warranty_end_datetime": 2022-09-17T12:00:00+08:00`** | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a><br>**warranty_end_datetime** 時間要大於 **warranty_start_datetime**，且兩者要同時賦值 |

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/products/import-product-guarantee-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "warranty_id": "qqq123",
      "member_sn": "www123",
      "product": {"default": "item_group_id1", "sku": "sku_id1"},
      "registration_datetime": "2022-08-17T12:00:00+08:00",
      "purchase_datetime": "2022-08-17T12:00:00+08:00",
      "warranty_name": "buy1get1",
      "purchase_source": "supermarket",
      "purchase_city": "taipei",
      "purchase_receipt": "https://example.com/receipt/1.png",
      "product_quantity": 1,
      "is_available": true,
      "warranty_start_datetime": "2022-08-17T12:00:00+08:00",
      "warranty_end_datetime": "2022-09-17T12:00:00+08:00",
   }
}'
```