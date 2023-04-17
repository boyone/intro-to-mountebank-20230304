# 5. Responses

```json
{
  "responses": [
    {
      "is": {
        "statusCode": 200,
        "headers": { "Content-Types": "application/json" },
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
```

1. Stringify

   ```json
   {
     "responses": [
       {
         "is": {
           "statusCode": 200,
           "body": "<%- stringify(filename, 'resp.json') %>",
           "headers": {
             "Content-Type": "application/json"
           }
         }
       }
     ]
   }
   ```

   > resp.json

   ```json
   {
     "id": 1,
     "product_name": "Balance Training Bicycle",
     "product_price": 119.95,
     "product_image": "/Balance_Training_Bicycle.png"
   }
   ```

2. Inject

   ```json
   {
     "responses": [
       {
         "inject": "function (request) { if (request.path.indexOf('/items/1') === 0) { return { statusCode: 404 }; } }"
       }
     ]
   }
   ```

   - inject with stringify

     ```json
     "responses": [
                     {
                         "inject": "<%-stringify(filename, 'validateItem.js') %>"
                     }
                 ],
     ```

   - validateItem.js

     ```js
     function (request) {
         if (request.path.indexOf('/items/1') === 0) {
             return { statusCode: 404 };
         }
     }
     ```

## Exercise Add timestamp to json response body

- Submit Order & Confirm Payment
- timestamp.js

  ```js
  function (request, response, logger) {
       const item = JSON.parse(request.body);
       response.body.timestamp = new Date().toString();
  }
  ```

---

[Home](README.md) [Next](./06-Behaviors.md)
