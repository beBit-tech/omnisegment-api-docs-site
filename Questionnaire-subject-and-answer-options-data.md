
# 題目類別和答案格式

> answer options 如果為空代表不用給

| **Subject Type** | **Description** |Answer options required| **Sample**                      | **Data Type** | Note |
|:----------------:| --------------- | --- | ------------------------------- | ------------- | ---- |
|     TXTSHORT     | 單行文字        |     | ![](https://i.imgur.com/7ifkqwX.png)| dict           |      |
|     TXTLONG      | 多行文字        |     | ![](https://i.imgur.com/iKMfNx4.png)| dict        |      |
|    CHOICEONE     | 單選題          | &#10004; | ![](https://i.imgur.com/A5WQreO.png) | dict          |      |
|    CHOICEMULTI     | 多選題          | &#10004; | ![](https://i.imgur.com/iyaSdVN.png) | dict          |      |
|    NEST     | 矩陣題          | &#10004; | ![](https://i.imgur.com/mPJXXbH.png) | dict  | 矩陣題的題目會是最外層的，以此範例為例就是 ”矩陣題“，需要給答案選項（非常不滿意、不滿意...），並且一定要給 extras 說明子類別的 sn 為哪些|
|    NESTCHILD     | 矩陣題子類別          | | ![](https://i.imgur.com/mPJXXbH.png)  | dict          | 矩陣題子類別的題目會是內層的，以此範例為例就是 “服務態度” “整潔”，不用額外再給答案選項 |
|    DIGITINPUT     | 數字題目          | | ![](https://i.imgur.com/lufdi35.png)  | dict          |      |
|    DIGITSLIDE     | 數字滑桿          | | ![](https://i.imgur.com/jcJMRA4.png)  | dict          |      |
|    ITEMSORT     | 項目排序          | &#10004; | ![](https://i.imgur.com/klfWRgr.png)  | dict          |      |
|    RATINGBAR     | 星級評分          | | ![](https://i.imgur.com/lUtIAuA.png)  | dict          |      |
|    PICKFROM     | 重複核選題          | &#10004; | ![](https://i.imgur.com/ErTnA4S.png)  | dict          | 題目選項只能來自單選 or 多選，以此範例為例就是來自上面的單選跟多選，須額外給 optfrom 說明選項來自哪幾個 sn|
|    DATEPICKER     | 日期          | | ![](https://i.imgur.com/MoJosC3.png)  | dict          |      |


> 以下為各題型資料範例
> sn 為該問卷題目的唯一編號 type (int)
```json!
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
```