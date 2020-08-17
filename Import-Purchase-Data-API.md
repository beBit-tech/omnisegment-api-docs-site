# Import Purchase Data API

An API endpoint for import audience's purchase history data

## Required Field:

- tid: Organization id

- api_key: Organization api key

- data: Purchase data content.

  - Allow fields: `['member_sn', 'datetime', 'transaction_id', 'transaction_revenue', 'products', 'products_quantity', 'coupon', 'source', 'device', 'user_agent', 'quantities']`
  - Required fields: `member_sn`, `datetime`, `transaction_id` and `transaction_revenue`

## Example:

```
curl --location --request POST 'https://omnisegment.com/api/import-purchase-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "tid": "OA-xxxxxx",
    "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "data": {
       "member_sn":1,
       "transaction_id":"23740b4a-5872-4363-ad32-5532a89e4cb1",
       "datetime":"2020-1-1 0:0:0",
       "products":"1,2",
       "quantities":2,
       "products_quantity":"1,1",
       "transaction_revenue":5000.0,
       "user_agent":"Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1"}
}'
```

## data內欄位說明
| 必填欄位 | 說明 | |
| ------ | ------ | ------ |
| member_sn | `"member_sn": 1`<br>會員編號 |
| datetime | `"datetime": "2013-06-27T08:48:27-04:00"`<br>訂單日期, 日期格式遵循<a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> |
| transaction_id | `"transaction_id":"23740b4a-5872-4363-ad32-5532a89e4cb1"`<br>訂單ID |
| transaction_revenue | `"transaction_revenue":5000`<br>訂單收入 |
| 選填欄位 | |
| products | `"products":"1,2"`<br>此訂單內包含的商品ID，若訂單內有多筆商品則以`,`分隔。 | 若OmniSegment 沒有則會自動建立, 商品名稱預設為這邊的商品ID|
| products_quantity | `"products_quantity":"1,1"`<br>此訂單內每個商品的數量，若訂單內有多筆商品則以`,`分隔，這邊會對應products 的順序。 | products 不可為空 |
| coupon | `"Coupon": "couponABC"`<br>優惠名稱 |
| source | `"source": “Facebook"`<br>來源名稱|
| device | `"device": "Android"`<br>此訂單來自哪個裝置 |
| user_agent | `"user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36"`<br>使用者代理，這邊可以清楚知道使用者是透過什麼工具來產生這筆訂單（電腦系統、瀏覽器、瀏覽器版本等） |
| quantities | `"quantities":2`<br>訂單內商品總數量 |
