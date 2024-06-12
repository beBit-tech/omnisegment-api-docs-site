## API URL
* `https://api.omnisegment.com/api/v1/tracking-event-report/?tid=OA-xxxxxx`

## Description
* 創建埋碼報告

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Query Parameter Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "九月報告"`** | string | &#10004; | |
| start_date | 開始日期 | **`"start_date": "2022-09-01"`** | string | &#10004; | |
| end_date | 結束日期 | **`"end_date": "2022-09-30"`** | string | &#10004; | |
| include_anonymous_user | 是否涵蓋匿名資料 | **`"include_anonymous_user": "true"`** | boolean | | |

### Note
 - 報表的撈取區間不得超過 31 天

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "report_id": 12345
    }
}
```
-----------------------------------------------------------------

## API URL
* `https://api.omnisegment.com/api/v1/tracking-event-report/?tid=OA-xxxxxx`

## Description
 - 獲取一天內所有埋碼報告狀態 

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Note
 - 僅提供一天內產生的報表資料，請於一天內抓取報表

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": [
         {
              "report_name": "Report1",
              "report_id": 1,
              "status": "RUNNING"
         },
         {
              "report_name": "Report2",
              "report_id": 2,
              "status": "SUCCESS"
         },
    ]
}
```

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_id | Report ID | **`"report_id": 123 `** | int | |
| report_name | Report 名稱 | **`"report_name": "八月報告" `** | string | |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |

-----------------------------------------------------------------

## API URL
* `https://api.omnisegment.com/api/v1/tracking-event-report/<id>/?tid=OA-xxxxxx`

## API Method
* `GET`

### Note
 - status 狀態為 SUCCESS，才會有 report_url 資料


## Example

```
curl --location --request GET 'https://api.omnisegment.com/api/v1/tracking-event-report/123/?tid=OA-xxxxxx' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "report_name": "Report1",
        "status": "SUCCESS",
        "report_url": "https://xxx/xxx/xxx/xxx.csv",
    }
}
```
| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "八月報告" `** | string | |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |

### Report columns

| **Column** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| member_sn | 會員編號 | **`"member_sn": "zDf11234ASd" `** | string | |
| event_time | 事件時間 | **`"event_time": "2022-08-12 23:23:45+00" `** | string | |
| event_name | 事件名稱 | **`"event_name": "AddToCart" `** | string | |
| user_engagement_duration | 停留時間(sec) | **`"user_engagement_duration": "1 day 12:00:00"`** | string | 若時間小於一天，則不會有**天**這個維度 |
| page_url | 瀏覽網域 | **`"page_url": "https://www.google.com"`** | string | |
| device | 裝置 | **`"device": "PC"`** | string | |
| session_id | 工作階段ID | **`"session_id": 5`** | integer | |
| cid | Client ID | **`"cid": "12345"`** | string | |