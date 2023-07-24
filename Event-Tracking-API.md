# Event tracking API

## Event Categories

1. [Product Impressions](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#product-impressions)
> Tracking Product list. Such as Home page, Category page or Search result page.


2. [Product Clicks](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#product-clicks)
> A user expresses interest in this particular product by clicking on the product listing to view more details.

3. [Product Detail Impressions](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#product-detail-impressions)
> After clicking on the product listing, a user views the product details page.

4. [Add / Remove from Cart](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#add--remove-from-cart)
> The user expresses intent to buy the item by adding it to a shopping cart.

5. [Checkout](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#checkout)
> Check user is ready to begin the checkout process.

6. [Purchases and Refund](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#purchases-and-refund)
> User completes the checkout process and submits their purchase.

7. [Complete Registration](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#complete-registration)
> When user complete the registration.

8. [Submit a search](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#submit-a-search)
> User use any web site search engine to search products.

9. [Custom Events](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#custom-events)
> Custom event registered in Omnisegment and trigger based on which your system define.


***

## Integrate with MemberSN(uid)
**Mapping visit user with your member system.<br/> 
The membersn could be encoded or plain,<br/> 
but it must be persistent and unique.**

***

## Parameters
| 必填欄位 | 資料型別 | 說明 | 
| ---- | -------- | -------- | 
|   client_id   |    string      |  Client ID;裝置ID;系統中未登入user的ID, IOS：送IDFA，若無，則傳送IDFV(值後面加上-IDFV), 安卓：送AAID，若無，則傳送SSAID|
|   tid   |    string      |   在Omnisegment中組織的ID       | 
|   **選填欄位**   |          |          | 
|   app_id   |     string     |     Application ID     | 
|   app_version   |     string     |     Application Version     | 
|   app_name   |     string     |     Application Name     | 
|   currency_code   |     string     |     訂單金額的currency code     | 
|   document_location   |     string     |     trigger事件的網站url;包含parameter     | 
|   document_title   |     string     |     trigger事件的網站主旨(Document title)  | 
|   data_source   |     string     |   DataSource; "web" or "app"       | 
|   event_action   |    string      |   Event Action, Choices are "AddToCart", "Checkout", "Refund", "ClickProduct", "CompleteRegistration", "ViewContent", "Purchase", "RemoveFromCart", "Search", "AddToWishlist", "FormFillOut"       | 
|   event_category   |    string      | Event Category, Choices are "ClickFooter", "ViewContent", "Ecommerce", "CompleteRegistration", "Sort", "Filter", "ClickMenu", "Search", "FormFillOut"        | 
|   event_label   |     string     |     json format string, express value in Search & CompleteRegistration     | 
|   event_value   |     string     |     Event value     | 
|   hit_type   |    string      |   "pageview" or "event"       | 
|   products   |    list of json object    | 詳見 [Product Parameters]() |  
|   transaction_revenue   |    int      |    訂單總金額      | 
|   transaction_id   |     string     |     訂單ID     | 
|   transaction_tax   |     string     |      訂單稅額    | 
|   transaction_shipping   |     string     |     訂單運費     | 
|   transaction_couponcode   |     string     |   訂單優惠卷       | 
|   uid   |    string      |     User ID。 會員編號 ，使用者登入後須帶入     |

***

## Product Parameters
> Product parameter 以每個product object為單位傳送, 最高30組

| 必填欄位 | 資料型別 | 說明 | 
| ---- | -------- | -------- | 
|   id   |    string      |  Product ID; 商品編號; 須與ProductFeed 中的 ID欄位相同, 缺少或錯誤的ID會讓事件無法對應到正確的商品|
|   name   |    string      |  Product Name|
|   **選填欄位**   |          |          | 
|   price   |    int      |  Product Price|
|   category   |    string      |  Product Category; 商品類別|
|   brand   |    string      |  Product Brand; 商品品牌; 多品牌用逗號分開; 如"Samsung,Apple"|
|   quantity   |    string      |  Product Quantities; 商品數量; 表示訂單中此商品的個數|
|   variant   |    json formatted string      |  Product variant; 商品規格; 顏色, size, 包裝數量等等|
|   sku   |    string      |  Product sku; Product variant sku number |

***


## Request sample code

### Endpoint: https://api.omnisegment.com/api/v1/beacon/track-event/
### Request method: POST
### Request Headers: X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

***

### Product Impressions:
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "1235621.1252357334"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "web"     |
|   version   |     "2.0.4"     |
|   hit_type   |     "pageview"     |
|   products(id, name)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠"}]     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |
|   uid   |    "139540"      |
| products(brand, price, variant)  | [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}] |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "1235621.1252357334",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "data_source": "web",
    "version": "2.0.4",
    "hit_type": "pageview",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}, {"id": "DCAN8J-A90097Q9R", "name": "羅技 k65m 機械式鍵盤", "brand": "Logitech", "price": 2800, "variant": "{\"color\": \"黑色\"}", "sku": "SM21-SH-M02-RD-S-002"}],
    "currency_code": "TWD",
    "document_location": "https://test.com.tw/store/DEDI0R",
    "document_title": "iloom 全系列商品"
}'
```

***

### Product Clicks
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "ClickProduct"      |
|   event_category   |    "Ecommerce"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   products(id, name)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠"}]     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   uid   |    "139540"      |
| products(brand, price, variant)  | [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}] |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "ClickProduct",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products":{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}],
    "currency_code: "TWD",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname"
}'
```

***

### Product Detail Impressions
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "1235621.1252357334"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "web"     |
|   version   |     "2.0.4"     |
|   hit_type   |     "pageview"     |
|   products(id, name)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠"}]     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |
|   uid   |    "139540"      |
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}]     |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "1235621.1252357334",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "data_source": "web",
    "version": "2.0.4",
    "hit_type": "pageview",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠",
    "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}],
    "currency_code: "TWD",
    "document_location": "https://test.com.tw/store/DEDI0R",
    "document_title": "iloom 全系列商品"
}'
```
***

### Add / Remove from Cart
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "AddToCart" or "RemoveFromCart"      |
|   event_category   |    "Ecommerce"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   products   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}]     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   uid   |    "139540"      |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "AddToCart",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠",
    "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}],
    "currency_code: "TWD",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname"
}'
```


***

### Checkout
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "Checkout"      |
|   event_category   |    "Ecommerce"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   products(id, name)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠"}]     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   uid   |    "139540"      |
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}]     |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "Checkout",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}],
    "currency_code: "TWD",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname"
}'
```

***

### Purchases and Refund
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "Purchase" or "Refund"      |
|   event_category   |    "Ecommerce"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   products(id, name, quantity)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "quantity": 2}]     |
|   transaction_id  |     "#8701873727"     |
|   transaction_revenue   |     800     |
|   **選填欄位**   |          | 
|   currency_code   |     "TWD"     |
|   uid   |    "139540"      |
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "quantity": 2, "brand": "Logitech", "price": 800, "variant": '{"color": "藍色"}', "sku": "SM21-SH-M02-RD-S-001"}]     |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/store/DEDI0R"     |
|   document_title   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "Purchase",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "transaction_id": "#8701873727",
    "transaction_revenue": 3400,
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "quantity": 2, "brand": "Logitech", "price": 800, "variant": "{\"color\": \"藍色\"}", "sku": "SM21-SH-M02-RD-S-001"}, {"id": "DCAN8J-A90097HK2", "name": "羅技 K65M 機械式鍵盤", "quantity": 1, "brand": "Logitech", "price": 1800, "variant": "{\"color\": \"黑色\"}", "sku": "SM21-SH-M02-RD-S-001"}],
    "currency_code: "TWD",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname"
}'
```

