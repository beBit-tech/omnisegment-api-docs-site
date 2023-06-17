# Event beacon tracking API

## Event Beacons Categories

1. [Product Impressions](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#product-impressions)
> Tracking Product list. Such as Home page, Category page or Search result page.


2. [Product Clicks](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API#product-impressions)
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


## Integrate with MemberSN(uid)
**Mapping visit user with your member system.<br/> 
The membersn could be encoded or plain,<br/> 
but it must be persistent and unique.**

## Parameters
| 必填欄位 | 資料型別 | 說明 | 
| ---- | -------- | -------- | 
|   cid   |    string      |  Client ID;裝置ID;系統中未登入user的ID, IOS：送IDFA，若無，則傳送IDFV(值後面加上-IDFV), 安卓：送AAID，若無，則傳送SSAID|
|   tid   |    string      |   在Omnisegment中組織的ID       | 
|   **選填欄位**   |          |          | 
|   aid   |     string     |     Application ID     | 
|   av   |     string     |     Application Version     | 
|   an   |     string     |     Application Name     | 
|   cu   |     string     |     訂單金額的currency code     | 
|   dl   |     string     |     trigger事件的網站url;包含parameter     | 
|   dt   |     string     |     trigger事件的網站主旨(Document title)  | 
|   ds   |     string     |   DataSource; "web" or "app"       | 
|   ea   |    string      |   Event Action, Choices are "AddToCart", "Checkout", "Refund", "ClickProduct", "CompleteRegistration", "ViewContent", "Purchase", "RemoveFromCart", "Search", "AddToWishlist", "FormFillOut"       | 
|   ec   |    string      | Event Category, Choices are "ClickFooter", "ViewContent", "Ecommerce", "CompleteRegistration", "Sort", "Filter", "ClickMenu", "Search", "FormFillOut"        | 
|   el   |     string     |     json format string, express value in Search & CompleteRegistration     | 
|   ev   |     string     |     Event value     | 
|   t   |     string     |     "pageview" or "event"     | 
|   tr   |    int      |    訂單總金額      | 
|   ti   |     string     |     訂單ID     | 
|   tt   |     string     |      訂單稅額    | 
|   ts   |     string     |     訂單運費     | 
|   tcc   |     string     |   訂單優惠卷(transaction coupon code)       | 
|   uid   |    string      |     User ID。 會員編號 ，使用者登入後須帶入     |
|   v   |     string     |     api version; "2.0.4"     | 



## Product Parameters
> Product parameter 以組為單位傳送, 最高30組, 如果要傳送多組, 以pr1id=id1..., pr2id=id2...,pr3id=id3... 以此類推

| 必填欄位 | 資料型別 | 說明 | 
| ---- | -------- | -------- | 
|   pr1id   |    string      |  Product ID; 商品編號; 須與ProductFeed 中的 ID欄位相同, 缺少或錯誤的ID會讓事件無法對應到正確的商品|
|   pr1nm   |    string      |  Product Name|
|   **選填欄位**   |          |          | 
|   pr1pr   |    int      |  Product Price|
|   pr1ca   |    string      |  Product Category; 商品類別|
|   pr1br   |    string      |  Product Brand; 商品品牌; 多品牌用逗號分開; 如"Samsung,Apple"|
|   pr1qt   |    string      |  Product Quantities; 商品數量; 表示訂單中此商品的個數|
|   pr1va   |    string      |  Product variant; 商品規格; 顏色, size, 包裝數量等等|

## Product Impression Parameter
> Product Impression parameter 以組為單位傳送, 最高30組, 如果要傳送多組, 以il1pi1id=id1..., il1pi2id=id2...,il1pi3id=id3... 以此類推

| 必填欄位 | 資料型別 | 說明 | 
| ---- | -------- | -------- | 
|   il1pi1id   |    string      |  與pr1id意義相同, 只在product impression 中使用|
|   il1pi1nm   |    string      |  與pr1nm意義相同, 只在product impression 中使用|
|   **選填欄位**   |          |          | 
|   il1pi1pr   |    int      |  與pr1pr意義相同, 只在product impression 中使用|
|   il1pi1ca   |    string      |  與pr1ca意義相同, 只在product impression 中使用|
|   il1pi1br   |    string      |  與pr1br意義相同, 只在product impression 中使用|
|   il1pi1va   |    string      |  與pr1va意義相同, 只在product impression 中使用|


## Request sample code

### Endpoint: https://api.omnisegment.com/collect
### Request method: **POST**

### Product Impressions:
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "1235621.1252357334"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "web"     |
|   ea   |    "ViewContent"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   il1pi1id   |     "DCAN8J-A90097H2N"     |
|   il1pi1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |
|   uid   |    "139540"      |
|   il1pi1br   |     "Logitech"     |
|   il1pi1pr   |     800     |
|   il1pi1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "1235621.1252357334"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "ViewContent",
    "ec": "Ecommerce",
    "ds": "web",
    "v": "2.0.4",
    "t": "event",
    "il1pi1id": "DCAN8J-A90097H2N",
    "il1pi1nm": "羅技 M221 靜音無線滑鼠",
    "il1pi2id": "DCAN8J-A90097Q9R",     
    "il1pi2nm": "羅技 k65m 機械式鍵盤",    
    "cu": "TWD",
    "dl": "https//test.com.tw/store/DEDI0R",
    "dt": "iloom 全系列商品",
    "il1pi1br": "Logitech",
    "il1pi1pr": 800,
    "il1pi1va": "藍色"
    "il1pi1br": "Logitech",
    "il1pi1pr": 2800,
    "il1pi1va": "黑色"
}'
```

### Product Clicks
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "ClickProduct"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   pr1id   |     "DCAN8J-A90097H2N"     |
|   pr1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   uid   |    "139540"      |
|   pr1br   |     "Logitech"     |
|   pr1pr   |     800     |
|   pr1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "ClickProduct",
    "ec": "Ecommerce",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "pr1id": "DCAN8J-A90097H2N",
    "pr1nm": "羅技 M221 靜音無線滑鼠",
    "pr1br": "Logitech",
    "pr1pr": 800,
    "pr1va": "藍色"
    "cu": "TWD",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname"
}'
```

### Product Detail Impressions
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "1235621.1252357334"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "web"     |
|   ea   |    "ViewContent"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   il1pi1id   |     "DCAN8J-A90097H2N"     |
|   il1pi1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |
|   uid   |    "139540"      |
|   il1pi1br   |     "Logitech"     |
|   il1pi1pr   |     800     |
|   il1pi1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "1235621.1252357334"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "ViewContent",
    "ec": "Ecommerce",
    "ds": "web",
    "v": "2.0.4",
    "t": "event",
    "il1pi1id": "DCAN8J-A90097H2N",
    "il1pi1nm": "羅技 M221 靜音無線滑鼠", 
    "cu": "TWD",
    "dl": "https//test.com.tw/store/DEDI0R",
    "dt": "iloom 全系列商品",
    "il1pi1br": "Logitech",
    "il1pi1pr": 800,
    "il1pi1va": "藍色"
}'
```


### Add / Remove from Cart
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "AddToCart" or "RemoveFromCart"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   pr1id   |     "DCAN8J-A90097H2N"     |
|   pr1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   uid   |    "139540"      |
|   pr1br   |     "Logitech"     |
|   pr1pr   |     800     |
|   pr1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "AddToCart",
    "ec": "Ecommerce",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "pr1id": "DCAN8J-A90097H2N",
    "pr1nm": "羅技 M221 靜音無線滑鼠",
    "pr1br": "Logitech",
    "pr1pr": 800,
    "pr1va": "藍色"
    "cu": "TWD",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname"
}'
```


