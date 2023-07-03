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
|   variant   |    string      |  Product variant; 商品規格; 顏色, size, 包裝數量等等|

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
| products(brand, price, variant)  | [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}] |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "1235621.1252357334"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "data_source": "web",
    "version": "2.0.4",
    "hit_type": "pageview",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}, {"id": "DCAN8J-A90097Q9R", "name": "羅技 k65m 機械式鍵盤", "brand": "Logitech", "price": 2800, "variant": "黑色"},]
    "currency_code: "TWD",
    "document_location": "https://test.com.tw/store/DEDI0R",
    "document_title": "iloom 全系列商品",
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
| products(brand, price, variant)  | [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}] |
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "ClickProduct",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products":{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}],
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
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}]     |
|   app_id   |     "com.company.app"     |
|   app_version   |     "1.3.2"     |
|   app_name   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/api/v1/beacon/track-event/' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "client_id": "1235621.1252357334"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "data_source": "web",
    "version": "2.0.4",
    "hit_type": "pageview",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠",
    "brand": "Logitech", "price": 800, "variant": "藍色"}]
    "currency_code: "TWD",
    "document_location": "https://test.com.tw/store/DEDI0R",
    "document_title": "iloom 全系列商品",
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
|   products   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}]     |
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "AddToCart",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠",
    "brand": "Logitech", "price": 800, "variant": "藍色"}]
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
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}]     |
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "Checkout",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "brand": "Logitech", "price": 800, "variant": "藍色"}],
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
|   products(brand, price, variant)   |     [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "quantity": 2, "brand": "Logitech", "price": 800, "variant": "藍色"}]     |
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "Purchase",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "transaction_id": "#8701873727",
    "transaction_revenue": 3400,
    "products": [{"id": "DCAN8J-A90097H2N", "name": "羅技 M221 靜音無線滑鼠", "quantity": 2, "brand": "Logitech", "price": 800, "variant": "藍色"}, {"id": "DCAN8J-A90097HK2", "name": "羅技 K65M 機械式鍵盤", "quantity": 1, "brand": "Logitech", "price": 1800, "variant": "黑色"}],
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "CompleteRegistration",
    "event_category": "Ecommerce",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname",
    "event_label": '{"email": "fake@gmail.com", "city": "Taipei", "birthdayYear": "1996", "regType": "google"}'
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "event_action": "Search",
    "event_category": "Search",
    "data_source": "app",
    "version": "2.0.4",
    "hit_type": "event",
    "app_id": "com.company.app",
    "app_version": "1.3.2",
    "app_name": "appname",
    "event_label": '{"search_string": "滑鼠"}'
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
    "client_id": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
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
