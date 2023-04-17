# 4. Predicates

1. Method

   ```json
   {
     "predicates": [
       {
         "equals": {
           "method": "GET"
         }
       }
     ]
   }
   ```

2. Path

   ```json
   {
     "predicates": [
       {
         "equals": {
           "path": "/api/v1/product"
         }
       }
     ]
   }
   ```

3. Header

   ```json
   {
     "predicates": [
       {
         "equals": {
           "headers": {
             "Content-Types": "application/json"
           }
         }
       },
       {
         "exists": {
           "headers": { "Authorization": true }
         }
       }
     ]
   }
   ```

4. Query Param

   ```json
   {
     "predicates": [
       {
         "equals": {
           "path": "/api/v1/product"
         }
       },
       {
         "equals": {
           "query": { "q": "robot" }
         }
       }
     ]
   }
   ```

5. Body Json

   ```json
   {
     "predicates": [
       {
         "equals": {
           "method": "POST"
         }
       },
       {
         "equals": {
           "path": "/api/v1/product"
         }
       },
       {
         "jsonpath": { "selector": "$.product_name" },
         "caseSensitive": true,
         "equals": { "body": "robot" }
       },
       {
         "jsonpath": { "selector": "$.product_price" },
         "caseSensitive": true,
         "equals": { "body": 100 }
       },
       {
         "jsonpath": { "selector": "$.product_image" },
         "caseSensitive": true,
         "equals": { "body": "/robot.png" }
       }
     ],
     "responses": [
       {
         "is": {
           "statusCode": 201,
           "headers": { "Content-Types": "application/json" }
         }
       }
     ]
   }
   ```

6. Exercise

   1. POST `/api/v1/order` with Request Body

      - request's body(json)

        ```json
        {
          "cart": [
            {
              "product_id": 2,
              "quantity": 1
            }
          ],
          "shipping_method": "Kerry",
          "shipping_address": "405/37 ถ.มหิดล",
          "shipping_sub_district": "ท่าศาลา",
          "shipping_district": "เมือง",
          "shipping_province": "เชียงใหม่",
          "shipping_zip_code": "50000",
          "recipient_name": "ณัฐญา ชุติบุตร",
          "recipient_phone_number": "0970809292"
        }
        ```

      - stub

        ```json
        {
          "predicates": [
            {
              "equals": {
                "method": "POST"
              }
            },
            {
              "equals": {
                "path": "/api/v1/order"
              }
            },
            {
              "jsonpath": { "selector": "$.cart[0].product_id" },
              "caseSensitive": true,
              "equals": { "body": "2" }
            },
            {
              "jsonpath": { "selector": "$.cart[0].quantity" },
              "caseSensitive": true,
              "equals": { "body": "1" }
            }
          ],
          "responses": [
            {
              "is": {
                "statusCode": 200,
                "headers": { "Content-Types": "application/json" },
                "body": {
                  "order_id": 8004359122,
                  "total_price": 14.95
                }
              }
            }
          ]
        }
        ```

   2. POST `/api/v1/confirmPayment`

      - Request body

        ```json
        {
          "order_id": 8004359122,
          "payment_type": "credit",
          "type": "visa",
          "card_number": "4719700591590995",
          "cvv": "752",
          "expired_month": 7,
          "expired_year": 20,
          "card_name": "Karnwat Wongudom",
          "total_price": 14.95
        }
        ```

      - Response body

        ```json
        {
          "notify_message": "วันเวลาที่ชำระเงิน 1/3/2020 13:30:00 หมายเลขคำสั่งซื้อ 8004359122 คุณสามารถติดตามสินค้าผ่านช่องทาง Kerry หมายเลข 1785261900"
        }
        ```

7. Body: Xml

   ```xml
   <items>
       <item name="TA Robot">
           <price>109.99</price>
           <location>Bangkok</location>
       </item>
       <item name="AlphaBot2">
           <price>71.50</price>
           <location>Covid-19 Zone</location>
       </item>
   </items>
   ```

   ```json
   {
     "predicates": [
       { "equals": { "method": "POST" } },
       { "equals": { "path": "/shipping" } },
       {
         "xpath": {
           "selector": "//item[@name='AlphaBot2']/location"
         },
         "equals": { "body": "Covid-19 Zone" }
       }
     ]
   }
   ```

8. Body: Text

   ```json
   {
     "predicates": [
       { "startsWith": { "body": "smart" } },
       { "contains": { "body": "alpha3" } },
       { "endsWith": { "body": "robot" } },
       { "matches": { "body": "^text to match" } },
       { "matches": { "body": ".*text to match.*" } },
       { "matches": { "body": "text to match$" } }
     ]
   }
   ```

9. Inject Predicate

   ```json
   {
      "predicates": [
          {
          "inject": "function (request) {\n if (...) {\n return true;\n }\n else {\n return false;\n}\n}"
          }
      ],
      "responses": [
          {
          "is": { ... }
          }
      ]
   }
   ```

   to

   ```json
   "predicates": [
       {
       "inject": "<%- stringify(filename, 'inject-predicate-file.js') %>"
       }
   ]
   ```

   > inject-predicate-file.js

   ```js
   function (request) {
       if (...) {
          return true;
      }
      else {
          return false;
      }
   }
   ```

---

[Home](README.md) [Next](05-Responses.md)
