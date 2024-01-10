# Get Audiences API

## Description
* Retrieve audiences who have interacted within the specified timeframe.

## API URL
* `https://api.omnisegment.com/api/v1/audiences/interactive-audiences-report/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| start_date | 開始日期 | **`"start_date": "2023-09-01"`** | string | &#10004; | |
| end_date | 結束日期 | **`"end_date": "2023-09-30"`** | string | &#10004; | |

### Note
 - start_date and end_date need to be within (Now - 30 days）

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": null
}
```

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/audiences/interactive-audiences-report/?tid=OA-xxxxxx' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
   "start_date": "2023-09-01",
   "end_date": "2023-09-30"
}'
```

-----------------------------------------------------------------

## API URL
* `https://api.omnisegment.com/api/v1/interactive-audiences-report/?tid=OA-xxxxxx`

## Description
 - 獲取一天內所有報告狀態 and report url 

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Note
 - 僅提供一天內產生的報表資料

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
    ]
}
```

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "2024_01_10_file" `** | string | |
| status | Report 狀態 | **`"status": "SUCCESS" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| file_url | Report link url | **`"file_url": "https://omnisegmeny/org/report/2024_01_10_file.json" `** | string | |
| start_date | The request data `start_date` | **`"start_date": "2023-09-01" `** | string | |
| end_date | The request data: `end_date` | **`"end_date": "2023-09-30" `** | string | |


### Report data scheme

```
{
    "member_sn": "string",
    "is_headless_acc": false,
    "tags": ["string", "string", "string"],
    "cid_objects": [
        {
            "cid": "string",
            "webpush_info":
                {
                    "endpoint": "string",
                    "p256dh": "string",
                    "auth": "string",
                    "expirationTime" : "string[datetime: UTC]"
                },
            "fcm_token": "string"
        },
        {
            "cid": "string",
            "webpush_info":
                {
                    "endpoint": "string",
                    "p256dh": "string",
                    "auth": "string",
                    "expirationTime" : "string[datetime: UTC]"
                },
            "fcm_token": "string"
        }
        // ... many cid_objects
    ]
}
```



## Example

```
curl --location --request GET 'https://api.omnisegment.com/api/v1/audiences/interactive-audiences-report/?tid=OA-xxxxxx' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```