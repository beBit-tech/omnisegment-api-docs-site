## Description
* Import the Audience Mapping table from different providers, such as CRM, offline sources, etc.

## API URL
* `https://api.omnisegment.com/api/v1/audiences/audiences-mapping/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Required Fields
| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | **Note** |
| :------: | ------ | ------ | ------ | :------: | ------ |
| source_id | The unique ID of the client | "12345" | string | &#10004; | Represents the client's unique identifier |
| source_system | The system category | "CRM" | string | &#10004; | Indicates the category of the system (e.g., CRM, offline) |
| mapping_key | The key used to find corresponding audience in our system | "phone" | string | &#10004; | Can be one of: phone, email, line_id |
| phone/email/line_id | The value corresponding to the mapping key | "+886987654321" | string | | Required if `mapping_key` is used; should match the `mapping_key` value (e.g., if `mapping_key` is "phone", provide "phone": "+886987654321") |

## Response
```
{
    "SUCCESS": true,
    "PAYLOAD": null
}
```

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v1/audiences/audiences-mapping/?tid=OA-xxxxxx'
--header 'X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
--data-raw '{
    "source_id": "12345",
    "source_system": "CRM",
    "mapping_key": "phone",
    "phone": "+886987654321"
}'
```