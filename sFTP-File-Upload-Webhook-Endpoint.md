## When customer upload file to sFTP success and completed, call this api to let us know.

## API URL
* `https://api.omnisegment.com/api/v1/sftp-file-upload-status/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers
* `X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

## Request body 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| file_name| File name. | **`"file_name": "71b04d6d-4389-4d07-836c-6fc2eacff8b4.csv"`** | string | &#10004; | |
| file_type| File type. | **`"file_type": "Batch PII"`** | string | &#10004; | `Batch PII`, `Batch Audiences` |
| status| The file upload status. | **`"status": "Completed"`** | string | &#10004; | `Completed`, `Running` |

### Example
```
curl --location --request POST 'https://api.omnisegment.com/api/v1/sftp-file-upload-status/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "file_name": "71b04d6d-4389-4d07-836c-6fc2eacff8b4.csv",
    "file_type": "Batch PII",
    "status": "Completed"
}'
```

