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

## Run Swagger-ui in Local machine

1. Clone Swagger-ui

    ```sh
    git clone https://github.com/swagger-api/swagger-ui.git --depth 1
    ```

2. Change Directory to `swagger-ui`

    ```sh
    cd swagger-ui
    ```

3. Create `examples` Directory in `dev-helpers` directory

    ```sh
    mkdir dev-helpers/examples
    ```

4. Copy `swagger files` to `dev-helpers/examples`
5. Run `swagger-ui`

    ```sh
    // npm install
    npm run dev
    ```

---

[Home](README.md)