***

### Complete Registration
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "CompleteRegistration"      |
|   event_category   |    "Ecommerce"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   event_label   |    '{"email": "fake@gmail.com", "city": "Taipei", "regType": "google"}'      |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/register"     |
|   document_title   |     "註冊或登入會員"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "CompleteRegistration",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname",
    "event_label": "{\"email\": \"fake@gmail.com\", \"city\": \"Taipei\", \"birthdayYear\": \"1996\", \"regType\": \"google\"}"
}'
```

***

### Submit a search
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "Search"      |
|   event_category   |    "Search"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   event_label   |    '{"search_string": "滑鼠"}'      |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/search?q=滑鼠"     |
|   document_title   |     "搜尋"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "Search",
    "event_category": "Search",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname",
    "event_label": "{\"search_string\": \"滑鼠\"}"
}'
```

***

### Custom Events
| 必填欄位 | 範例 |
| ---- | -------- |
|   client_id   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   data_source   |     "app"     |
|   event_action   |    "Subscribe"      |
|   event_value   |    "遊戲微服務計畫"      |
|   version   |     "2.0.4"     |
|   hit_type   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |
|   document_location   |     "https://test.com.tw/category/13"     |
|   document_title   |     "訂閱頻道"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606",
    "uid": "139540",
    "tid": "OA-xxxxxxxx",
    "event_action": "Subscribe",
    "event_value": "遊戲微服務計畫",
    "data_source": "web",
    "version": "2.0.4",
    "hit_type": "event",
    "document_location": "https://test.com.tw/category/13",
    "document_title": "訂閱頻道"
}'
```

***

### Examples For Integrate With App

- Implement a module to track user interactions
  - get device info
  - get CSRFToken and OmniSegment Api Key
  - Integrate With beacon api

```javascript
import { Platform } from "react-native";
import DeviceInfo from "react-native-device-info";
import WebAPI from "./WebAPI";

interface AnalyticsEvent {
  event_action?: string;
  event_label?: string;
  event_category?: string;
  [key: string]: string | undefined;
}

