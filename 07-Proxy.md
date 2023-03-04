# 7. Proxy

## Mode

- `proxyOnce`: ensures that the same request (defined by the predicates) is never proxied twice. mountebank only records one response for each request, and automatically replays that response the next time the request predicates match.
- `proxyAlways`: All calls will be proxied, allowing multiple responses to be saved for the same logical request. You have to explicitly tell mountebank to replay those responses.
- `proxyTransparency`: All calls will be proxied, but will not be recorded.

1. http proxy

   ```json
   {
       "port": <port>,
       "protocol": <protocol>,
       "stubs": [
           {
             "responses": [
                {
                    "proxy": {
                        "to": "http://161.35.76.206",
                        "mode": <mode>
                    }
                }
             ]
           }
       ]
   }
   ```

   ```sh
   curl --location 'http://161.35.76.206' \
   --header 'Content-Type: application/json' \
   --header 'Accept: application/json'
   ```

2. https proxy

   ```json
   {
       "port": <port>,
       "protocol": <protocol>,
       "stubs": [
           {
             "responses": [
                {
                    "proxy": {
                        "to": "https://dminer.in.th",
                        "mode": <mode>
                    }
                }
             ]
           }
       ]
   }
   ```

   ```sh
   curl --location 'https://dminer.in.th/api/v1/product/2' \
   --header 'Content-Type: application/json' \
   --header 'Accept: application/json'
   ```

3. predicateGenerators

   The `predicateGenerators` field defines the template for the generated predicates.

   ```json
   {
       "port": <port>,
       "protocol": <protocol>,
       "stubs": [
           {
           "responses": [
               {
                   "proxy": {
                       "to": "https://dminer.in.th",
                       "mode": <mode>,
                       "predicateGenerators": [
                           {
                               "matches": {
                                   "path": true,
                                   "query": true,
                                   "headers": true,
                               }
                           },
                           {
                               "matches": {
                                   "body": true
                               }
                           }
                       ]
                   }
               }
           ]
           }
       ]
   }
   ```

4. Save

   The `save` command is a convenient command line mechanism to save the configuration into a file.

   ```sh
   mb save --removeProxies
   ```

   > by default mountebank cli will create file name mb.json

   ```sh
   mb save --savefile saved.json --removeProxies
   ```

    > mountebank cli will create file name saved.json the remove proxies

   ```sh
   mb save --port 2525 --savefile saved.json --removeProxies
   ```

   > mountebank cli will call to the port of the running the mountebank server create file name saved.json the remove proxies

5. Replay

   The `replay` command is a convenience that removes all proxies, effectively switching from record mode to replay mode.

   ```sh
   mb replay
   ```

---

[Home](README.md)
