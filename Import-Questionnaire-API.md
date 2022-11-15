# Import Questionnaire API
* An API endpoint for import questionnaire data

## API URL
* `https://omnisegment.com/api/v1/questionnaire/import-questionnaire-data/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Required Fields
- **svid**: questionnaire id.

- **title**: questionnaire title.

- **subjects**: questionnaire subjects and answer options data.

## data 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| svid | 問卷 ID（unique） | **`"id": 12345678`** | int | &#10004; | |
| title | 問卷名稱 | **`"title": "服務滿意度問卷"`** | string | &#10004; | |
| subjects | 該問卷的題目跟答案 | **```"subjects": [{}, {}]```** | list | | subjects 資料範例請看：[data](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Questionnaire-subject-and-answer-options-data)|

## Example

```
curl --location --request POST 'https://omnisegment.com/api/v1/questionnaire/import-questionnaire-data/?tid=OA-xxxxxx' \
--header 'Content-Type: application/json' \
--header 'X-OmniSegment_Api_Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--data-raw '{
   "svid": 12346,
   "title": "服務滿意度問卷",
   "subjects": [
        {
            "sn": 0,
            "text": "單行文字",
            "type": "TXTSHORT",
        },
        {
            "sn": 1,
            "text": "多行文字",
            "type": "TXTLONG",
        },
        {
            "sn": 2,
            "text": "單選題",
            "type": "CHOICEONE",
            "options": [
                {
                    "text": "A",
                },
                {
                    "text": "B",
                },
                {
                    "text": "C",
                }
            ]
        },
        {
            "sn": 3,
            "text": "多選題",
            "type": "CHOICEMULTI",
            "options": [
                {
                    "text": "D",
                },
                {
                    "text": "E",
                },
                {
                    "text": "F",
                },
                {
                    "text": "G",
                },
                {
                    "text": "H",
                },
            ]
        },
        {
            "sn": 4,
            "text": "矩陣圖",
            "type": "NEST",
            "extras": {"child_sn": [5, 6]},
            "options": [
                {
                    "text": "非常不滿意",
                },
                {
                    "text": "不滿意",
                },
                {
                    "text": "尚可",
                },
                {
                    "text": "滿意",
                },
                {
                    "text": "非常滿意",
                }
            ]
        },
        {
            "sn": 5,
            "text": "服務態度",
            "type": "NESTCHILD",
        },
        {
            "sn": 6,
            "text": "整潔",
            "type": "NESTCHILD",
        },
        {
            "sn": 7,
            "text": "數字題",
            "type": "DIGITINPUT",
        },
        {
            "sn": 8,
            "text": "數字滑感",
            "type": "DIGITSLIDE",
        },
        {
            "sn": 9,
            "text": "項目排序",
            "type": "ITEMSORT",
            "options": [
                {
                    "text": "整潔",
                },
                {
                    "text": "服務",
                },
                {
                    "text": "美味",
                }
            ]
        },
        {
            "sn": 10,
            "text": "星級評分",
            "type": "RATINGBAR",
        },
        {
            "sn": 11,
            "text": "重複核選題",
            "type": "PICKFROM",
            "optfrom": [2, 3]
        },
        {
            "sn": 12,
            "text": "日期",
            "type": "DATEPICKER",
        }
    ]
}'
```