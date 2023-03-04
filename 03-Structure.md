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
           <% include xml.json %>,
           <% include xmlv2.json %>
       ]
   }
   ```

---

[Home](README.md) [Next](04-Predicates.md)
