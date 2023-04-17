# 6. Behaviors

```json
{
  "responses": [
    {
      "is": {},
      "_behaviors": {
        "decorate": {},
        "wait": {},
        "copy": []
      }
    }
  ]
}
```

1. decorate

   ```json
   {
     "_behaviors": {
       "decorate": "function (request, response, state, logger) { const item = JSON.parse(request.body); response.body.message = item.name"
     }
   }
   ```

2. wait

   ```json
   {
     "responses": [
       {
         "is": {
           "statusCode": 201,
           "headers": { "Content-Type": "application/json" },
           "body": { "name": "sleep" }
         },
         "_behaviors": {
           "wait": 3000
         }
       }
     ]
   }
   ```

3. copy

   ```sh
   curl http://localhost:3000/api/v1/product/1
   ```

   ```json
   {
     "protocol": "http",
     "port": 3000,
     "stubs": [
       {
         "is": {
           "body": {
             "id": "$ID",
             "name": "43 Piece Dinner Set",
             "price": 12.95
           }
         },
         "_behaviors": {
           "copy": [
             {
               "from": "path",
               "into": "$ID",
               "using": {
                 "method": "regex",
                 "selector": "\\d+$"
               }
             }
           ]
         }
       }
     ]
   }
   ```

4. lookup

   - imposter-lookup.json

     ```json
     {
       "protocol": "http",
       "port": 8000,
       "stubs": [
         {
           "predicates": [
             {
               "matches": { "path": "/api/v1/product/\\d+" },
               "caseSensitive": true
             },
             {
               "equals": {
                 "method": "GET",
                 "headers": { "Content-Type": "application/json" }
               }
             }
           ],
           "responses": [
             {
               "is": {
                 "statusCode": 200,
                 "headers": { "Content-Type": "application/json" },
                 "body": {
                   "id": "${row}['id']",
                   "product_name": "${row}['name']",
                   "product_price": "${row}[price]",
                   "product_image": "${row}[image]"
                 }
               },
               "_behaviors": {
                 "lookup": [
                   {
                     "key": {
                       "from": "path",
                       "using": {
                         "method": "regex",
                         "selector": "product/(\\w+)"
                       },
                       "index": 1
                     },
                     "fromDataSource": {
                       "csv": { "path": "products.csv", "keyColumn": "id" }
                     },
                     "into": "${row}"
                   }
                 ]
               }
             }
           ]
         }
       ]
     }
     ```

   - products.csv

     ```csv
     "id","name","price","image"
     "1","Balance Training Bicycle","119.95","/Balance Training Bicycle.png"
     "2","43 Piece Dinner Set","12.95","/43 Piece Dinner Set.png"
     "3","Alpha Bot","33.95","/Alpha Bot.png"
     ```

---

[Home](README.md) [Next](07-Proxy.md)
