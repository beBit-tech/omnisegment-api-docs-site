## When customer uploaded file to sFTP succeed and completed, call this api to let us know.

## API URL
* `https://api.omnisegment.com/api/v1/sftp-file-upload-status/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers
* `X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

## Request body 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| file_name| File name. | **`"file_name": "71b04d6d-4389-4d07-836c-6fc2eacff8b4.csv"`** | string | &#10004; | The file name need to be identifiable, maybe can use uuid. |
| file_type| File type. | **`"file_type": "Batch PII"`** | string | &#10004; | `BatchPII`, `BatchAudiences`, `BatchProduct` |
| status| The file upload status. | **`"status": "Completed"`** | string | &#10004; | `Completed`, `Running` |
| upload_id | The ID to identify which workflow's ta. | **`"upload_id": "cc411a94-2375-45fa-9b13-bc50394e791a"`** | string | | When file_type is `BatchPII` need to bring this parameter. You can get the ID from the [api](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Provide-personal-Info-temporarily). |

### Example
```
curl --location --request POST 'https://api.omnisegment.com/api/v1/sftp-file-upload-status/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "file_name": "71b04d6d-4389-4d07-836c-6fc2eacff8b4.csv",
    "file_type": "Batch PII",
    "status": "Completed",
    "upload_id": "cc411a94-2375-45fa-9b13-bc50394e791a"
}'
```

