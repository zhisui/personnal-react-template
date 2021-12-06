本模板只供个人日常写demo时使用，更完美的配置请参考相关文档
# Eslint + Prettier + stylelint + Husky + Lint-staged

### 创建样板文件

```
yarn create react-app myapp --typescript
```

在使用yarn的时候如果发现报错，可以尝试使用npm

### 添加依赖

```
yarn add prettier lint-staged husky stylelint stylelint-prettier stylelint-config-prettier stylelint-config-recommended eslint-config-prettier eslint-plugin-prettier -D
```

注意stylelit默认版本是14.1.0，react不支持，可能会报错，建议安装低版本。

### 添加配置文件

```
touch .eslintrc .eslintignore .gitattributes .prettierrc .stylelintrc
```

#### .eslintrc.js

后缀加上js,否则无法识别module.exports语句

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 13,
  },
  plugins: ['react', '@typescript-eslint', 'prettier'],
  rules: {
    'prettier/prettier': 'error',
  },
  extends: ['prettier'],
}

```

####  .eslintignore

设置不需要eslint语法检查的部分

```
# build
build/
```

####  .gitattributes

```
* text=auto eol=lf
```

####  .prettierrc

```
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": false,
  "singleQuote": true,
  "endOfLine": "lf"
}
```

####  .stylelintrc

```
{
  "extends": ["stylelint-prettier/recommended", "stylelint-config-standard"],
  "plugins": ["stylelint-prettier"],
  "rules": {
    "prettier/prettier": true,
    "unit-case": null,
    "no-descending-specificity": null,
    "block-no-empty": null,
    "no-empty-source": [true, { "severity": "warning" }],
    "declaration-colon-newline-after": null,
    "function-name-case": null,
    "indentation": null,
    "no-invalid-double-slash-comments": null
  }
}
```

#### 在package.json条件以下字段

```
{
  "scripts": {
    "lint": "eslint \"src/**/*.{js,jsx,ts,tsx}\"",
    "lint:fix": "yarn lint --fix",
    "stylelint": "stylelint \"src/**/*.{css,scss}\"",
    "stylelint:fix": "yarn stylelint --fix"
  },
  "lint-staged": {
    "src/**/*.{js,jsx,ts,tsx,json,css,scss,md}": ["prettier --write", "git add"]
  },
   "eslintConfig": {
    "parser": "babel-eslint"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  }
}
```


