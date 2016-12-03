# Local Storage

## 前言

總是會有一些資料必須儲存在 local 端的，我們的 API 也整合了這個部分。在 Deeperience-react-native 裡，我們也整合了這個實用的功能。

## 架構

#### AsyncStorage

React Native 預設提供了 AsyncStorage 來做為手機端儲存的機制。這部分像routing 一樣，我們不直接操作原生的 API ，選擇使用 [redux-storage-engine-reactnativeasyncstorage](https://github.com/michaelcontento/redux-storage-engine-reactnativeasyncstorage) 來產生一個  storageEngine。

這個 storageEngine 可以幹麻呢？讓我們直接研究他的source code。

```
import { AsyncStorage } from 'react-native';

export default (key) => ({
    load() {
        return AsyncStorage.getItem(key)
            .then((jsonState) => JSON.parse(jsonState) || {});
    },

    save(state) {
        const jsonState = JSON.stringify(state);
        return AsyncStorage.setItem(key, jsonState);
    }
});
```

原來就是把 AsyncStorage 包起來嘛。當然囉，如果你想要把這段程式碼直接整合到 ```/src/lib/localStorage.js```，也是可以的。

####  /src/lib/localStorage.js

廢話不多說，先看source code。

```
export default (key) => ({
  load() {
    return createStorageEngine(key)
            .load()
            .then(res => {
              if (console.groupCollapsed && console.groupEnd) {
                const now = new Date()

                console.groupCollapsed(`%c load @ ${now.getHours()}:${now.getMinutes()}` +
                  `:${now.getSeconds()}:${now.getMilliseconds()} key = ${key}`,
                  'fontWeight: bold, color:"black"'
                )
                console.log(res)
                console.groupEnd()
              }
              return res
            })
  },
  save(state) {
    if (console.groupCollapsed && console.groupEnd) {
      const now = new Date()
      console.groupCollapsed(`%c save @ ${now.getHours()}:${now.getMinutes()}` +
        `:${now.getSeconds()}:${now.getMilliseconds()} key = ${key}`,
        'fontWeight: bold, color: black'
      )
      console.log(state)
      console.groupEnd()
    }

    return createStorageEngine(key).save(state)
  },
  delete() {
    return createStorageEngine(key).save(null)
  },
})
```

簡單來說，我把原本的又再包了一層，這部分加上我們自製的 logger，方便我們debug的時候使用。

#### 實際使用 —— /src/reducers/auth/authToken.js

這個檔案是拿來儲存 session token 的，雖然在我們預設的 firebase 架構不會用到，但如果使用 mongodb 的話，就會操作到。

```
export class AppAuthToken {
  constructor() {
    this.SESSION_TOKEN_KEY = Config.sessionTokenKey
    this.token = null
    this.fbToken = null
  }

  storeSessionToken(sessionToken) {
    if (sessionToken.token) this.token = sessionToken.token
    else if (sessionToken.fbToken) this.fbToken = sessionToken.fbToken
    return localStorage(this.SESSION_TOKEN_KEY).save(sessionToken)
  }
  /**
   * ### getSessionToken
   * @param {Object} sessionToken the currentUser object
   *
   * When Hot Loading, the sessionToken  will be passed in, and if so,
   * it needs to be stored on the device.  Remember, the store is a
   * promise so, have to be careful.
   */
  getSessionToken(sessionToken) {
    if (sessionToken) {
      localStorage(this.SESSION_TOKEN_KEY)
        .save(sessionToken)
        .then(() => localStorage(this.SESSION_TOKEN_KEY).load())
    }
    return localStorage(this.SESSION_TOKEN_KEY).load(sessionToken)
  }
  /**
   * ### deleteSessionToken
   * Deleted during log out
   */
  deleteSessionToken() {
    return localStorage(this.SESSION_TOKEN_KEY).delete()
  }
}
// The singleton variable
export const appAuthToken = new AppAuthToken()
```
這份 code要關注的重點是，我使用了一個 singleton，來專門處理有關 session 的操作。這樣做有什麼好處呢？主要是節省時間。如果有操作過資料庫的，應該都會知道，操作資料庫是十分花時間的，如果我們之後需要常常用到這份資料，拿我就拿一次就好了，之後就使用已經拿出來的這一份資料。

## 延伸閱讀
1. [singleton](http://openhome.cc/Gossip/DesignPattern/SingletonPattern.htm)