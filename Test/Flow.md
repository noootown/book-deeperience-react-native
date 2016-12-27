# Flow

## 前言

從這章開始的3章，我們要來討論有關 test 的內容。這章探討的是 facebook 的開源專案 flow。

對於 JS 有一般了解的人，應該會知道 JS 是弱型態的語言，也就是宣告參數的時候不需要指定型別。雖然弱型別有弱型的好處，但是對於使用程式碼撰寫習慣不好，或者註解不清楚的程式碼，都有可能導致大量的臭蟲，而 flow 就是為了解決這個問題。

## 用法介紹

在使用 flow 之前，需要先在文件的開頭寫上下面這段，兩者的差別可以參考這篇 [文章](https://flowtype.org/docs/existing.html#weak-mode)。
```
// @flow
// 或
// @flow weak
```

使用 flow 的方法很簡單，只要在參數後面加上型別即可。而型別的種類，在 [這篇文](https://flowtype.org/docs/quick-reference.html#primitives)。

```
export signup = (username:string, email:string, password:string) => {
  type: SIGNUP_START, // redux-saga actions
  payload: {
    username,
    email,
    password,
  },
}
```

除了檢查參數的型別外，也可以檢查回傳值的型別。

```
function returnNum(a): number {
	return a
}
```
如果回傳或傳入的是一個物件，而且結構很複雜，也可以使用 ```any``` type 來略過，但為了日後維護容易，建議使用 flow 提供的 type來定義。

```
type ObjectWithManyProperties = {
  foo: string,
  bar: number,
}
```

全部都寫完後，我們就可以輸入 ```flow``` 來檢查專案囉。


## 結語

整個專案之中，我們認為 action 的地方掌握資料的傳遞，是比較好驗證 flow 的，因此我們選擇在 action 上加上 flow 測試。雖然 flow 的用法相較於 typescript 而言，是比較不侵入的，但還是有可能會拖慢專案的進度，因此為了專案進度的關係，我們只部份選擇部分使用 flow。

此外，因為 flow 也有和第三方套件相容的問題，這個目前還沒有在我專案解決，這部分會在之後的 boilerplate 版本釋出後，再將 flow 的覆蓋覆提升。

## 延伸閱讀

1. [Flow vs Typescript](https://djcordhose.github.io/flow-vs-typescript/2016_hhjs.html#/1)
2. [Flow 官方網站](https://flowtype.org/)