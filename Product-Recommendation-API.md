# Product Recommendation API

## Example

```
curl --location --request GET 'https://api.omnisegment.com/ai-recommendation/get-ai-recommendation/?tid=OA-xxx&cid=xxxxxx&recommend_type=user_item_embedding&num=30&product_ids=p1,p2'
```

### Query Parameters

| Parameter | Description | Required | Note |
| :-: | --- | --- | --- |
| tid | 組織 tid | &#10004; | e.g. `OA-xxxxxx` |
| cid | 裝置 ID | | 當 recommend_type 為 `user_item_embedding` 時為必填 |
| uid | 會員 ID | | 除非為訪客，否則建議都帶上 |
| recommend_type | 推薦類型 | &#10004; | Choices: `user_item_embedding`, `also_bought`, `also_viewed` |
| num | 推薦商品數量 | &#10004; | 最多 30 個 |
| product_ids | 商品的 id，會以這些商品來找相似的推薦商品 | | e.g. `product1,product2`<br>最多 10 個 |
| product_tag | 指定商品標籤 | | e.g. `product_tag1,product_tag2` |
| product_category | 指定商品類別 | | e.g. `product_category1,product_category2` |
| excluded_product_ids | 排除指定商品 | | e.g. `product1,product2`<br>最多 10 個 |
| excluded_product_tag | 排除指定商品標籤 | | e.g. `product_tag1,product_tag2` |

### Response

```
[
  {
    "product_id": 1,
    "product_name": "product1",
    "product_url": "https://xxx",
    "product_price": 123,
    "special_price": 123,
    "photo_url": "https://xxx",
    "additional_photo_url": [
      {
        "name": "100x100",
        "link": "https://xxx"
      },
      {
        "name": "200x200",
        "link": "https://xxx"
      }
    ]
  },
  {
    "product_id": 2,
    "product_name": "product2",
    "product_url": "https://xxx",
    "product_price": 321,
    "special_price": 321,
    "photo_url": "https://xxx",
    "additional_photo_url": [
      {
        "name": "100x100",
        "link": "https://xxx"
      },
      {
        "name": "200x200",
        "link": "https://xxx"
      }
    ]
  }
]
```