# birman

[expo](https://expo.io/)を使用しないReactNative(0.61.2)の環境構築メモ

## 前提

- Mac

- vscode

- react-native 0.61.2

## 前準備

一度も環境構築したことない場合、
[公式](https://facebook.github.io/react-native/docs/getting-started.html#installing-dependencies)を見て`Node`、`Watchman`、`ReactNative`、`Xcode`を入れておく

## プロジェク構築

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/1)

### プロジェクトの作成

`react-native init [プロジェクト名]`

```
$ react-native init birman
$ cd birman
```

### Podインストール

```
$ cd ios && pod install && cd ../
```

### iPhoneシュミレータ起動

welcomeページが立ち上がる

```
$ react-native run-ios
```

## パッケージマネージャをnpmにする

[この手順の差分](https://github.com/ryunosukemaeda0922/birman/pull/2)

yarnのままでも問題はない、個人的な好み
`yarn.lock`と`node_modules`を削除し`npm install`
`npm install`は`npm i`に省略可能。

```
$ rm yarn.lock && rm -rf node_modules && npm i
```


### ESLint

JavaScript のための静的検証ツールを追加

参考
[ESLint 最初の一歩](https://qiita.com/mysticatea/items/f523dab04a25f617c87d)

```
$ npm install --save-dev eslint
$ ./node_modules/.bin/eslint --init
```
