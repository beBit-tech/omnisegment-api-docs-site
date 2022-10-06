# Report Submit API
* An API endpoint for submit report's data

## API URL
* `https://omnisegment.com/api/v1/reports/submit/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data**: product guarantee data content.

  - Necessary fields: `start_datetime `, `end_datetime `

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| start_datetime | 開始時間 | **`"start_datetime ": "2022-08-01T00:00:00+08:00"`** | string | &#10004; | |
| end_datetime | 結束時間 | **`"end_datetime ": "2022-08-31T23:59:59+08:00"`** | string | &#10004; | |

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
      "start_datetime": "2022-08-01T00:00:00+08:00",
      "end_datetime": "2022-08-31T23:59:59+08:00"
   }
}'
```