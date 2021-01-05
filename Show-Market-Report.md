
### Sample:
```
curl --location --request POST 'https://omnisegment.com/omnidata/show-market-report/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "start_date": "2020-11-1",
        "end_date": "2020-11-30"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx"
}'
```

### Response:
```
{
    "SUCCESS": true,
    "PAYLOAD": {
        "email": {
            "total_send": 325669,
            "total_fee": 9770.07
        },
        "sms": {
            "total_send": 13953,
            "total_fee": 12557.7
        },
        "line": {
            "total_send": 189246,
            "total_fee": 189246
        },
        "crescendo_line": {
            "total_send": 0,
            "total_fee": 0
        },
        "pn": {
            "total_send": 0,
            "total_fee": 0
        },
        "monthly_fee": 75000
    }
}
```
### Url: 

```https://omnisegment.com/omnidata/show-market-report/```

### Input:
* api_key: "xxxxxx-xxxxxxx-xxxxxx"
* tid: "OA-xxxxxxxx"
* data:
    * start_date: "[year]-[month]-[day]"
    * end_date: "[year]-[month]-[day]"

### Output:
* total_send: the total sent amount in each market channel
* total_fee: the total fee of the total sent amount multiplied by the single fee of the market channel
