# ReactAppConfiguration
Guide to configure react app. 
Stack:
1. [Typescript](#typesctipt)
2. [Redux](#Redux)
3. [TSLint](#TSLint)
4. [Prettier](#Prettier)
5. [Styles + Bootstrap](#Styles)
6. [Translations](#Translations)
7. [Fetching data](#Fetching-data)
8. [Router](#Router)
9. [Tests](#Tests)

## Basic build setup

1. Update `create-react-app`
```
# run uninstall scrpt to uninstall current version of CRA 
npm uninstall -g create-react-app
# or
yarn global remove create-react-app

# install latest version of CRA 
npm install -g create-react-app
#or
yarn global add create-react-app
```
2. Run `create-react-app`
```
npx create-react-app my-app
# or
npx create-react-app my-app --template typescript
```
3. `cd ./my-app`
4. `npm install`
5. `npm start`

For more info visit https://facebook.github.io/create-react-app/docs/getting-started

## Typesctipt

1. Install typescript and types for default packages.  
```
npm install typescript @types/node @types/react @types/react-dom @types/jest --save-dev
# or  
yarn add typescript @types/node @types/react @types/react-dom @types/jest --dev
```
2. rename your `.js` files to `.tsx` in case components or `.ts` in case pure typescript files

For more info visit https://create-react-app.dev/docs/adding-typescript/

## Redux and Saga
1. `npm install redux redux-saga react-redux`
2. `npm install @types/react-redux --save-dev`

## ESLint

Why ESLint?
https://eslint.org/blog/2019/01/future-typescript-eslint

1. `npm install @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb eslint-plugin-react eslint-plugin-react-redux eslint-plugin-redux-saga eslint-plugin-react-hooks --save-dev`
2. create `.eslintrc.json` file for configuration
```
{
  "extends": [
    "airbnb",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-redux/recommended",
    "plugin:redux-saga/recommended"
  ],
  "plugins": ["react-hooks", "react-redux", "redux-saga", "@typescript-eslint"],
  "env": {
    "browser": true,
    "jasmine": true,
    "jest": true
  },
  "rules": {
    "react/jsx-handler-names": 1,
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "redux-saga/no-unhandled-errors": "off",
    "react-redux/prefer-separate-component-file": "off",
    "@typescript-eslint/interface-name-prefix": ["warn", "always"],
    "@typescript-eslint/explicit-function-return-type": 1
  },
  "settings": {
    "react": {
      "pragma": "React",
      "version": "detect"
    }
  },
  "parser": "@typescript-eslint/parser"
}
```
3. Create `.eslintignore`
```
src/registerServiceWorker.js
src/**/__tests__/**
```
4. Update `scripts` section in your `package.json`
```
"scripts": { 
    "lint:fix": "eslint './src/**/*.{ts,tsx}'"
 }
```
5. Run `npm run lint:fix`

## Prettier - TODO

1. You need to have `TSLint` configured
2. `npm install tslint-config-prettier --save-dev`
3. `npm install tslint-plugin-prettier --save-dev`
4. Update your `tslint.json` file
```
{
  "extends": [
    "tslint:recommended",
    "tslint-react",
    "tslint-config-prettier"
  ],
  "rulesDirectory": [
    "tslint-plugin-prettier"
  ],
  "rules": {
    "prettier": true
  }
}
```
5. Create `.prettierrc`
```
{
  "trailingComma": "none",
  "singleQuote": true,
  "printWidth": 120
}
```
6. Update `scripts` section in your `package.json`
```
  {
    "scripts": {
      "tslint-check": "tslint-config-prettier-check ./tslint.json",
      "prettier": "npm run tslint-check && prettier --write \"*/**/*.{ts,tsx,less}\""
    }
  }
```
7. Run `npm run prettier`
