## API URL
* `https://omnisegment.com/api/v1/create_tracking_event_report`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.
- **api_key**: organization's api key.
- **start**: report start date ("2022-09-01").
- **end**: report end date ("2022-09-30").
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
* `https://omnisegment.com/api/v1/tracking_event_report_data`

## API Method
* `GET`

## Required Fields
- **tid**: organization's id.
- **api_key**: organization's api key.
- **report_id**: report id

## Example

```
curl --location --request POST 'https://omnisegment.com/api/v1/tracking_event_report_data' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "report_id ": 123
}'
```

## Response
```
{
    "SUCCESS": True,
    "PAYLOAD": {
        "status": "SUCCESS",
        "content":{
            "id": <report_id>,
            "creation_time": "2022-10-06T10:12:28.147958+0800",
            "start_date": "2022-09-01",
            "end_date": "2022-09-30",
            "report_content": [
                {
                    "member_sn": 34567,
                    "creation_time": "2022-10-06T10:12:28.147958+0800",
                    "event_name": "add_to_cart",
                    "page_url": "https://www.panasonic.com/tw/",
                    "time_stayed": 180,
               },
               {
                    "member_sn": 12345,
                    "creation_time": "2022-10-05T10:12:28.147958+0800",
                    "event_name": "product_impression",
                    "page_url": "https://www.panasonic.com/tw/",
                    "time_stayed": 50,
               }
            ],
        }
    }
}
```

