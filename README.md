# birman

[expo](https://expo.io/)を使用しないReactNative(0.61.2)の環境構築メモ

## 前提

- Mac

- Visual Studio Code (VSCode)

- ReactNative 0.61.2

- JavaScript

## 前準備

一度も環境構築したことない場合、
[公式](https://facebook.github.io/react-native/docs/getting-started.html#installing-dependencies)を見て`Node`、`Watchman`、`ReactNative`、`Xcode`を入れておく

## プロジェク構築

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/1)

### プロジェクトの作成

#### `react-native init [プロジェクト名]`

```
$ react-native init birman
$ cd birman
```
#### Podインストール

```
$ cd ios && pod install && cd ../
```

#### iPhoneシュミレータ起動

```
$ react-native run-ios
```

welcomeページが立ち上がる

### パッケージマネージャをnpmにする

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/2)

yarnのままでも問題はない、個人的な好み

#### `yarn.lock`と`node_modules`を削除し`npm install`

`npm install`は`npm i`に省略可能。

```
$ rm yarn.lock && rm -rf node_modules && npm i
```

### ESLint

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/3)

JavaScript のための静的検証ツールを追加(参考[ESLint 最初の一歩](https://qiita.com/mysticatea/items/f523dab04a25f617c87d))

```
$ npm install --save-dev eslint@5.16.0
$ ./node_modules/.bin/eslint --init
```

色々質問されるのでが、下記の設定で

```
? How would you like to use ESLint? 
❯ To check syntax, find problems, and enforce code style

? What type of modules does your project use? (Use arrow keys)
❯ JavaScript modules (import/export) 

? Which framework does your project use? (Use arrow keys)
❯ React 

? Where does your code run? (Press <space> to select, <a> to toggle all, <i> to 
invert selection)
❯ Node

? How would you like to define a style for your project? (Use arrow keys)
❯ Use a popular style guide 

? Which style guide do you want to follow? (Use arrow keys)
❯ Airbnb (https://github.com/airbnb/javascript) 

? What format do you want your config file to be in? (Use arrow keys)
❯ JSON 

? Do you want to downgrade? (y/N)
❯ y

? Would you like to install them now with npm? (Y/n) 
❯ y
```

#### VSCodeの設定

VSCodeに[ESlint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)の拡張機能を追加

VSCode上でエラーメッセージを表示してくれます

### Prettier

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/4)

コードフォーマッタ(参考[ESLint 最初の一歩](https://qiita.com/mysticatea/items/f523dab04a25f617c87d))

```
$ npm i --save-dev  prettier-eslint prettier-eslint-cli eslint-plugin-jest
```

#### VSCodeの設定

[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)の拡張機能を追加

VSCodeの設定で`Format On Save`をにチェックをすると、ファイル保存時に自動で整形してくれる

### Flow

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/5)

JavaScriptの形チェックを行える(参考[@babel/preset-flow](https://babeljs.io/docs/en/babel-preset-flow))

```
[AwesomeProject/.flowconfig] Connection to flow server got closed. See the output for more information.
```
vscodeでこのエラーが出てたらこの項目で解決する

#### .flowconfigの修正

`react-native 0.61.2`なら`0.105.0`が指定されていると思う

```terminal
$ npm install --save-dev flow-bin@0.105.2 babel-preset-flow
```

node_modulesをflow対象外にする
`.flowconfig`の[ignore]の下に追記

```javascript
./node_modules/.
```
[version]を`^0.105.2`に変更(flow-binとversionを合わせる)

#### scriptsに追記

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/5)

package.jsonのscriptsに`lint`、`prettier`、`flow`、`flow-stop"`、追記

```json
"scripts": {
"start": "react-native start",
"test": "jest",
"lint": "eslint ./src",
"prettier": "eslint ./src --fix",
"flow": "flow",
"flow-stop": "flow stop"
},
```

