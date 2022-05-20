# serverless-ts-webpack-absolute-path-boilerplate
Boilerplate of `Serverless X Aws Lambda` function with `Typescript`, `Webpack` and `Aliased absolute path`.



## Installation
```bash
git clone https://github.com/dannylisa/serverless-ts-webpack-absolute-path-boilerplate [your_project_name]
```
```bash
npm install
```

## Config
Set your own environment variables.

1. Edit `config/config.js`
```js
module.exports.CONFIG = (serverless) => ({
    dev: {
        PRIVATE_KEY: "EXAMPLE_PRIVATE_KEY"
    },
    prod: {
        PRIVATE_KEY: "EXAMPLE_PRIVATE_KEY"
    }
});
```

2. Edit `serverless.yml`
```yml
...
provider:
  name: aws
  runtime: nodejs14.x
  stage: ${opt:stage, 'dev'}
  environment:
      STAGE: ${self:provider.stage}
      PRIVATE_KEY: ${self:custom.CONFIG.${self:custom.STAGE}.PRIVATE_KEY} 
...
```
3. Add to `.gitignore`
```
config/config.js
```

## Aliased absolute path
1. Edit `webpack.config.js`
```js
...
resolve: {
    extensions: ['.mjs', '.json', '.ts'],
    symlinks: false,
    cacheWithContext: false,
    alias: {
        '@': path.resolve(__dirname, './src')
    }
},
...
```

2. Edit `tsconfig.json`
```
...
"baseUrl": "./src",
"paths": {
    "@/*": ["./*"]
}
...
```
