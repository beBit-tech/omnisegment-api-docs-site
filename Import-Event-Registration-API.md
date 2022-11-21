# Import Event Registration API
* An API endpoint for import event registration data

## API URL
* `https://api.omnisegment.com/api/v1/products/import-event-registration-data/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**: event registration data content.

  - Necessary fields: `event_id`, `member_sn`, `event_name`, `registration_datetime`
  - Optional fields: `purchase_source`, `purchase_city`, `delivery_address`, `is_available`, `purchase_datetime`, `event_start_datetime`, `event_end_datetime`

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| event_id | 活動編號 | **`"event_id": "qqq123"`** | string | &#10004; | |
| member_sn | 會員編號 | **`"member_sn": "www123"`** | string | &#10004; | |
| products | 表示該商品在各個不同系統中的 id | **```"products": {"default": ["item_group_id1","item_group_id2"], "sku": ["sku_id1","sku_id2"]}```** | dict | | **default** 指的是 item_group_id<br>**sku** 指的是 sku_id<br>兩者可以不用同時給<br>若同時給的話 default 和 sku 內的順序和數量要一致|
| registration_datetime | 登錄日期 | **`"registration_datetime": "2022-08-17T12:00:00+08:00"`** | datetime | &#10004; | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> |
| purchase_datetime | 購買日期 | **`"purchase_datetime": "2022-08-17T12:00:00+08:00"`** | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a>|
| event_name | 活動名稱 | **`"event_name": "buy1get1"`** | string | &#10004; | |
| purchase_source | 購買通路 | **`"purchase_source": "supermarket"`** | string | | |
| purchase_city | 購買縣市 | **`"purchase_city": "taipei"`** | string | | |
| delivery_address | 寄送地址 | **`"delivery_address": "台北市信義區XXXXXXX"`** | string | | |
| is_available | 是否可以使用 | **`"is_available": true`** | bool | | 沒給的話預設是 `true` |
| event_start_datetime | 活動起始日 | **`"event_start_datetime": "2022-08-17T12:00:00+08:00"`** | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a><br>**event_end_datetime** 時間要大於 **event_start_datetime**，且兩者要同時賦值 |
| event_end_datetime | 活動結束日 | **`"event_end_datetime": "2022-09-17T12:00:00+08:00"`** | datetime | | 時區必須要指定<br>日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a><br>**event_end_datetime** 時間要大於 **event_start_datetime**，且兩者要同時賦值 |

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/products/import-event-registration-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "event_id": "qqq123",
      "member_sn": "www123",
      "products": {"default": ["item_group_id1","item_group_id2"], "sku": ["sku_id1","sku_id2"]},
      "registration_datetime": "2022-08-17T12:00:00+08:00",
      "purchase_datetime": "2022-08-17T12:00:00+08:00",
      "event_name": "buy1get1",
      "purchase_source": "supermarket",
      "purchase_city": "taipei",
      "delivery_address": "台北市XXXXX",
      "is_available": true,
      "event_start_datetime": "2022-08-17T12:00:00+08:00",
      "event_end_datetime": "2022-09-17T12:00:00+08:00"
   }
}'
```