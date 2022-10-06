# Report Submit API
* An API endpoint for submit report's data

## API URL
* `https://omnisegment.com/api/v1/reports/submit/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**:

  - Necessary fields: `start`, `end`

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| start | 開始時間 | **`"start": "2022-08-01"`** | string | &#10004; | |
| end | 結束時間 | **`"end": "2022-08-31"`** | string | &#10004; | |

## Note
 - 撈取時間不得超過 31 days

## Example

```
curl --location --request POST 'https://omnisegment.com/api/v1/reports/submit/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data": {
      "start": "2022-08-01",
      "end": "2022-08-31"
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