# Get Report Data API
* An API endpoint for get report's data

## API URL
* `https://omnisegment.com/api/v1/reports/data/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**: Get Report data content.

  - Necessary fields: `report_id `

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_id | Report 編號 | **`"report_id ": 123 `** | int | &#10004; | |

## Example

```
curl --location --request POST'https://omnisegment.com/api/v1/reports/data/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "report_id ": 123
   }
}'
```

## Response

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| content | Report 內容 |  | list | title，is_open、open_time 只有在 channel_type 是 EMAIL 時才會有資料<br> |

```json
{
    "SUCCESS": true,
    "PAYLOAD": {
        "status": "SUCCESS"
        "content ": [
            {
                "member_sn": "XD1sfasf1233",
                "channel_type": "EMAIL",
                "template_name": "8月壽星",
                "title": "恭喜8月份壽星~",
                "is_open": true,
                "open_time": "2022-08-16T15:23:45+08:00",
                "is_click": true,
                "click_time": "2022-08-18T21:12:34+08:00",
                "click_link": "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
            },
            ...
        ]
    }
}
```