### Checkout
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "Checkout"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   pr1id   |     "DCAN8J-A90097H2N"     |
|   pr1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   uid   |    "139540"      |
|   pr1br   |     "Logitech"     |
|   pr1pr   |     800     |
|   pr1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "Checkout",
    "ec": "Ecommerce",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "pr1id": "DCAN8J-A90097H2N",
    "pr1nm": "羅技 M221 靜音無線滑鼠",
    "pr1br": "Logitech",
    "pr1pr": 800,
    "pr1va": "藍色"
    "cu": "TWD",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname"
}'
```


### Purchases and Refund
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "Purchase" or "Refund"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   pr1id   |     "DCAN8J-A90097H2N"     |
|   pr1nm   |     "羅技 M221 靜音無線滑鼠"     |
|   pr1qt   |     2     |
|   ti  |     "#8701873727"     |
|   tr   |     800     |
|   **選填欄位**   |          | 
|   cu   |     "TWD"     |
|   uid   |    "139540"      |
|   pr1br   |     "Logitech"     |
|   pr1pr   |     800     |
|   pr1va   |     "藍色"     |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/store/DEDI0R"     |
|   dt   |     "iloom⧑全系列商品"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "Purchase",
    "ec": "Ecommerce",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "ti": "#8701873727",
    "tr": 3400,
    "pr1id": "DCAN8J-A90097H2N",
    "pr1nm": "羅技 M221 靜音無線滑鼠",
    "pr1br": "Logitech",
    "pr1pr": 800,
    "pr1va": "藍色"
    "pr1qt": 2,
    "pr2id": "DCAN8J-A90097HK2",
    "pr2nm": "羅技 K65M 機械式鍵盤",
    "pr2br": "Logitech",
    "pr2pr": 1800,
    "pr2qt": 1,
    "pr2va": "黑色"
    "cu": "TWD",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname"
}'
```


