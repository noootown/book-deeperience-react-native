# Redux Saga

## 前言

上一章談完了```redux-thunk```，這章要來談 ```redux-saga```。redux-saga 和 redux-thunk 一樣，都是為了解決 redux 非同步的問題。廢話不多說，直接進程式碼囉。

## 架構

在我們的架構裡，saga 檔案都是放在 ```src/reducers/XXX/XXXSaga.js```。但是在實際進到這個檔案看之前，我們先來看一下其它部分。

首先，我們在```src/lib/rootSagas```裡面，引入所有的 saga 檔。接著在 ```src/lib/configureStore.js``` 裡面，我們把 saga middleware 放入到我們的 middleware，專門處理和 saga 有關的 action。最後把 saga 啟動，於是我們的 store 就會監聽 action ，然後相關的動作就會在 saga 檔案定義的程式碼裡面做了。

## Saga 程式碼

saga 的程式碼因為牽涉到 ```genertor function```，所以會比較複雜。接下來我們會慢慢解釋：

首先我們先解釋 authSaga 裡面的這個部分：
```
export default [
  fork(watchSignUp),
  fork(watchInitAuth),
  fork(watchLogout),
  fork(watchLogin),
  fork(watchResetPassword),
  fork(watchFacebookLogin),
]
```
如果有學過作業系統的，應該會知道 ```fork``` 這個函數。這邊的 fork 和作業系統的 fork 有異曲同工之妙，每當我們接收到一個 action（類似 signal 的概念），就會 fork 出一個類似 process 的東西，去執行一個 generator function，如此一來，才不會造成阻塞。

```
export function* watchSignUp() {
  while (true) {
    const { payload } = yield take(SIGNUP_START)
    yield fork(signUp, payload)
  }
}
```

接著這個 watch 函數會不斷的去監聽 action，當我們監聽到 SIGNUP_START 的時候，就會先拿出payload，然後將 payload 傳到 signUp 這個新 fork 的 process。監聽 action 的話，要使用 ```take```。

因為我們是使用generator function，所以可以很完美的停在各個斷點。首先我們會先發一個signupRequest，使用的是 ```put``` 函數。接著，我們會使用 call 來 call 一個 signup api。，並把 payload 傳入。回傳回來的本來應該要是一個 promise，但因為 generator function 的寫法，現在接回來的是一個 user 的 instance。

接著我們拿這個 user 的 instance ，去製作一筆資料庫要存的資料（前面那個只是去跑 firebase 的 auth 流程），這資料可能包含了使用者在註冊時填的資訊之類的。然後再寫一次 database 。細節的部分，就讓各位自己看吧！

```
export function* signUp(payload) {
  try {
    yield put(authActions.signupRequest())
    // user is a promise backed from firebase
    const user = yield call([api, api.signup], payload)
    // newUser will be written in database
    const newUser = yield new UserModel(user.uid, {
      email: payload.email,
      username: payload.username,
    })
    yield call([api, api.writeDataBase], newUser.getPath(), newUser.getData())
    yield put(authActions.signupSuccess({ uid: user.uid }))
    yield put(authActions.logoutState())
    Actions.Main()
  } catch (error) {
    SimpleAlert.alert(I18n.t('AuthMessage.error'), I18n.t('AuthMessage.signupError'))
    yield put(authActions.signupFailure(error))
  }
}
```
## 結語

Saga 引入了 generator function，將巢狀不好維護的 promise 結構扁平化。除了程式碼優美外，也比較容易維護和測試。使用 thunk 和使用 saga 並沒有優劣，看個人需求而定。saga 寫起來麻煩，但日後好維護，我的團隊就是因為這個原因，選擇全面使用 saga。但我們也保留了thunk 的 middleware 在專案裡，各位可认選擇使用。

## 延伸閱讀

1. [redux-saga文檔](http://leonshi.com/redux-saga-in-chinese/)