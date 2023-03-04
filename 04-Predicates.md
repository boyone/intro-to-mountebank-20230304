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

4. Body: Param

   ```json
   {
     "predicates": [
       {
         "equals": {
           "query": { "q": "robot" }
         }
       }
     ]
   }
   ```

5. Body: Json

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

   ```json
   {
     "predicates": [
       {
         "jsonpath": { "selector": "$.cart[0].product_id" },
         "caseSensitive": true,
         "equals": { "body": "2" }
       }
     ]
   }
   ```

6. Body: Xml

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

7. Body: Text

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

8. Inject Predicate

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
