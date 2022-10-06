## API URL
* `https://omnisegment.com/api/v1/tracking_event_report`

## API Method
* `POST`

## Request Headers:
```
{"X-Omnicha-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Required Fields
- **tid**: organization's id.
- **start**: report start date ("2022-09-01T00:00:00+0800").
- **end**: report end date ("2022-09-30T23:59:59+0800").
- **report_name**: report name

## Response
```
{
    "SUCCESS": True,
    "PAYLOAD": {"report_id": 12345}
}
```
-----------------------------------------------------------------

## API URL
* `https://omnisegment.com/api/v1/tracking_event_report/`

## API Method
* `GET`

## Request Headers:
```
{"X-Omnicha-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Required Fields
- **tid**: organization's id.

## Response
```
{
    "SUCCESS": True,
    "PAYLOAD": [
         {
              "name": "Report1",
              "id": 1,
         },
         {
              "name": "Report2",
              "id": 2,
         },
    ]
}
```
-----------------------------------------------------------------

## API URL
* `https://omnisegment.com/api/v1/tracking_event_report/<id>`

## API Method
* `GET`

## Request Headers:
```
{"X-Omnicha-Api-Key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```

## Required Fields
- **tid**: organization's id.

## Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/tracking_event_report/12345?tid="OA-xxxxxx"' \
--header 'X-Omnicha-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

## Response
```
{
    "SUCCESS": True,
    "PAYLOAD": {
        "status": "SUCCESS",
        "file_url": "https://s3.amazonaws.com/media/XXX.png",
        "failed_reason": "",
    }
}

{
    "SUCCESS": True,
    "PAYLOAD": {
        "status": "RUNNING",
        "file_url": "",
        "failed_reason": "",
    }
}

{
    "SUCCESS": True,
    "PAYLOAD": {
        "status": "FAIL",
        "file_url": "",
        "failed_reason": "",
    }
}
```