export const getDeviceInfo = async (): Promise<{
  deviceId: string | null;
  version: string;
  bundleId: string;
  appName: string;
}> => {
  let deviceId: string | null = null;

  if (Platform.OS === "ios") {
    // On iOS, use the advertising identifier (IDFA) as the device ID
    deviceId = await DeviceInfo.getUniqueId();
  } else if (Platform.OS === "android") {
    // On Android, use the Android advertising ID as the device ID
    deviceId = await DeviceInfo.getAndroidId();
  }
  const version = DeviceInfo.getVersion();
  const bundleId = DeviceInfo.getBundleId();
  const appName = DeviceInfo.getApplicationName();

  return {
    deviceId,
    version,
    bundleId,
    appName,
  };
};

export const trackAnalytics = async (
  event: AnalyticsEvent = {},
  type: string = "Event"
): Promise<void> => {
  const { deviceId, version, bundleId, appName } = await getDeviceInfo();
  const endpoint = "https://api.omnisegment.com/api/v1/beacon/track-event/";
  const user_id = "xxxxxxxxxx";
  const baseInfo = {
    version: "2.0.4",
    data_source: "app",
    tid: "OA-xxxxx",
    currency_code: "TWD",
    hit_type: type,
    client_id: deviceId!,
    app_version: version,
    app_id: bundleId,
    app_name: appName,
    document_location: base_url,
    uid: user_id,
  };

  fetch(endpoint, {
    method: "POST",
    credentials: "include",
    headers: {
      "Content-Type": "application/json",
      "X-OmniSegment-Api-Key": "xxxxxxxxxxxxxxx",
      Referer: base_url,
    },
    body: JSON.stringify({ ...baseInfo, ...event }),
  })
    .then((response) => console.log("Analytics request success"))
    .catch((error) => {
      console.error("Analytics request failed:", error);
    });
};

```
- Collect information when an event occurs and send the event

```javascript

export default class LoginView extends Component {
    componentDidMount() {
        trackAnalytics({
            event_action: 'ViewContent',
            event_category: 'Ecommerce',
            products: [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠"}],
            document_title: 'iloom 系列商品',
        }, "pageview");
    }

   private _LoginButton(): ReactNode {
        return (
            <TouchableHighlight
                style={[styles.button, { top: 32 }]}
                onPress={() => {
                    trackAnalytics({
                        event_action: 'CompleteRegistration',
                        event_category: 'CompleteRegistration',
                        event_label: JSON.stringify({
                            email: 'example@gmail.com'
                        }),
                    }, "event");
                }}
            >
                <Text style={{ textAlign: "center", color: "white" }}>登入</Text>
            </TouchableHighlight>
        )
    }
}



```

#### Examples For Integrate With WebView in App

- ios - inject JavaScript into webView
  - Use `WKUserScript` to injects script
  - reference: [WKUserScript](https://developer.apple.com/documentation/webkit/wkuserscript)

- android - inject JavaScript into webView
  - Use `evaluateJavascript` and `addJavascriptInterface` to injects script
  - reference: [evaluateJavascript](https://developer.android.com/reference/android/webkit/WebView#evaluateJavascript(java.lang.String,%20android.webkit.ValueCallback%3Cjava.lang.String%3E)), [addJavascriptInterface](https://developer.android.com/reference/android/webkit/WebView#addJavascriptInterface(java.lang.Object,%20java.lang.String))

- react native - inject JavaScript into webView
  - Use `injectedJavaScript` to injects script
  - reference: [injectedJavaScript](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Guide.md#communicating-between-js-and-native)
```javascript
import React, { Component } from 'react';
import { View } from 'react-native';
import { WebView } from 'react-native-webview';
import { getDeviceInfo } from './Sources/Modules/trackAnalytics'

export default class App extends Component {

  render() {
    const { deviceId, version, bundleId, appName } = getDeviceInfo()
    const deviceInfo = `
      window.isNativeApp = true;
      true; // note: this is required, or you'll sometimes get silent failures
      window.DeviceConfig = ${JSON.stringify({
         client_id: ${deviceId},
         app_id: ${bundleId},
         app_name: ${appName},
         app_version: ${version}
      })}
    `;
    return (
      <View style={{ flex: 1 }}>
        <WebView
          source={{
            uri: 'https://example.com/react-native-webview',
          }}
          injectedJavaScript={deviceInfo}
        />
      </View>
    );
  }
}
```
- Get DeviceInfo From WebView
  - Please verify if the WebView has also been embedded with the tracking code from Omnitag

```javascript
if (window.ReactNativeWebView) {
  const deviceInfo = (window as any).DeviceConfig
  
  /*
    Send tracking code based on web page interactions,
    the events sent from the WebView should include the app device information
  */
     window.i13n.dispatch('action', {
        I13N: {
          action: 'ClickProduct',
          ...deviceInfo,
        }
      }
}
```

#### Verify if the events have been successfully received
- Checking the customer's browsing history in Omnisegment
  - Audience page -> Audience detail page -> Audience's browsing history
<img width="923" alt="截圖 2023-07-12 下午6 02 32" src="https://github.com/beBit-tech/omnisegment-api-docs/assets/32828379/7364dd43-7212-4601-a762-fad03ecefa4e">


