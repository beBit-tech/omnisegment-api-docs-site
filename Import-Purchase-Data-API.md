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