### Complete Registration
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "CompleteRegistration"      |
|   ec   |    "Ecommerce"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   el   |    '{"email": "fake@gmail.com"}'      |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/register"     |
|   dt   |     "註冊或登入會員"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "CompleteRegistration",
    "ec": "Ecommerce",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname",
    "el": '{"email": "fake@gmail.com"}'
}'
```

### Submit a search
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "Search"      |
|   ec   |    "Search"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   el   |    '{"search_string": "滑鼠"}'      |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/search?q=滑鼠"     |
|   dt   |     "搜尋"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "Search",
    "ec": "Search",
    "ds": "app",
    "v": "2.0.4",
    "t": "event",
    "aid": "com.company.app",
    "av": "1.3.2",
    "an": "appname",
    "el": '{"search_string": "滑鼠"}'
}'
```


### Custom Events
| 必填欄位 | 範例 |
| ---- | -------- |
|   cid   |    "EA7583CD-A667-48BC-B806-42ECB2B48606"      | 
|   tid   |    "OA-xxxxxxxx"      |
|   ds   |     "app"     |
|   ea   |    "Subscribe"      |
|   ev   |    "遊戲微服務計畫"      |
|   v   |     "2.0.4"     |
|   t   |     "event"     |
|   **選填欄位**   |          | 
|   uid   |    "139540"      |
|   aid   |     "com.company.app"     |
|   av   |     "1.3.2"     |
|   an   |     "appname"     |
|   dl   |     "https//test.com.tw/category/13"     |
|   dt   |     "訂閱頻道"     |


```
curl --location --request POST 'https://api.omnisegment.com/collect' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cid": "EA7583CD-A667-48BC-B806-42ECB2B48606"
    "uid": "139540"
    "tid": "OA-xxxxxxxx",
    "ea": "Subscribe",
    "ev": "遊戲微服務計畫",
    "ds": "web",
    "v": "2.0.4",
    "t": "event",
    "dl": "https//test.com.tw/category/13",
    "dt": "訂閱頻道"
}'
```
