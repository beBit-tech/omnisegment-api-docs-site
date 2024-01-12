
### Use Case

* 透過 [Event Tracking API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API) 追蹤APP的成效

### How to

*  OS發送的推播訊息中, [DataMessage](https://firebase.google.com/docs/cloud-messaging/concept-options) 會帶有 `omnisegment_tracking_url`, 此參數是用來追蹤此次發送與使用者後續的互動關係

*  APP應對此 `omnisegment_tracking_url` 的處理為以下兩步驟

1.   使用者點擊推播之後, 根據 `omnisegment_tracking_url` 發送一個 GET request, 此request應回傳 302 Redirect to `document_location`
2.   根據收到的 `document_location` 覆蓋瀏覽頁面應帶有的參數 `document_location`, 並送出對應的追蹤request