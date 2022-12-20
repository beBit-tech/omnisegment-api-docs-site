
## Steps of how to provide personal info temporarily

###  1. (Customer) Setup your workflow in Omnisegment.
###  2. Omnisegment send a request to customer's API endpoint during the flow.
###  3. (Customer) Upload required personal info to sFTP. (3 hours timeout)
###  4. Send a request to [webhook](https://github.com/beBit-tech/omnisegment-api-docs/wiki/sFTP-File-Upload-Webhook-Endpoint) to let us know file upload completed.
###  5. Personal info deleted after Omnisegment workflow complete.

## API URL
* `https://<customer-api-endpoint>`

## API Method
* `POST`

## request headers
* `X-Omnisegment-Signature: <signature>`
 >  You need to verify signature to confirm that the request was sent from the OmniSegment.
### code example in python
```
import base64
import hashlib
import hmac
import json

api_key = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
body = {"member_raw": "/path/to/sFTP/member_raw_file.csv", "member_pii": "/path/to/sFTP/member_pii_file.csv", "upload_id": "cc411a94-2375-45fa-9b13-bc50394e791a"} # the request body
hash = hmac.new(str(api_key).encode('utf-8'), json.dumps(body, sort_keys=True).encode('utf-8'), hashlib.sha256).digest()
signature = base64.b64encode(hash)

# Compare X-Omnisegment-Signature request header and the signature
```

## request body
```json
{
 "member_raw": "<csv file in sFTP>"
 "member_pii": "<Personal Info upload destination in sFTP>",
 "upload_id": "<The memeber_raw unique id in sFTP>"
}
```


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

