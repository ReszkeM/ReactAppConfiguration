# ReactAppConfiguration

Guide to configure react app. 
Stack:
1. [Basic setup](#basic-project-setup)
2. [Typescript](#typesctipt)
3. [State management](#state-management)
4. [Router](#router)
5. [ESLint](#eslint)
6. [Prettier](#prettier)
7. [Styles](#styles)
8. [Translations](#translations)
9. [Tests](#tests)

## Basic project setup

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

## State management

1. Redux
```
npm install redux
npm install @types/react-redux --save-dev
# or  
yarn add redux
yarn add @types/react-redux --dev
```
2. Redux Saga
```
npm install redux-saga
# or  
yarn add redux-saga
```
3. React Query
```
npm install react-query
# or  
yarn add react-query
```

## Router

1. Install Router
```
npm install react-router react-router-dom
npm install @types/react-router-dom --save-dev
# or 
yarn add react-router react-router-dom
yarn add @types/react-router-dom --dev
```
2. Samples  
```
<Switch>
    <Route
      path={'/test-route-1'}
      render={() => (
        <Layout
          content={<YourContainer1 />}
          cannotAccesView={cannotAccesView}
        />
      )}
    />

    <Route
      path={'/test-route-2'}
      render={() => {
        if (cannotAccesView) {
          return <Redirect to="/" />;
        }
        return <Layout content={<YourContainer2 />} />;
      }}
    />
    
    <Route
      path={'/test-route-3'}
      render={() => {
        if (condition1) {
          return <Layout content={<YourContainer1 />} />;
        }

        if (condition2) {
          return <Layout content={<YourContainer2 />} />;
        }

        return <Layout content={<YourContainer3 />} />;
      }}
    />
</Switch>
```

## ESLint

Why ESLint?
https://eslint.org/blog/2019/01/future-typescript-eslint

1. `npm install @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb eslint-plugin-react eslint-plugin-react-redux eslint-plugin-redux-saga eslint-plugin-react-hooks eslint-plugin-import --save-dev`
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
    "@typescript-eslint/explicit-function-return-type": 1,
    "import/order": [
      "error",
      {
        "pathGroups": [
          {
            "pattern": "react",
            "group": "external",
            "position": "before"
          },
          {
            "pattern": "./styles",
            "group": "sibling",
            "position": "after"
          }
        ],
        "groups": ["builtin", "external", "internal", "parent", "sibling", "index"],
        "pathGroupsExcludedImportTypes": ["react"],
        "newlines-between": "always",
        "alphabetize": {
          "order": "asc",
          "caseInsensitive": true
        }
      }
    ],
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
webpack/*
```
4. Update `scripts` section in your `package.json`
```
"scripts": { 
    "lint:fix": "eslint './src/**/*.{ts,tsx}'"
 }
# or you can use your local esslint
npm i -g eslint
```
5. Run linter
```
npm run lint:fix
# or you can use your local esslint
eslint --ext .ts,.tsx --fix --debug source/path-to-directory
eslint --fix --debug source/path-to-file/Component.tsx
```

## Prettier

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

## Styles

## Translations

## Tests
