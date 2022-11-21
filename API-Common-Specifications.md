# API Common Specifications

---

### Domain name

* Make sure to use the correct domain name for each endpoint.

    | domain name  | endpoint   |  
    |---|---|
    |  `api.omnisegment.com` | `https://api.omnisegment.com/api/v1/interaction-report/` <br/> `https://api.omnisegment.com/api/v1/tracking-event-report/`   <br/> `https://api.omnisegment.com/api/v1/products/import-event-registration-data/` <br/> `https://api.omnisegment.com/api/v1/products/import-product-guarantee-data/` <br/> `https://api.omnisegment.com/api/v1/products/import/` <br/> `https://api.omnisegment.com/api/import-gift-voucher/` <br/> `https://api.omnisegment.com/omnidata/show-market-report/` <br/> `https://api.omnisegment.com/api/import-purchase-data/` <br/> `https://api.omnisegment.com/ma_audience/import-audience/`|

### Authentication
* Make sure to comply with our authentication mechanism

    | authentication | endpoint | example |  
    |---|---|---|
    |  header with key `X-OmniSegment-Api-Key` | `https://api.omnisegment.com/api/v1/interaction-report/` <br/> `https://api.omnisegment.com/api/v1/tracking-event-report/` <br/> | `"X-OmniSegment-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"` |
    | body with key `api_key` | `https://api.omnisegment.com/api/v1/products/import-event-registration-data/` <br/> `https://api.omnisegment.com/api/v1/products/import-product-guarantee-data/` <br/> `https://api.omnisegment.com/api/v1/products/import/` <br/> `https://api.omnisegment.com/api/import-gift-voucher/` <br/> `https://api.omnisegment.com/omnidata/show-market-report/` <br/> `https://api.omnisegment.com/api/import-purchase-data/` <br/> `https://api.omnisegment.com/ma_audience/import-audience/` | `"api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"` |

### Rate limit
* Make sure to comply with the specification of the rate limit for each endpoint

    | rate limit  | endpoint   |  
    |---|---|
    |  10 requests per second | `https://api.omnisegment.com/api/v1/interaction-report/` <br/> `https://api.omnisegment.com/api/v1/tracking-event-report/`   <br/> `https://api.omnisegment.com/api/v1/products/import-event-registration-data/` <br/> `https://api.omnisegment.com/api/v1/products/import-product-guarantee-data/` <br/> `https://api.omnisegment.com/api/v1/products/import/` <br/> `https://api.omnisegment.com/api/import-gift-voucher/` <br/> `https://api.omnisegment.com/omnidata/show-market-report/` <br/> `https://api.omnisegment.com/api/import-purchase-data/` <br/> `https://api.omnisegment.com/ma_audience/import-audience/`|

### General response format
* Success response format
    ```
    {"SUCCESS": true, "PAYLOAD": "xxxxxx"}
    ```
    * Note:
        * the value of key **PAYLOAD** is the result of called api, and the value depends on each api specification
        * include the status code (**200**)

* Fail response format
    ```
    {"SUCCESS": false, "ERR_MSG": "xxxxxx"}
    ```
    * Note:
        * the value of key **ERR_MSG** is the result of called api, and the value depends on each api specification
        * include the status code (**400**, **403**, **500**)

### Error response status code handbook

* `502 Bad Gateway` `503 Service Unavailable` `504 Gateway timeout`

    If you receive one of the above status codes, retry again every **five minutes** until getting other status code or having retried over **five times**.
