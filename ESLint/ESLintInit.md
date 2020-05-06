# ESLint 세팅값

React + typescript로 프로젝트를 시작할 때 환경 세팅에 시간을 너무 많이 뺏기는 것 같아 정리해 둠.

---

### install

```
$> npm i -D eslint eslint-config-airbnb-base eslint-config-prettier eslint-import-resolver-typescript eslint-plugin-import eslint-plugin-react

$> npm i -D @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

### eslintrc.json

```json
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "airbnb-base"
  ],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 2018
  },
  "plugins": ["react", "@typescript-eslint", "import"],
  "rules": {
    "quotes": "off",
    "import/no-unresolved": "error",
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "js": "never",
        "jsx": "never",
        "ts": "never",
        "tsx": "never"
      }
    ],
    "comma-dangle": "off",
    "react/self-closing-comp": [
      "error",
      {
        "component": true,
        "html": true
      }
    ],
    "no-confusing-arrow": "off",
    "react/no-unescaped-entities": 0,
    "implicit-arrow-linebreak": "off",
    "import/prefer-default-export": "off",
    "@typescript-eslint/explicit-function-return-type": "off",
    "@typescript-eslint/no-explicit-any": "off",
    "indent": "off",
    "operator-linebreak": 0,
    "camelcase": "off",
    "@typescript-eslint/camelcase": "off"
  },
  "settings": {
    "react": {
      "version": "detect"
    },
    "import/extensions": [".js", ".jsx", ".ts", ".tsx"],
    "import/parsers": {
      "@typescript-eslint/parser": [".ts", ".tsx"]
    },
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  },
  "ignorePatterns": []
}
```

rules는 필수는 아니지만, 내가 작업하며 불편했던 내용들이므로 그대로 쓰는게 편할 듯. 개인프로젝트 한정.
