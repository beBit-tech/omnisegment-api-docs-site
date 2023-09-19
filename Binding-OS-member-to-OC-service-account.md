# OC ServiceAccount Binding Api Documentation


* An API endpoint for binding OmniSegment member to OmniCommence service account
* Note： 此 API 僅供 member 已存在 OmniSegmemt 的狀況

## API URL
* `https://api.omnisegment.com/api/v2/audiences/oc-sa-bind/`

## API Method
* `POST`

## Required Fields
- **tid**: organization's id.

- **api_key**: organization's api key.

- **data_list**: bind info data (support multi data, max size is 50).


## data_list 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| member_sn | 會員編號 | **`"member_sn": "www123"`** | string | &#10004; | os 會員編碼 |
| account_id | 服務單位編號 | **`"account_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"`** | string |  &#10004; | 於 oc 系統後台匯出, must be uuid type |

* Note: 綁定時會自動檢查 member_sn 是否有 line_id(Line 的 UserId)，有的話才會進行綁定

## Error response type

| **Type** | **Description** | **Sample** |
| :------: | ------ | ------ |
| InputError | request data is wrong | member_sn or account_id 不符合格式 or data too much | 
| MissingInputError | request data is missing | request data 未給 account_id |
| PermissionDenied | permission denied | request data missing api key |

## Example

```
curl --location --request POST 'https://api.omnisegment.com/api/v2/audiences/oc-sa-bind/' \
--header 'Content-Type: application/json' \
--data-raw '{
   "tid": "OA-xxxxxx",
   "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
   "data_list": [
       {
          "member_sn": "www123",
          "account_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
       },
       {
          "member_sn": "qqq456",
          "account_id": "zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz"
       },
       ...
}'
```