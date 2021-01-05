# show_market_report


### sample:
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
### url: 

```https://omnisegment.com/omnidata/show-market-report/```

### Input:
* api_key: xxxxxx-xxxxxxx-xxxxxx
* tid: OA-xxxxxxxx
* start_date: [year]-[month]-[day]
* end_date: [year]-[month]-[day]
------
