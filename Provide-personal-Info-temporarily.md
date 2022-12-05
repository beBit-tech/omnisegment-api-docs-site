
## Steps of how to provide personal info temporarily

###  1. (Customer) Setup your workflow in Omnisegment.
###  2. Omnisegment send a request to customer's API endpoint during the flow.
###  3. (Customer) Upload required personal info to GCS. (3 hours timeout)
###  4. Personal info deleted after Omnisegment workflow complete.

## API URL
* `https://<customer-api-endpoint>`

## API Method
* `POST`

## request body
```json
{
 "member_raw": "<csv file in GCS>"
 "member_pii": "<Personal Info upload destination in GCS>",
 "api_key": "xxxxxx-xxxxxxx-xxxxxx",
 "credential":{
 "<short-lived-credential>"
}
}
```

## Authentication for read and upload
- **Google cloud service account short-lived credential**


## csv file description
- **Encoding**: UTF-8
- **member_raw**: csv file contains only member_sn(會員編號)
- **member_pii**:  csv file uploaded by customer, with personal info included 

## csv file format

### member_raw

|member_sn|
|---------|
|61971    |
|212806   |
|453821   |
|776281   |

### member_pii


|member_sn|name|email                               |phone                                                             |
|---------|----|------------------------------------|------------------------------------------------------------------|
|61971    |王大明|test123@gmail.com                   |+886912345678                                                     |
|212806   |王大明|test4526@gmail.com                  |+886912345678                                                     |
|453821   |王大明|test4516@gmail.com                  |+886912345678                                                     |
|776281   |王大明|test45316@gmail.com                 |+886912345678                                                     |

