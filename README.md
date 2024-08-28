IN REMOTE REPO A project guide to set up eslint and prettier correctly.

# Setup `package.json`

-   `npm init -y`

# Set up prettier and es-lint-airbnb

-   Run `npm install --save-dev eslint-plugin-prettier eslint-config-prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser`
-   Run `npm install --save-dev --save-exact prettier`
-   Run `npx install-peerdeps --dev eslint-config-airbnb`

-   Create `.eslintrc.json` file and add the following:-

```js
{
    "root": true,
    "parser": "@typescript-eslint/parser",
    "extends": [
        "airbnb",
        "airbnb/hooks",
        "plugin:prettier/recommended",
        "plugin:@typescript-eslint/recommended"
    ],
    "plugins": ["@typescript-eslint", "prettier"],
    "rules": {
        "prettier/prettier": "error",
        "no-unused-vars": "warn",
        "no-console": "off",
        "func-names": "off",
        "no-process-exit": "off",
        "object-shorthand": "off",
        "class-methods-use-this": "off",
        "import/extensions": [
            "error",
            "ignorePackages",
            {
                "js": "never",
                "mjs": "never",
                "ts": "never",
                "tsx": "never",
                "jsx": "never"
            }
        ]
    },
    "settings": {
        "import/resolver": {
            "node": {
                "extensions": [".js", ".jsx", ".ts", ".tsx", ".json"]
            }
        },
        "import/extensions": [".js", ".jsx", ".ts", ".tsx", ".mjs"]
    }
}

```

-   Create a `.prettierrc.json` file with the following:-

```json
{
    "semi": true,
    "singleQuote": true,
    "printWidth": 80,
    "tabWidth": 4,
    "trailingComma": "es5",
    "arrowParens": "always" // always include parenteshes around arrow function parameteres
}
```

-   Create a `.prettierignore` and `.eslintignore` file, and add the following to both.

```
node_modules
build
dist
.cache
public
```

-   Create a `.vscode` folder and inside it create `settings.json` file with the following content.

```json
{
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": "explicit"
    },
    "eslint.alwaysShowStatus": true,
    "files.eol": "\n",
    "prettier.requireConfig": true
}
```

-   Add the following to `package.json` file:-

```json
    "scripts": {
        "lint": "eslint .",
        "lint:fix": "eslint . --fix",
        "format": "prettier --write .",
        "check": "npm run lint && npm run format"
    },
```

-   Create `tsconfig.json` file and add the following:-

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "strict": true,
        "esModuleInterop": true
    }
}
```

-   Finally Install `ESLint` and `Prettier - Code formatter` vscode extensions if you haven't already.

# Common Errors

-   Ts-extension isn't found. In which case, the error maybe that we set `type: module` in `package.json`.
