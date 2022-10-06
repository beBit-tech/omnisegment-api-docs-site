# Create Report API
* An API endpoint for submit report's data

## API URL
* `https://omnisegment.com/api/v1/reports/create/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers:
```
{"api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Request 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "八月報告"`** | string | &#10004; | |
| start_datetime | 開始時間 | **`"start_datetime": "2022-08-01T00:00:00+0800"`** | string | &#10004; | |
| end_datetime | 結束時間 | **`"end_datetime": "2022-08-31T23:59:59+0800"`** | string | &#10004; | |

### Note
 - 撈取時間不得超過 31 days

## Example

```
curl --location --request POST 'https://omnisegment.com/api/v1/reports/create/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-Omnicha_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
      "report_name": "八月報告",
      "start_datetime": "2022-08-01T00:00:00+0800",
      "end_datetime": "2022-08-31T23:59:59+0800"
   }
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