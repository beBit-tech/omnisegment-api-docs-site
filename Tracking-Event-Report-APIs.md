## API URL
* `https://omnisegment.com/api/v1/tracking_event_report/?tid=OA-xxxxxx`

## Description
* 創建埋碼報告

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "九月報告"`** | string | &#10004; | |
| start_date | 開始日期 | **`"start_date": "2022-09-01"`** | string | &#10004; | |
| end_date | 結束日期 | **`"end_date": "2022-09-30"`** | string | &#10004; | |

## Response
```
{
    "PAYLOAD": {
        "report_id": 12345
    }
}
```
-----------------------------------------------------------------

## API URL
* `https://omnisegment.com/api/v1/tracking_event_report/?tid=OA-xxxxxx`

## Description
 - 獲取一天內所有埋碼報告狀態 

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Response
```
{
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
* `https://omnisegment.com/api/v1/tracking_event_report/<id>/?tid=OA-xxxxxx`

## API Method
* `GET`

### Note
 - status 狀態為 SUCCESS，才會有 report_url 資料


## Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/tracking_event_report/12345?tid=OA-xxxxxx' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

## Response
```
{
    "PAYLOAD": {
        "status": "SUCCESS",
        "report_url": "https://s3.amazonaws.com/media/XXX.csv",
    }
}
```
| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |

### Report columns

| **Column** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| member_sn | 會員編號 | **`"member_sn": "zDf11234ASd" `** | string | |
| event_time | 事件時間 | **`"event_time": "2022-08-12T23:23:45+0800" `** | string | |
| event_name | 事件名稱 | **`"event_name": "add_to_cart" `** | string | |
| user_engagement_duration | 停留時間(sec) | **`"user_engagement_duration": 10`** | int | |
| page_url | 瀏覽網域 | **`"page_url": "www.google.com"`** | string | |