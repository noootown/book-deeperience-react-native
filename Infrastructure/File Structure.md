# File Structure

## 前言

這章要來講檔案結構的部分，檔案結構是整個boilerplate的精華，因為有好的檔案結構，才能最快速的在對的地方找到想要的資料。在了解檔案結構之後，我們才會一一介紹，並深入各個部分。

## 檔案結構

以下這部分，我會列舉檔案之中，可能之後會寫到的部分

```
/android		<- android 的目錄
/ios			<- ios 的目錄
/src			<- 所有 js 檔都在這
.eslintrc.json	<- eslint rule
.editorconfig	<- 編輯器的通用設定
.eslintignore	<- 哪些檔案不要跑 lint
.gitignore		<- 哪些檔案不要 push 到 github
gulpfile.js		<- gulpfile，不過目前沒有用到
index.android.js<- android 的 entry point
index.ios.js	<- ios 的 entry point
package.json	<- 整個專案的資訊
testHelper		<- test的設定檔

```

接著我們拆開 /src

```
/__mocks__	<-- Jest 的 mock 檔
/api		<-- api定義處 
/components	<-- presentation components 放置處
/constants	<-- constants 放置處
/containers	<-- container 放置處
/images		<-- 放圖片
/lib		<-- 放一些共用的 function
/model		<-- 放 data model
/reducers	<-- 放 action creator, action, reducer
/styles		<-- 放整個專案的 style 定義
config.js	<-- 放設定檔
index.js	<-- 整個專案的 entry point
```
這是大致的檔案結構，除了 ```constants``` 之外，其它部分我們都會一一講到。

## 結語
這就是這個專案的大致結構，事實上，大部分旳boilerplate 也都是這樣分的，那麼細部的差異，我會在之後的章節，一個一個帶到。