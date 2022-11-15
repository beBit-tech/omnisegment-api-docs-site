# Import Audience Questionnaire data
* An API endpoint for import audience questionnaire data

## API URL
* `https://omnisegment.com/api/v1/questionnaire/import-audience-questionnaire-data/?tid=OA-xxxxxx`

## API Method
* `POST`

## Request Headers:
```
X-OmniSegment-Api-Key: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Parameter 內欄位說明

| **Parameter** | **Description** | **Sample** | **Data Type** | **Required** | Note |
| :------: | ------ | ------ | ------ | ------ | ------ |
| svid | 問卷 ID（unique） | **`"svid": "12345678"`** | string | &#10004; | |
| title | 問卷名稱 | **`"title": "服務滿意度問卷"`** | string | &#10004; | |
| status | 問卷填寫狀態 | **`"status": "FINISH"`** | string | &#10004; | 如果沒有特別的狀況請給 “FINISH” |
| submitTime | 問卷填寫時間 | **`"submitTime": "2022-02-16 08:30:20"`** | string | &#10004; | 如果沒帶時區會自動認定為 utc|
| alias | 問卷額外資訊，用來提供 member_sn 的，以此告知是哪個 audience 填寫的 | **`"alias": {"omniuid": ["test_sn"]}`** | dict | &#10004; | 依照不同的 audience 給予 alias value 裡的 value 就好|
| result | 該 audience 填寫問卷的結果 | **```"result": [{}, {}]```** | list | | result 資料範例請看：[example](https://github.com/beBit-tech/omnisegment-api-docs/wiki/%E5%A1%AB%E5%AF%AB%E5%95%8F%E5%8D%B7%E7%B5%90%E6%9E%9C%E7%AF%84%E4%BE%8B)|

## Example


```json
{
    'svid': '12345678',
    'title': '服務滿意度問卷',
    'status': 'FINISH',
    'submitTime': '2022-02-16 08:30:20',
    'alias': {
        'omniuid': ['test_sn']
    },
    'result': [
        {
            'subject': '單行文字',
            'type': 'TXTSHORT',
            'sn': 0,
            'answer': ['安安安'],
        },
        {
            'subject': '多行文字',
            'type': 'TXTLONG',
            'sn': 1,
            'answer': ['珍重再見...'],
        },
        {
            'subject': '單選題',
            'type': 'CHOICEONE',
            'sn': 2,
            'answer': ['A'],
        },
        {
            'subject': '多選題',
            'type': 'CHOICEMULTI',
            'sn': 3,
            'answer': ['D', '其他'],
            'otherAnswer': ['J'],
        },
        {
            'subject': '矩陣圖',
            'type': 'NEST',
            'sn': 4,
        },
        {
            'subject': '服務態度',
            'type': 'NESTCHILD',
            'sn': 5,
            'answer': ['非常滿意'],
        },
        {
            'subject': '整潔',
            'type': 'NESTCHILD',
            'sn': 6,
            'answer': ['尚可'],
        },
        {
            'subject': '數字題',
            'type': 'DIGITINPUT',
            'sn': 7,
            'answer': ['66666'],
        },
        {
            'subject': '數字滑桿',
            'type': 'DIGITSLIDE',
            'sn': 8,
            'answer': ['48'],
        },
        {
            'subject': '項目排序',
            'type': 'ITEMSORT',
            'sn': 9,
            'answer': ['b', 'a', 'c'],
        },
        {
            'subject': '星級評分',
            'type': 'RATINGBAR',
            'sn': 10,
            'answer': ['4'],
        },
        {
            'subject': '重複核選題',
            'type': 'PICKFROM',
            'sn': 11,
            'answer': ['A', 'D', '其他'],
            'otherAnswer': ['Ｊ'],
        },
        {
            'subject': '日期',
            'type': 'DATEPICKER',
            'sn': 12,
            'answer': ['2022-02-16'],
        }
    ],
}

```