# Interaction Report APIs
* API endpoints for report's data

------------------
# Create Report

## API URL
* `https://api.omnisegment.com/api/v1/interaction-report/?tid=OA-xxxxxx`

## Description
 - 創建 interaction report endpoint

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Request 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "八月報告"`** | string | &#10004; | |
| start_date | 開始日期 | **`"start_date": "2022-08-01"`** | string | &#10004; | |
| end_date | 結束日期 | **`"end_date": "2022-08-31"`** | string | &#10004; | |

### Note
 - 撈取時間不得超過 31 days

### Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/interaction-report/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "report_name": "八月報告",
    "start_date": "2022-08-01",
    "end_date": "2022-08-31"
}'
```

## Response

```json
{
    "SUCCESS": true,
    "PAYLOAD": {
        "report_id": 123
    }
}
```

-----------------------
# List Report

## API URL
* `https://api.omnisegment.com/api/v1/interaction-report/?tid=OA-xxxxxx`

## Description
 - 獲取一天內 reports 狀態 endpoint

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Note
 - 只會給一天內的 report 狀態

### Example

```
curl --location --request GET 'https://api.omnisegment.com/api/v1/interaction-report/?tid=OA-xxxxxx' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```

## Response
| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_id | Report ID | **`"report_id": 123 `** | int | |
| report_name | Report 名稱 | **`"report_name": "八月報告" `** | string | |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |



### Example
```json
{
    "SUCCESS": true,
    "PAYLOAD": [
        {
            "report_id": 123,
            "report_name": "八月報告",
            "status": "RUNNING"
        },
        {
            "report_id": 124,
            "report_name": "九月報告",
            "status": "SUCCESS"
        },
        ...
    ]
}
```

------------------------
# Retrieve Report

## API URL
* `https://api.omnisegment.com/api/v1/interaction-report/<id>/?tid=OA-xxxxxxx`

## Description
 - 獲取該 report 產生的 url endpoint

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Request

### Example

```
curl --location --request GET 'https://api.omnisegment.com/api/v1/interaction-report/123/?tid=OA-XXXXXXX' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```

## Response

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "八月報告"`** | string | &#10004; | |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |

### Note
 - report 狀態為 SUCCESS，才會有 url 資料

### Example

```json
{
    "SUCCESS": true,
    "PAYLOAD": {
        "report_name": "八月報告",
        "status": "SUCCESS",
        "report_url": "https://xxx/xxx/xxx/xxx/xxx.csv"
    }
}
```

### Report columns

| **Column** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| member_sn | 會員編號 | **`"member_sn": "abcdefg" `** | string | |
| channel_type | 頻道編號 | **`"channel_type": "EMAIL" `** | string | |
| template_id | 素材 ID | **`"template_id": 111 `** | int | |
| template_name | 素材名稱 | **`"template_name": "八月壽星" `** | string | |
| delivery_time | 發送時間 | **`"delivery_time": "2022-08-12 23:23:45+00" `** | string | |
| template_title | 主旨 | **`"template_title": "恭喜您生日～" `** | string | 只有 channel_type 是 EMAIL 時才會有這資料 |
| open | 是否開啟 | **`"open": true `** | bool | 只有 channel_type 是 EMAIL 時才會有這資料 |
| open_time | 開啟時間 | **`"open_time": ["2022-08-12 23:23:45+00"] `** | list with string | 只有 channel_type 是 EMAIL 時才會有這資料，若沒有 `open_time` 資料時為 `null` |
| click | 是否點擊 | **`"click": true `** | bool | |
| click_event | 點擊事件 | **`"click_event": [{"click_time": "2022-08-12 23:24:13+00", "click_link": "https://do-not-click"}]`** | list with dict object | `click_time` (點擊時間), `click_link` (點擊連結)，若沒有 `click_event` 資料時為 `null` |
| email_status | email最後狀態 | **`"email_status": "sent" `** | string | 只有 channel_type 是 EMAIL 時才會有這資料。 包含 `sent, open, click, bounce, blocked, unsub, spam`|

#### Email status

| **email_status** | **Description** |
| :------: | ------ | 
| sent | Message has been successfully delivered to the receiving server. |
| open | Recipient has opened the HTML message. Open Tracking needs to be enabled for this type of event. |
| click | Recipient clicked on a link within the message. Click Tracking needs to be enabled for this type of event. |
| bounce | Receiving server could not or would not accept mail to this recipient permanently. If a recipient has previously unsubscribed from your emails, the message is dropped. |
| blocked | Receiving server could not or would not accept the message temporarily. If a recipient has previously unsubscribed from your emails, the message is dropped. |
| unsub | Recipient clicked on the 'Opt Out of All Emails' link (available after clicking the message's subscription management link). Subscription Tracking needs to be enabled for this type of event. |
| spam | Recipient marked message as spam. |
