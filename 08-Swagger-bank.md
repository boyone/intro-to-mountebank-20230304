# 8. Swagger Bank

[https://github.com/Tzinov15/swagger-bank](https://github.com/Tzinov15/swagger-bank)

## Install

```sh
npm install swaggerbank
```

## Usage

```js
const SwaggerBank = require('swaggerbank');
const api = new SwaggerBank.API('<path to your swagger file>');

api.validateAPI()
.then( () => {
    api.setupMountebankImposter(3000);
})
```

## Download Imposter File

```sh
curl http://localhost:2525/imposters/:port
```

or

```sh
curl http://localhost:2525/imposters/:port > imposters.json
```

---

[Home](README.md)