## Trriger Workflow API

### Endpoint

- `[POST] /api/v1/workflow/trigger/`

| Parameter | Description | Data type | Required | Note |
|-----------|-------------|-----------|----------|------|
| `node_id` | Target node ID to trigger workflow. | integer | &#10004; | |
| `member_sn_list` | Member SN of target audiences. | array | &#10004; | |

### Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/workflow/trigger/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "tid": "OA-c19eb6",
    "api_key": "2471880c-515c-47a5-a5ba-09c6235ff9ba",
    "node_id": 128,
    "member_sn_list": ["123", "12345"]
}'
```