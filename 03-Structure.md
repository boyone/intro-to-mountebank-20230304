# 3. Structure

1. Imposter

   1. Single Imposter

      ```json
      { // imposter
          "port": <port>,
          "protocol": <protocol>,
          "stubs": [
              { // stub
                "predicates": [

                ],
                "responses": [

                ]
              }
          ]
      }
      ```

      - Example

        ```json
        {
          "port": 8000,
          "protocol": "http",
          "stubs": [
            {
              "predicates": [
                { "equals": { "method": "GET" } },
                { "equals": { "path": "/api/v1/product/1" } }
              ],
              "responses": [
                {
                  "is": {
                    "statusCode": 200,
                    "headers": { "Content-Type": "application/json" },
                    "body": {
                      "id": 1,
                      "product_name": "Balance Training Bicycle",
                      "product_price": 119.95,
                      "product_image": "/Balance_Training_Bicycle.png"
                    }
                  }
                }
              ]
            }
          ]
        }
        ```

   2. Multiple Imposter

      ```json
      {
        "imposters": [
          { // imposter
              "port": <port>,
              "protocol": <protocol>,
              "stubs": [
                  { // stub
                    "predicates": [

                    ],
                    "responses": [

                    ]
                  }
              ]
          },
          { // imposter
              "port": <port>,
              "protocol": <protocol>,
              "stubs": [
                  { // stub
                    "predicates": [

                    ],
                    "responses": [

                    ]
                  }
              ]
          }
        ]
      }
      ```

2. Using Include with multiple imposters

   ```json
   {
       "imposters": [
           <% include stub01.json %>,
           <% include stub02.json %>
       ]
   }
   ```

3. Default Response

   ```json
   {
     "port": 8000,
     "protocol": "http",
     "defaultResponse": {
       "statusCode": 404,
       "headers": {
         "Connection": "Keep-Alive",
         "Content-Length": 0
       }
     },
     "stubs": [
       {
         "predicates": [
           { "equals": { "method": "GET" } },
           { "equals": { "path": "/api/v1/product/1" } }
         ],
         "responses": [
           {
             "is": {
               "statusCode": 200,
               "headers": { "Content-Type": "application/json" },
               "body": {
                 "id": 1,
                 "product_name": "Balance Training Bicycle",
                 "product_price": 119.95,
                 "product_image": "/Balance_Training_Bicycle.png"
               }
             }
           }
         ]
       }
     ]
   }
   ```

4. Exercise

   1. Product detail 2: `/api/v1/product/2`

      ```json
      {
        "id": 2,
        "product_name": "43 Piece dinner Set",
        "product_price": 12.95,
        "product_image": "/43_Piece_dinner_Set.png"
      }
      ```

   2. Product List: `/api/v1/product`

      ```json
      {
        "total": 3,
        "products": [
          {
            "id": 1,
            "product_name": "Balance Training Bicycle",
            "product_price": 119.95,
            "product_image": "/Balance_Training_Bicycle.png"
          },
          {
            "id": 2,
            "product_name": "43 Piece dinner Set",
            "product_price": 12.95,
            "product_image": "/43_Piece_dinner_Set.png"
          },
          {
            "id": 3,
            "product_name": "Alpha Bot",
            "product_price": 33.95,
            "product_image": "/Alpha Bot.png"
          }
        ]
      }
      ```

   3. Submit Order

      - Path: `/api/v1/order`
      - Method: `POST`
      - Response Body

        ```json
        {
          "order_id": 8004359122,
          "total_price": 14.95
        }
        ```

   4. Confirm Payment

      - Path: `/api/v1/confirmPayment`
      - Method: `POST`
      - Response Body

        ```json
        {
          "notify_message": "วันเวลาที่ชำระเงิน 1/3/2020 13:30:00 หมายเลขคำสั่งซื้อ 8004359122 คุณสามารถติดตามสินค้าผ่านช่องทาง Kerry หมายเลข 1785261900"
        }
        ```

---

[Home](README.md) [Next](04-Predicates.md)
