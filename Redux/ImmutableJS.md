# ImmutableJS

## 前言

這章要講的是 immutableJS，是一種特殊的資料儲存方式，而且是由 Facebook 開源的專案。他因為有一些良好的特性，所以被使用在我們的專案之中。

# Immutable object vs plain object 

Immutable object 和 plain object 相比，有以下幾個較為優勢的特點：

1. 變數一但成為 immutable object，他就不能再被改變，call 任何 immutable js 的 API 來改變它都會再回傳一個新的 immutable object。 這代表著每一個immutable 的 function 都是一個 pure function。我們可以在程式碼的各個地方輕鬆 console.log()，而不用去管是不是有被其它段程式碼不小心改到。

2. 數據是被鎖住的，避免在任意情況下，不經意的被修改，也就能保證我們的數據是我們想要的，而不會發生臭蟲。

3. 擁抱functional programming。

然而相比之下，immutableJS 的特點便是需要另一個學習成本來了解 immutable 的 API。

其它關於 immutable 的優勢和介紹，可以看延伸閱讀2。

## 架構

在我們的架構之下，所有的 initialState 都是使用 immutable object。我們使用 immutable 提供的 record 來設定 initial state。檔案的位置放在 ```src/reducers/XXX/XXXInitialState.js```。一層一層的關係都是事先定義好的。

```
const Form = Record({
  state: REGISTER,
  disabled: false,
  isFetching: false,
  fields: new (Record({
    username: '',
    usernameHasError: false,
    usernameErrorMsg: '',
  }))(),
})
```

接著我們會在 reducer 內引入這個檔案。如果我們不是使用 immutablejs，那麼 reducer 會長這個樣子。

```
switch (action.type) {
  case SET_HOTEL_TYPE:
	return {
		...state,
		hotelType: action.payload.type
	}
}
```
寫成這個樣子有一個，便是可讀性較低，容易有臭蟲產生。

## 延伸閱讀

1. [Immutable.js 簡介](https://rhadow.github.io/2015/05/10/flux-immutable/)
2. [簡述 Immutable js 和 React中的實踐](http://inder.com.tw/immutable-js-and-react/)
3. [Record](https://facebook.github.io/immutable-js/docs/#/Record)