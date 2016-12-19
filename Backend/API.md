# API

## 前言

接著我們要探討和後端相接的 API 。一般來說 API 都可以分成 CRUD (Create, read, update and delete) 這四種。也因此，就會分別對應到 POST, GET , PUT, DELETE 這四種 API。好的API設計方便管理，也方便做更改，接下來我會介紹一下我們 boilerplate 的 API 設計。也會勾勒出之後改版的新設計模式。

## 架構

#### 使用不同的後端

首先，在我們的 boilerplate 裡面，目前是只支援 firebase 。但是我們也保留彈性的空間，讓讀者可以自由接其它種系統，例如 api server。因此我們先定義一下，API 另一端的接口是什麼，這部分的程式碼寫在 ```/src/api/apiFactory.js``` 和 ```/src/config.js```。 apiFactory.js 裡面，會回傳一個 firebase 的 factory instance，由這個 instance ，我們可以做所有的  firebase 資料庫操作。

#### Interface 和實作

為了方便表示所有的 API 的參數和實作的內容 ，我們另外開了一個 API Interface ，把所有 API 的相關需求都列了上去，程式碼在```src/api/apiInterface.js```裡。接著我們在 ```src/api/firebase.js```裡面才去繼承它，然後實作實際的功能。

#### 細節

其中可以看到的是，我們實作了一個很通用的API，只要傳入 path 和 data ，就可以讀寫資料庫了。

```
  writeDataBase(path, value) {
    return firebase.database().ref(path).set(value)
  }

  updateDataBase(path, value) {
    return firebase.database().ref(path).update(value)
  }

  readDataBaseOnce(path) {
    return firebase.database().ref(path).once('value').then(res => res.val())
  }

ex: 
const user = new UserModel(uid, { email, username })
writeDataBase(user.getPath(), user.getData())
```

## 之後版本改進方向

目前的 API 實作還是十分簡陋的，主要有下列缺點：

1. 功能分配不夠明確，目前是全部都塞在 firebase.js 裡面，之後會把 API 依照操作資料屬性獨立出來。
2. 目前的 API 在讀寫資料方面，都是直接操作最底層的  writeDataBase, updateDataBase, readDataBase，之後應該再外面再包一層 function，如此一來，對於整個系統才更加的彈性。

## 延伸閱讀

1. [Firebase API](https://firebase.google.com/docs/reference/js/)