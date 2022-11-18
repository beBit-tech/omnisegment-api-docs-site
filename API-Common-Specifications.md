# API Common Specifications

* Domain name

    Make sure to use the correct domain name for each endpoint.

    | domain name  | endpoint   |  
    |---|---|
    |  `omnisegment.com` | `https://omnisegment.com/api/v1/interaction-report/` <br/> `https://omnisegment.com/api/v1/tracking-event-report/`   <br/> `https://omnisegment.com/api/v1/products/import-event-registration-data/` <br/> `https://omnisegment.com/api/v1/products/import-product-guarantee-data/` <br/> `https://omnisegment.com/api/v1/products/import/` <br/> `https://omnisegment.com/api/import-gift-voucher/` <br/> `https://omnisegment.com/omnidata/show-market-report/` <br/> `https://omnisegment.com/api/import-purchase-data/` <br/> `https://omnisegment.com/ma_audience/import-audience/`|

* Response status code
    * `502 Bad Gateway` `503 Service Unavailable` `504 Gateway timeout`

       If you receive one of the above status codes, retry again every **five minutes** until getting other status code or having retried over **five times**.
