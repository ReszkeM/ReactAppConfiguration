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

1. Create project folder
```
mkdir ./test-project
cd ./test-project
```
2. Install parcel
```
yarn add --dev parcel
# or
npm install --save-dev parcel
```
3. Create index page
```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8"/>
    <title>My First Parcel App</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```
4. Run app
```
yarn parcel src/index.html
# or
npx parcel src/index.html
```
5. Add shortcut scripts to package.json
```
 "scripts": {
    "start": "parcel",
    "build": "parcel build"
  },
```
6. Install React
```
yarn add react react-dom
# or
npm i react react-dom
```
7. Create a react component and include it in script
- src/index.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>My Parcel App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="index.js"></script>
  </body>
</html>
```
- src/index.js:
```jsx
import { createRoot } from "react-dom/client";
import { App } from "./App";

const container = document.getElementById("app");
const root = createRoot(container)
root.render(<App />);
```
- src/App.jsx:
```jsx
export function App() {
  return <h1>Hello world!</h1>;
}
```

## Typesctipt

[TSC](https://www.typescriptlang.org/docs/handbook/compiler-options.html) is the official TypeScript compiler from Microsoft. While Parcel’s default transpiler for TypeScript is much faster than TSC, you may need to use TSC if you are using some configuration in `tsconfig.json` that Parcel doesn't support. In these cases, you can use the `@parcel/transformer-typescript-tsc` plugin by adding it to your `.parcelrc`.

.parcelrc
```rc
{
  "extends": "@parcel/config-default",
  "transformers": {
    "*.{ts,tsx}": ["@parcel/transformer-typescript-tsc"]
  }
}
```

1. Install typescript and types for default packages.  
```
npm install @types/react @types/react-dom @types/jest --save-dev
# or  
yarn add @types/react @types/react-dom @types/jest --dev
```

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
type Props = {
  redirectTo: string;
}

const RequireAuth: React.FC<Props> = ({ redirectTo }): JSX.Element => {
  const { isAuthenticated } = useIsAuthenticated();
  return isAuthenticated ? <Outlet /> : <Navigate to={redirectTo} />;
}

export const App: React.FC = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/login" element={<Login />} />

        <Route path="/settings" element={<RequireAuth redirectTo="/login" />}>
          <Route index element={<Settings />} />
          <Route path="account" element={<Account />} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}
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
    ]
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
