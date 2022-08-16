# Import Product Guarantee API
* An API endpoint for import product's guarantee data

## Required Fields
- **tid**: Organization's id.

- **api_key**: Organization's api key.

- **data**: Product guarantee data content.

  - Necessary fields: `member_sn`, `products`, `campaign_id`, `purchase_date`
  - Optional fields: `product_name`, `campaign_name`, `purchase_source`, `purchase_city`, `registration_date`

## Example

```
curl --location --request POST 'https://omnisegment.com/api/import-proudct-guarantee-data/' \
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
      }
   }
}'
```