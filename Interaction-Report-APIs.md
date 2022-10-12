# Interaction Report APIs
* API endpoints for report's data

------------------
# Create Report

## API URL
* `https://omnisegment.com/api/v1/interaction_report/?tid=OA-xxxxxx`

## Description
 - 創建 report endpoint

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Request 欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| report_name | Report 名稱 | **`"report_name": "八月報告"`** | string | &#10004; | |
| start_date | 開始日期 | **`"start_date": "2022-08-01"`** | string | &#10004; | |
| end_date | 結束日期 | **`"end_date": "2022-08-31"`** | string | &#10004; | |

### Note
 - 撈取時間不得超過 31 days

### Example

```
curl --location --request POST 'https://omnisegment.com/api/v1/interaction_report/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
    "report_name": "八月報告",
    "start_datetime": "2022-08-01T00:00:00+0800",
    "end_datetime": "2022-08-31T23:59:59+0800"
}'
```

## Response

```json
{
    "PAYLOAD": {
        "report_id": 123
    }
}
```

-----------------------
# List Report

## API URL
* `https://omnisegment.com/api/v1/interaction_report/?tid=OA-xxxxxx`

## Description
 - 獲取一天內 reports 狀態 endpoint

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Note
 - 只會給一天內的 report 狀態

### Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/interaction_report/?tid=OA-xxxxxx' \
--header 'X-OmniSegment_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```

## Response
| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| report_id | Report ID | **`"report_id": 123 `** | int | |
| report_name | Report 名稱 | **`"report_name": "八月報告" `** | string | |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |



### Example
```json
{
    "PAYLOAD": [
        {
            "report_id": 123,
            "report_name": "八月報告",
            "status": "RUNNING"
        },
        {
            "report_id": 124,
            "report_name": "九月報告",
            "status": "SUCCESS"
        },
        ...
    ]
}
```

------------------------
# Retrieve Report

## API URL
* `https://omnisegment.com/api/v1/interaction_report/:id/?tid=OA-xxxxxxx`

## Description
 - 獲取該 report 產生的 url endpoint

## API Method
* `GET`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Request

### Example

```
curl --location --request GET 'https://omnisegment.com/api/v1/interaction_report/123/?tid=OA-XXXXXXX' \
--header 'X-OmniSegment_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
```

## Response

| **Parameter** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| status | Report 狀態 | **`"status": "RUNNING" `** | string | 包含 `RUNNING, SUCCESS, FAIL` |
| report_url | Report URL |  | string |  |

### Note
 - report 狀態為 SUCCESS，才會有 url 資料

### Example

```json
{
    "PAYLOAD": {
        "status": "SUCCESS",
        "report_url": "https://omnisement-edm-image.s3.amazonaws.com/media/report/xxxxx.png"
    }
}
```

### Report columns

| **Column** | **Description** | **Sample** | **Data Type** | Note |
| :------: | ------ | ------ | ------ | ------ |
| member_sn | 會員編號 | **`"member_sn": "zDf11234ASd" `** | string | |
| channel_type | 頻道編號 | **`"channel_type": "EMAIL" `** | string | |
| template_id | 素材 ID | **`"template_id": 111 `** | int | |
| template_name | 素材名稱 | **`"template_name": "八月壽星" `** | string | |
| title | 主旨 | **`"title": "恭喜您生日～" `** | string | 只有 channel_type 是 EMAIL 時才會有這資料 |
| open | 是否開啟 | **`"open": true `** | bool | 只有 channel_type 是 EMAIL 時才會有這資料 |
| open_time | 開啟時間 | **`"open_time": "2022-08-12T23:23:45:0800" `** | string | 只有 channel_type 是 EMAIL 時才會有這資料 |
| click | 是否點擊 | **`"click": true `** | bool | |
| click_time | 點擊時間 | **`"click_time": "2022-08-12T23:24:13:0800" `** | string | |
| click_link | 點擊連結 | **`"click_link": "`[https://do-not-click](https://www.youtube.com/watch?v=dQw4w9WgXcQ)`" `** | string | |