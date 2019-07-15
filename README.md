# ReactAppConfiguration
Guide to configure react app. 
Stack:
1. [Typescript](#typesctipt)
2. [TSLint](#TSLint)
3. [Prettier](#Prettier)
4. [Styles + Bootstrap](#Styles)
5. [Translations](#Translations)
6. [Fetching data](#Fetching-data)
7. [Redux](#Redux)
8. [Router](#Router)
9. [Tests](#Tests)

## Basic build setup

1. `npx create-react-app my-app`
2. `cd ./my-app`
3. `npm install`
4. `npm start`

For more info visit https://facebook.github.io/create-react-app/docs/getting-started

## Typesctipt

1. `npm install typescript --save-dev`
2. `npm install @types/node @types/react @types/react-dom --save-dev`
3. rename your `.js` files to `.jsx` in case components or `.ts` in case pure ts files

## TSLint

1. `npm install tslint --save-dev`
2. `npm install tslint-react --save-dev`
3. Create `tslint.json`
```
{
  "extends": [
    "tslint:recommended",
    "tslint-react",
  ],
  "rules": {
    // add your favourites rules
  }
}
```
4. Update `scripts` section in your `package.json`
```
"scripts": { 
     "lint": "tslint -c tslint.json src/**/*.{ts,tsx} --fix --format verbose"
 }
```
5. Run `npm run lint`

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
