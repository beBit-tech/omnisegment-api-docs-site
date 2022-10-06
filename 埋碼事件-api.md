## API URL
* `https://omnisegment.com/api/v1/tracking_event_report/?tid=OA-xxxxxx`

## Description
* 創建埋碼報告

## API Method
* `POST`

## Request Headers:
```
{"X-Omnicha-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "九月報告"`** | string | &#10004; | |
| start_datetime | 開始時間 | **`"start_datetime": "2022-09-01T00:00:00+0800"`** | string | &#10004; | |
| end_datetime | 結束時間 | **`"end_datetime": "2022-09-30T23:59:59+0800"`** | string | &#10004; | |

## Response
```
{
    "SUCCESS": True,
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
{"X-Omnicha-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Response
```
{
    "SUCCESS": True,
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
--header 'X-Omnicha-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

## Response
```
{
    "SUCCESS": True,
    "PAYLOAD": {
        "status": "SUCCESS",
        "report_url": "https://s3.amazonaws.com/media/XXX.png",
    }
}
```
| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |
