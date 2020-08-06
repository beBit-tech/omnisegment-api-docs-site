key的範例

* api key : xxxxxx-xxxxxxx-xxxxxx 
* tid : OA-xxxxxxxx 

example:

```
curl --location --request POST 'https://omnisegment.com/ma_audience/import-audience/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "data": {
        "member_sn": "1",
        "name": "Eason Lee",
        "first_name": "Eason",
        "last_name": "Lee",
        "email": "eason@demo",
        "phone": "+886912345678",
        "member_level": "1",
        "sex": "female",
        "birthday": "1990-01-01",
        "register_date": "2020-6-4",
        "facebook_id": "facebook_id",
        "google_id": "google_id",
        "line_id": "line_id",
        "fcm_token": "fcm_token",
        "apns_token": "apns_token",
        "is_subscriber": "true",
        "is_active": true,
        "crm_pk": "1",
        "tags": "tag_a,tag_b,tag_c",
        "sites": "site_a,site_b,site_c"
    },
    "tid": "OA-xxxxxxxx",
    "api_key": "xxxxxx-xxxxxxx-xxxxxx"
}'
```