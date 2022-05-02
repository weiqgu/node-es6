# Setting up node js express with ES6

```
npm install --save-dev @babel/cli @babel/core @babel/preset-env
npm install --save-dev nodemon
npm install --save-dev rimraf
npm install eslint --save-dev

# setup eslint config
npm init @eslint/config

npm install --save-dev eslint-config-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-n
npm install --save-dev babel-eslint
```

```
touch .babelrc
```

```
{
  "presets": [
    ["@babel/env", {
      "targets": {
        "node": "current"
      }
    }]
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties",
    "@babel/plugin-proposal-object-rest-spread"
  ]
}

{
  "presets": [
    "@babel/preset-env"
  ]
}
```

```
  "scripts": {
    "clean": "rimraf -rf .build/*",
    "clean:installDependencies": "rimraf -rf ./node_modules",
    "build:dev": "babel src --source-maps --copy-files --out-dir .build",
    "start:dev": "npm run clean && npm run build:dev",
    "lint": "./node_modules/.bin/eslint src/**",
    "lint:test": "./node_modules/.bin/eslint test/**",
    "lint:fix": "./node_modules/.bin/eslint src/** --fix",
    "lint:test:fix": "./node_modules/.bin/eslint test/** --fix",
    "start": "npm run start:dev && node ./.build/server.js",
    "docker:clean": "npm run clean:installDependencies",
    "test": "npm run test:coverage:clean && cross-env NODE_ENV=test nyc --reporter=html --reporter=text ./node_modules/mocha/bin/mocha --require @babel/register test/**",
    "test:coverage": "nyc report --reporter=text-lcov | coveralls",
    "test:coverage:clean": "rimraf -rf coverage/*"
  },

scripts": {
    "build": "babel index.js -d dist",
    "start": "npm run build && node dist/index.js"
  }

"scripts": {
    "build": "babel index.js -d dist",
    "start": "npm run build && nodemon dist/index.js"
  }  
```
