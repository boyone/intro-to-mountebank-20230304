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

---

[Home](README.md) [Next](07-Proxy.md)
