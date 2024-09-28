# Vue Template 2024
## Vite + Vue + Typescript + ESLint + Prettier
### Steps

Create a project with Vite:

`npm create vite@latest`

Update Vue, Vite and Typescript

`npm i vue@latest`

`npm i -D vite@latest typescript@latest vue-tsc@latest @vitejs/plugin-vue@latest`

Install linter

`npm install -D eslint eslint-plugin-vue`

Install prettier

`npm i -D prettier@latest eslint-plugin-prettier eslint-config-prettier`

Install Typescript linter configuration

`npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin`

Create a `eslint.config.js` at root folder (ESLint flat configuration)

Added linter rules to the `eslint.config.js` file:


```
import pluginVue from "eslint-plugin-vue";
import eslintPluginPrettierRecommended from "eslint-plugin-prettier/recommended";
import eslintConfigPrettier from "eslint-config-prettier";
import * as parserVue from "vue-eslint-parser";
import * as parserTypeScript from "@typescript-eslint/parser";
import pluginTypeScript from "@typescript-eslint/eslint-plugin";

export default [
  ...pluginVue.configs["flat/recommended"],
  eslintPluginPrettierRecommended,
  eslintConfigPrettier,
  {
    files: ["**/*.vue"],
    languageOptions: {
      parser: parserVue,
      parserOptions: {
        parser: parserTypeScript,
        extraFileExtensions: [".vue"],
        sourceType: "module",
      },
    },
    plugins: {
      "@typescript-eslint": pluginTypeScript,
    },
    rules: {
      ...pluginTypeScript.configs["recommended"].rules,
    },
  },
  {
    files: ["**/*.ts", "**/*.tsx"],
    languageOptions: {
      parser: parserTypeScript,
      parserOptions: {
        sourceType: "module",
      },
    },
    plugins: {
      "@typescript-eslint": pluginTypeScript,
    },
    rules: {
      ...pluginTypeScript.configs["recommended"].rules,
    },
  },
  {
    rules: {},
  },
];
```


Add `"prettier": "prettier . --write"` to `package.json` scripts to be able to run prettier.

Then at the console: `npm run prettier`



`TADA!`
