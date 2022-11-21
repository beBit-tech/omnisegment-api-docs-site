# Import Purchase Data API

An API endpoint for import audience's purchase history data

## Required Fields

- tid: Organization's id.

- api_key: Organization's api key.

- data: Purchase data content.

  - Allowed fields: `['member_sn', 'datetime', 'transaction_id', 'transaction_revenue', 'transaction_status', products', 'products_quantity', 'coupon', 'source', 'device', 'user_agent', 'quantities', 'physical_store_name', 'shipping_address']`
    - Allowed fields for `shipping_address`: `['address1', 'address2', 'city', 'company', 'country', 'country_code', 'latitude', 'longitude', 'province', 'province_code', 'zip']`
  - Required fields: `member_sn`, `datetime`, `transaction_id` and `transaction_revenue`

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/import-purchase-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "member_sn": 1,
      "transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb1",
      "datetime": "2020-1-1 0:0:0",
      "products": "1,2",
      "quantities": 2,
      "products_quantity": "1,1",
      "transaction_revenue": 5000.0,
      "transaction_status": "SUCCESS",
      "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1",
      "physical_store_name": "Fake Store",
      "shipping_address": {
         "address1": "123 Shipping Street",
         "address2": null,
         "city": "Shippington",
         "company": "Shipping Company",
         "country": "United States",
         "country_code": "US",
         "latitude": null,
         "longitude": null,
         "province": "Kentucky",
         "province_code": "KY",
         "zip": "40003"
      },
      "promotion": {
         "name": "promo1",
         "date_start": "2022-11-01",
         "date_end": "2022-11-30",
         "promo_id": "123456",
      }
   }
}'
```

## Example with multiple types of product id

```
curl --location --request POST 'https://api.omnisegment.com/api/import-purchase-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "member_sn": 1,
      "transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb1",
      "datetime": "2020-1-1 0:0:0",
      "products": {"default": "1,2", "CRM": "crm_id1,crm_id2", "ERP": "erp_id1,erp_id2"},
      "quantities": 2,
      "products_quantity": "1,1",
      "transaction_revenue": 5000.0,
      "transaction_status": "SUCCESS",
      "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1",
      "physical_store_name": "Fake Store",
      "shipping_address": {
         "address1": "123 Shipping Street",
         "address2": null,
         "city": "Shippington",
         "company": "Shipping Company",
         "country": "United States",
         "country_code": "US",
         "latitude": null,
         "longitude": null,
         "province": "Kentucky",
         "province_code": "KY",
         "zip": "40003"
      }
   }
}'
```

## data 內欄位說明

| **必填欄位** | **說明** | **備註** | **『歷史資料追蹤』節點當中的應用** |
| :------: | ------ | ------ | ------ | 
| member_sn | **`"member_sn": 1`**<br>會員編號 |
| datetime | **`"datetime": "2013-06-27T08:48:27-04:00"`**<br>訂單日期, 日期格式遵循 <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> | | 最後轉換時間 |
| transaction_id | **`"transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb1"`**<br>訂單ID |
| transaction_revenue | **`"transaction_revenue": 5000`**<br>訂單總金額 | | - 最後一次消費金額<br>- 總金額<br>- 平均花費|
| **<br>選填欄位<br><br>** | | |
| transaction_status | **`"transaction_status": "SUCCESS"`**<br>訂單狀態 | 不傳預設狀態為 "SUCCESS", 可接受之狀態選項有 "SUCCESS", "CANCEL", "REFUND", "FAIL", "SHIPPED", "PAID" | |
| products | **`"products": "1,2"`**<br>此訂單內包含的商品ID，若訂單內有多筆商品則以`,`分隔。<br><br>此欄位的值也可以是一個 object，用來表示該商品在各個不同系統中的 id，例如：**`"products": {"default": "1,2", "CRM": "crm_id1,crm_id2", "ERP": "erp_id1,erp_id2"}`**<br>若傳入以上內容，OmniSegment 會以 `default` 內的 id 來對應，並且將 `CRM` 以及 `ERP` 內的 id 紀錄起來(順序必須跟 `default` 一致)。 | 若OmniSegment 沒有則會自動建立, 商品名稱預設為這邊的商品ID| 購買產品名稱 |
| products_quantity | **`"products_quantity": "1,1"`**<br>此訂單內每個商品的數量，若訂單內有多筆商品則以`,`分隔，這邊會對應products 的順序。 | products 不可為空 |
| coupon | **`"Coupon": "couponABC"`**<br>優惠名稱 |
| source | **`"source": “Facebook"`**<br>來源名稱| | 最後來源 |
| device | **`"device": "Android"`**<br>此訂單來自哪個裝置 | 目前只接受 PC, Android, Iphone, Ipad, MobileWeb 這四種形式，大小寫皆可 |
| user_agent | **`"user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36"`**<br>使用者代理，這邊可以清楚知道使用者是透過什麼工具來產生這筆訂單（電腦系統、瀏覽器、瀏覽器版本等） |
| quantities | **`"quantities": 2`**<br>訂單內商品總數量 | | 任一次購買產品數量 |
| physical_store_name | **`"physical_store_name": "Fake Store"`**<br>線下商店名稱| | |
| shipping_address | **`"shipping_address": <Shipping Address Object>"`**<br>寄送地址資訊|<Shipping Address Object> 資訊請見附錄| |
| promotion | **`"promotion": <Promotion Object>"`**<br>promotion 資訊|<Promotion Object> | |

## 附錄

### Shipping Address Object

Example

```
{
    "address1":"123 Shipping Street",
    "address2":null,
    "city":"Shippington",
    "company":"Shipping Company",
    "country":"United States",
    "country_code":"US",
    "latitude":null,
    "longitude":null,
    "province":"Kentucky",
    "province_code":"KY",
    "zip":"40003"
}
```

| **選填欄位** | **說明** | **備註** |
| :------: | ------ | ------ |
| address1 | `"address1": "123 Shipping Street"`<br>地址1 | |
| address2 | `"address2": null`<br>地址2 | 外國地址之 address line 2 | |
| city | `"city": "Shippington"`<br>城市 | | |
| company |`"company": "Shipping Company"`<br>運送公司| | |
| country | `"country": "United States"`<br>寄送國家 | | |
| country_code | `"country_code": "US"`<br>寄送國家編碼 | | |
| latitude | `"latitude": null`<br>緯度 | | |
| longitude | `"longitude": null`<br>經度 | | |
| province | `"province": "Kentucky"`<br>州 | | |
| province_code| `"province_code": "KY"`<br>州碼 | | |
| zip | `"zip": "40003"`<br>郵遞區號 | | |