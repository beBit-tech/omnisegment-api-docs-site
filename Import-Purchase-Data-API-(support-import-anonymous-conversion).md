# Import Purchase Data API

> 如需一次匯入多筆訂單資料，請參考 [Batch Import Purchase Data API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Batch-Import-Purchase-Data-API)

```
POST https://api.omnisegment.com/api/import-purchase-data/
```

## Request headers

`Content-Type: application/json`

## Request body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid，需請 beBit 團隊協助提供 |
| api_key | string | &#10004; | 組織 api_key，需請 beBit 團隊協助提供 |
| data | object | &#10004; | [data object](#data-object) |
| identifier_field | string | | 會員 mapping 的欄位(***1**) |
| is_anonymous | boolean | | 是否為匿名訂單:<br>`True` : 匯入的訂單不會包含任何顧客的資訊, `False` (預設值) : 將準備匯入的訂單視為帶有顧客資訊來處理 |
| debug_mode | string/integer | | 偵錯模式(***2**) |

***1** 指定用於查找會員的字段名稱。此欄位決定了 API 將根據哪一個字段來查找和關聯會員信息。若 Request 未帶入 `identifier_field` 則將透過 `member_sn` 進行查找及關連。 `identifier_field` 可用選項為：
 - `line_id`
 - `phone`
 - `email`
 - `messenger_psid`

***2** `debug_mode` 控制 API 錯誤時的行為，有兩種模式：
 - `0`（預設值）：資料處理會在背景執行，即使有錯誤也不會立即回報
 - `1`：資料處理會立即執行，任何錯誤都會回報給客戶端

***3** 匿名訂單：
 - 允許匯入的訂單不帶有任何顧客的資訊

***4** `is_anonymous` 告訴 API 處理的訂單是否為匿名訂單：


### data object

| Name | Type | Description | Required | 「歷史資料追蹤」節點中的應用 |
|------|------|-------------|----------|------------------------------|
| member_sn/source_id | string | 會員編號<br><br>如果有先透過 [Audience Mapping API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Audience-Mapping-API) 打資料進來，就可以提供 source_id 去找對應的會員 | &#10004; | |
| source_system | string | source_id 的來源<br><br>當提供的是 source_id 而非 member_sn 時，此欄位為必填 | | |
| datetime | string | 訂單建立日期<br><br>日期格式遵循 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)<br><br>範例: `2024-07-15T09:51:23+0800` | &#10004; | - 最後轉換時間 |
| transaction_id | string | 訂單編號 | &#10004; | |
| transaction_revenue | number | 訂單總金額 | &#10004; | - 總金額<br>- 最後一次消費金額<br>- 平均花費 |
| transaction_status | string | 訂單狀態<br><br>成功: `SUCCESS` (預設)<br>取消: `CANCEL`<br>退回: `REFUND`<br>失敗: `FAIL`<br>出貨: `SHIPPED`<br>已付款: `PAID` | | |
| quantities | integer | 訂單內的商品總數量 | | - 任一次購買產品數量 |
| products | string/object | 訂單內的商品 ID，有多個時以 `,` 分隔<br><br>提供商品 ID 時：<br>- 型別: string<br>- 範例: `P001,P002`<br><br>商品 ID 與其他系統的 ID 一起提供時：<br>- 型別: object<br>- 範例: `{"default": "P001,P002", "CRM": "CRM-P001,CRM-P002"}`<br>- 說明: 以 `P001` 為商品 ID 並將 `CRM-P001` 註記為該商品的 CRM ID，未來可透過 `CRM-P001` 來找到此商品<br><br>只提供其他系統的 ID 時：<br>- 型別: object<br>- 範例: `{"CRM": "CRM-P001,CRM-P002"}`<br>- 說明: 以 `CRM-P001` 來找到商品 `P001` | | - 購買產品名稱 |
| products_name | string | 訂單內的商品名稱，有多個時以 `,` 分隔<br><br>對應 products 的順序，只有在商品不存在時才會以提供的名稱建立商品<br><br>範例: `商品一,商品二` | | |
| products_quantity | string | 訂單內的商品數量，有多個時以 `,` 分隔<br><br>對應 products 的順序<br><br>範例: `1,2` | | |
| physical_store_name | string | 線下商店名稱 | | |
| shipping_address | object | [寄送地址](#shipping_address-object) | | |
| voucher | array | [購物金](#voucher-object) | | |
| coupon | string | 優惠名稱<br><br>範例: `coupon-ABC` | | |
| source | string | 來源名稱<br><br>範例: `Facebook` | | - 最後來源 |
| device | string | 來源裝置<br><br>可接受之選項有：`PC`, `ANDROID`, `IPHONE`, `IPAD`, `MOBILEWEB` | | |
| user_agent | string | 使用者代理，這邊可以清楚知道使用者是透過什麼工具來產生這筆訂單（電腦系統、瀏覽器、瀏覽器版本等）<br><br>範例: `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36`| | |
| 自定義欄位 | objects | 組織需另外開啟自定義欄位功能，需依照當初設定的資料型別輸入，支援的資料型別有：datetime（日期時間）, date(日期), string(文字), 數值（Decimal)。 `{"purchase_custom_text": "text", "purchase_custom_number": 1, "purchase_custom_date": "2077-01-01", "purchase_custom_datetime": "2077-01-01T00:00:00+08:00"}` <br/><br/> 請注意，訂單自定義欄位的「文字格式」最多為 256 字元。| | |


<br class="Apple-interchange-newline">

#### shipping_address object

| Name | Type | Description | Required |
|------|------|-------------|----------|
| address1 | string | 地址 1 | &#10004; |
| address2 | string | 地址 2 (外國地址之 address line 2) | |
| city | string | 城市 | |
| company | string | 運送公司 | |
| country | string | 寄送國家 | |
| country_code | string | 寄送國家編碼 | |
| latitude | string | 緯度 | |
| longitude | string | 經度 | |
| province | string | 州 | |
| province_code | string | 州碼 | |
| zip | string | 郵遞區號 | |

#### voucher object

| Name | Type | Description | Required |
|------|------|-------------|----------|
| voucher_name | string | 購物金名稱 | &#10004; |
| 自定義欄位名稱 | string | 自定義欄位 (需事先開啟**自定義欄位**功能並建立購物金自定義欄位) | |

## Response

Returns status `200` and a JSON object with the following information.

```json
{
    "SUCCESS": true,
    "PAYLOAD": null
}
```

## Error Response

Returns the following HTTP status code and an error response:

- `400 Bad Request`
- `403 Forbidden`

```json
{
    "SUCCESS": false,
    "ERR_MSG": "Missing Input Error: Request must include api_key, tid and data_content.",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}
```

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/import-purchase-data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "member_sn": "1",
      "datetime": "2020-01-01T00:00:00+0800",
      "transaction_id": "23740b4a-5872-4363-ad32-5532a89e4cb1",
      "transaction_revenue": 5000.0,
      "transaction_status": "SUCCESS",
      "quantities": 2,
      "products": "P001,P002",
      "products_name": "Product1,Product2",
      "products_quantity": "1,1",
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
      },
      "voucher": [
         {"voucher_name" : "birthday_gift"}
      ],
      "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1"
   }
}'
```