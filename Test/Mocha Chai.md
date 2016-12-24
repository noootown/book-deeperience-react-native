# Mocha Chai

## 前言

上一章講完了 Jest 這個單元測試框架 ，這一章要來提另一個比較老牌的單元測試框架 mocha，以及他的斷言庫 Chai 。會使用 Mocha 當我們單元測試的其中一環，其實是當初在設定 Jest 的時候，在處理 saga test 的部分一直設定不過，後來用 mocha 就解決了，因此專案目前便採用 mocha 做為非同步 saga test 的測試框架。

## 架構

基本上所有的測試框架，撰寫起來的方法都差不多。因此我們直接上程式碼，然後慢慢的講解：

這部分的程式碼是這樣的，describe 代表的是一個單元測試的名稱。接著每一個 it 都代表著要完成的每一個小測試。也就是在面面這個測試裡，我們預期它 ```should take the SIGN_UP action```。最後，我們 ```expect``` next 要```deepEqual```，也就是完全相等 ```take(SIGNUP_START)```。關於這部分的語法，其實並不會很難，官方的 API 看一下，應該很快就可以上手了。

```
describe('signup', () => {
  it('watchSignUp should take the SIGN_UP action', () => {
    const gen = watchSignUp()
    const next = gen.next().value
    expect(next).to.deep.equal(take(SIGNUP_START))
  })
})
```
接著要進入這章比較重要的部分，也就是 saga generator function 的測試。這部分開始，要請讀者一一比對上下兩段程式碼，因為我們會來回在兩段程式碼之間穿梭。

首先我們先製作一個假的 payload ，然後把它丟到 signUp 這個 generator function 內，然後指定給 ```gen``` 這個常數。我們接著會用 gen 來做 generator function  的迭代。

當我們每一次 call next() 的時候，都會跑到下一個 yield 去，而 ```next.value``` 就必須等於 yield 右手邊的程式碼。

特別要發一個特殊的用法，如果我們在 ```next()``` 裡面使用一個變數去代換掉，就代表我們要拿這個變數去替換掉 yield 右邊的程式碼。相關程式碼可以看有關 ```UserModel``` 的部分。
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

```
it('should signup successful', () => {
    const username = 'fakeJohn'
    const email = 'fake@gmail.com'
    const password = 'fake2134'
    const uid = '1234'
    const payload = { username, email, password }
    const user = { uid }
    const newUser = new UserModel(uid, { email, username })

    const gen = signUp(payload)
    let next = gen.next().value
    expect(next).to.deep.equal(put(authActions.signupRequest()))

    next = gen.next().value
    expect(next).to.deep.equal(call([api, api.signup], payload))

    next = gen.next(user).value
    expect(next).to.deep.equal(newUser)

    next = gen.next(newUser).value
    expect(next).to.deep.equal(
      call([api, api.writeDataBase], newUser.getPath(), newUser.getData()))

    next = gen.next().value
    expect(next).to.deep.equal(
      put(authActions.signupSuccess({ uid })))

    next = gen.next().value
    expect(next).to.deep.equal(put(authActions.logoutState()))
  })
})

```

最後，當所有部分都完成後，就可以輸入 ```npm test``` 跑測試了。不過因為我們在 ```package.json``` 裡的設定，所以會先跑 ```Jest```，也就是 component test 的部分，接著才會跑 mocha 的 saga test。

## 延伸閱讀

1. [使用Mocha和Chai来测试Node.js应用](http://wwsun.github.io/posts/testing-node.js-with-mocha-and-chai.html)