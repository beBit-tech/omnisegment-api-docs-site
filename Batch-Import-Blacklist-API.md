# Batch Import Blacklist API

> Maximum number of audience in a batch request should not be larger than 100.

```
POST https://api.omnisegment.com/api/v2/audiences/batch-import-blacklist/
```

## Request headers

`Content-Type: application/json`

## Request body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| tid | string | &#10004; | 組織 tid |
| api_key | string | &#10004; | 組織 api_key |
| search_key | string | &#10004; | 用來找出Audiences的key，可接受之選項有 `email`, `phone`, `line_id`, `messenger_psid`, `member_sn` |
| to_be_blacklisted | boolean | &#10004; | - 當 to_be_blacklisted 為 `true` 時，透過data找出的Audiences將會被**設為黑名單**；<br> - 當 to_be_blacklisted 為 `false` 時，透過data找出的Audiences將會被**移出黑名單**|
| data | array | &#10004; | 裝著`search_key`對應的資料，如：`search_key`為`email`，data則將為要設為/移除黑名單的Audience email。 |

## Response

Returns status `200` and a JSON object with the following information.

```json
{
    "SUCCESS": true,
    "PAYLOAD": null
}
```

## Error Response

Returns the following HTTP status code and an error response:

- `400 Bad Request`
- `403 Forbidden`

```json
# missing input data
{
    "SUCCESS": false,
    "ERR_MSG": "Missing Input Error: Missing tid, search_key, to_be_blacklisted, data",
    "ERR_TYPE_KEY": "Missing Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}

# search_key error
{
    "SUCCESS": false,
    "ERR_MSG": "Input Error: search_key should be one of ['email', 'phone', 'line_id', 'messenger_psid', 'member_sn']",
    "ERR_TYPE_KEY": "Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}

# type of data should be list
{
    "SUCCESS": false,
    "ERR_MSG": "Input Error: type of data should be list instead of <class 'dict'>",
    "ERR_TYPE_KEY": "Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}

# data exceed size limit
{
    "SUCCESS": false,
    "ERR_MSG": "Input Error: size of batch import exceeds 100",
    "ERR_TYPE_KEY": "Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}

# data is empty
{
    "SUCCESS": false,
    "ERR_MSG": "Input Error: data is empty",
    "ERR_TYPE_KEY": "Input Error",
    "ERR_MSG_KEY": null,
    "EXTRA_INFO": null,
    "INTP_KEY": {},
    "INTP_VALUE": {}
}
```

## Example

```
curl --location 'https://api.omnisegment.com/api/v2/audiences/batch-import-blacklist/' \
--header 'Content-Type: application/json' \
--data '{
    "tid": "OA-xxxxxx",
    "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "search_key": "member_sn",
    "to_be_blacklisted": true,
    "data": [
        "member_sn_1"
    ]
}'
```