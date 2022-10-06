# Report API
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

## API URL
* `https://omnisegment.com/api/v1/reports/list/?tid=OA-xxxxxx`

## API Method
* `GET`

## Request Headers:
```
{"api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

### Note
 - 只會給一天內的 report 狀態

## Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/reports/list/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-Omnicha_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```

## Response

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

## API URL
* `https://omnisegment.com/api/v1/reports/data/?tid=OA-xxxxxxx`

## API Method
* `GET`

## Request Headers:
```
{"api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Request 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_id | Report 編號 | **`"report_id ": 123 `** | int | &#10004; | |


## Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/reports/data/?tid=OA-XXXXXXX' \
--header 'Content-Type: application/json' \
--header 'X-Omnicha_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "report_id ": 123
}'
```

## Response

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |

```json
{
    "SUCCESS": true,
    "PAYLOAD": {
        "status": "SUCCESS",
        "report_url": "https://omnicha-edm-image.s3.amazonaws.com/media/report/xxxxx.png"
    }
}
```