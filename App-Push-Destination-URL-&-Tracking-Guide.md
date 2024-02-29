# 導轉設定

可以設定在推播訊息中，帶入其他所需的資料。
舉例：可以對 OmniSegment 發送的每則推播訊息，設定使用者點擊推播後，進入特定的 APP 頁面或顯示指定的圖片網址等等。


## Configuration Steps
### Step 1: Key Setup in OmniSegment

進入 OmniSegment 設定/推播/key設定頁面

舉例：預計新增以下兩個 key，並分別填入設定頁中
| Key           | Default Value                         |
| ------------- | ------------------------------------- |
| key=action      | name=行為              |
| key=docid | name=文章id           |
| key=url       | name=導轉連結    |

> [!NOTE]
> 其中 name 僅代表在 Omnisegment 中的別名，不會影響到推播的內容。


<img width="892" alt="截圖 2024-02-17 下午5 43 49" src="https://github.com/beBit-tech/omnisegment-api-docs/assets/32828379/391208ea-cee6-443c-a435-31c7b55eb213">

### Step.2 Content Specification

> 在編輯器中，行銷人員則可以填入此模板發送時，預期發生的行為 (action) ,文章id(docid) 的 對應內容(value)，後續讓工程師能依照設定內容，將使用者導轉到特定的 APP 頁面或發生指定行為

Specify the desired values for actions or document IDs in the OmniSegment editor. This ensures users are directed to the intended app page or action upon interacting with the notification.

以 FCM 為例，最終的推播會在 request json payload 的 "data" object 之中加入這些 custom key。

> [!NOTE]
> Ref：
https://firebase.google.com/docs/cloud-messaging/http-server-ref#downstream-http-messages-json 


FCM Payload Example (Android):
```json
{
  "registration_ids": ["1", "2", "3", ...],
  "data": {
    "title": "TITLE",
    "body": "BODY",
    "action": "popup",
    "docid": "123",
    ...
  }
}
```

FCM Payload Example (iOS):
```json
{
  "registration_ids": ["1", "2", "3", ...],
  "data": {
    "action": "popup",
    "docid": "123",
    ...
  },
  "notification": {
    "title": "TITLE",
    "body": "BODY",
  }
}
```

***
# App Push Tracking Guide

## Use Case

* 透過 [Event Tracking API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API) 追蹤APP成效
* 透過 [APP SDK](https://github.com/beBit-tech/bebit-tech-ios-app-sdk/wiki/Track-events) 追蹤APP成效

## Variables

* `destination_url`: 作為產出 `omnisegment_tracking_url` 的基礎, 表示欲追蹤的連結
* `omnisegment_tracking_url`: OS發送的推播訊息中, [DataMessage](https://firebase.google.com/docs/cloud-messaging/concept-options) 會帶有 `omnisegment_tracking_url`, 此參數是用來追蹤此次發送與使用者後續的互動關係
* `document_location`: page key / page url, 在 SDK中的名稱為 [location](https://github.com/beBit-tech/bebit-tech-ios-app-sdk/wiki/Track-events#event-properties)
* variable sample
```
destination_url: https://shop/product/123
omnisegment_tracking_url:  https://omnsegment.com/collect?v=1&t=event&dr=pn&tid=oa-319523&ea=TrackingClick&ec=Tracking&luid=35431545_135123125&tuid=1231412351_13251232_3412351
document_location: https://shop/product/123?omniclid=1325123_1251932&utm_id=omnisegment
```


## How to

* 在 OS 系統中的前置作業

1. 在 OmniSegment 設定/推播/key設定頁面 加入 key `destination_url`
2. 在 Omnisegment 推播模板編輯器中, 加入對應的 `destination_url` value

*  APP應對點擊推播後的處理為以下兩步驟

1.   使用者點擊推播之後, APP端根據 `omnisegment_tracking_url` 發送一個 GET request, response應回傳 302 Redirect to `document_location`
2.   APP端根據收到的 `document_location` 覆蓋瀏覽頁面應帶有的參數 `document_location`, 並送出對應的追蹤request(trackEvent)