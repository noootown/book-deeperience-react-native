# React Native & Boilerplate

## 《從0到100打造一個React Native boilerplate》系列前言
前不久，為了開發一個產品，我和我的同事**Rae**，開發了一個 boilerplate，目標是讓新進的人能更好上手，也讓我們開發的速度更快，藉由這次30天的活動，我們想要將我們開發的成果和大家分享，也希望大家有興趣的人可以給我們一些建議和 PR。

在進行內文的撰寫之前，我想先謝謝我的同事**Rae** 。在這個過程之中，他教了我很多（包括我的 redux 就是他教的XD）此外，這一個 boilerplate 也是在他的通力合作之下完成的。所以在撰寫這一系列文之前，我想要先強調，這個 boilerplate **並非我一個人完成的**。

這次的30天鐵人文章，會同步發表於 [gitbook](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/)，喜歡文章的，歡迎給我們建議和star。

此外，這個專案的名稱叫做 [deeperience-react-native](https://github.com/noootown/deeperience-react-native)，也歡迎各位大大給我們 PR 或Star。

## 這個系列的介紹方法，及希望帶給讀者的知識和概念

- 了解 React Native 的精神和開發原則。
- 了解本 boilerplate 的精神，但不透過此書追求程式能力的訓練。
- 試著打造自己的 boilerplate。

## 你是我們的 Target Audience 嗎？

#### 1. 適合閱讀此系列的人
- 熟悉 ReactJs，想要了解 React Native 的人。
- 了解基本的 JS 特性的人，例如 closure, functional programming, this。
- 會用基本的 ES6 ES7 的人。
- 了解簡單的 reactjs 和 redux。
- 想要了解如何建造一個 boilerplate 的人。 

#### 2. 不適合閱讀此系列的人
- 了解JQuery，但是沒有碰過 ReactJs 的人。
- 對於 JS 沒有強烈興趣的人，因為接下來的所有程式碼全部都是 JS。

## React Native

#### 1. 關於 React Native

跨平台的開發一直都是工程師的夢想，也一直都是工程師關注的焦點。自從 Android 和 iOS 問世之後，大家就一直在找尋方法解決這個問題。之後陸續有PhoneGap、React Native、Xamarin、Cordova 的問世，主要的目標都是在解決這個問題。

React Native 由 Facebook 開源釋出，旨在解決跨平台的問題。React Native 官網上有一句話，可以很傳神的表達這個目標。


> Learn once, Write anywhere


這句話不同於 PhoneGap 的 Write once, Run anywhere，隱含著更不一樣的思想。首先，Facebook 相信各個平台有各自的風格，例如手機有自己的體驗，網頁也有自己一套設計原則，如果像PhoneGap，把所有的平台都用同一種方法（WebView）撰寫，那麼體驗會不好。因此 Facebook 希望，學習 React 這個開發的理念和方法，套用在各個平台，適應各個平台，藉此達到完美體驗，並提升開發效率。


#### 2. React Native 的特點


- 預設使用 ES6+ 和 React (Learn once, write anywhere)。
- 不同於 PhoneGap 使用 WebView，React Native 使用 Native Components，更貼近原生APP 使用者體驗。
- 全部都是由 JS 打造，容易整合 Web 的標準，XHR 和 geolocation 等。
- 可用 Chrome 開發者工具除錯，支援 Hot Reloading。
- 使用 CSS3 Flexbox。
- Facebook 積極維護，並已應用於現行產品中。市面上也有一些 APP 是由 React Native 開發的。
- Web developer (特別是前端工程師) 可無痛進入開發。
- 支援 iOS 和 Android 。
- 尚未發佈穩定版。

## Boilerplate

#### 1. 什麼是 boilerplate ？

由於 JS 的蓬勃發展，前後端都出現大量的 framework 和 library 可以使用，例如前端就有 reactjs, angularjs, vuejs。也因此，工程師可以自由選擇要組合哪些 framework 和 library，以便達到最好的開發效果，以及得到最適應目前情況的系統。

Boilerplate 的意思是模版，意即整個網站或系統的架構。專案裡寫的 code 全部都是由這個模版所定義的風格和格式所長出的。API 有統一的 call 法，架構怎麼擺、檔案怎麼放之類的，全部都已經事先規定好了。這種感覺有一點像學測作文一樣，第一段該寫什麼，接下來該怎麼寫，只要照著這個寫法，就準沒錯。當然，boilerplate 不是這麼八股的東西，但這就是模版的用途。

#### 2. 好的 boilerplate 的特點

一個好的模版，具有以下的特點，對於團隊的整個開發，也會是一個很大的幫助。

- 好的檔案結構，該工程師要找程式碼可以很快。
- 詳細清楚的模組化，方便工程師改程式碼，而不會讓整個系統爆掉，也就是有良好的相依性。
- 程式碼重複利用，這是一個 single source of truth 的概念，只要維護一段程式碼就好了。
- 統一且良好的程式碼風格，讓之後進來的工程師可以維護。
- 分成 test, development 和 production 版本，讓不同 team 的工程師可以對系統做不同的操作。
- 彈性，API 定義清楚，容易 migrate，模組容易插拔。例如可以很快速的換成不同的資料庫來服務系統。

## 安裝方法

請參考 [README.md](https://github.com/noootown/deeperience-react-native/blob/develop/README.md)

## 目錄

以下是這次30天的目錄 

1. [Introduction -- React Native & Boilerplate](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Introduction/React%20Native%20&%20Boilerplate.html)
2. [Basic -- ES6 vs Babel](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/ES6%20vs%20Babel.html)
3. [Basic -- Reactjs Lifecycle & State vs Props](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Reactjs%20Lifecycle%20&%20State%20vs%20Props.html)
4. [Basic -- Flexbox](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Reactjs%20Lifecycle%20&%20State%20vs%20Props.html)
5. [Basic -- Lint & Codings Style](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Lint%20&%20Coding%20Style.html)
6. [Infrastructure -- File Structure](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/File%20Structure.html)
7. [Infrastructure -- React Native Style](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/React%20Native%20Style.html)
8. [Infrastructure -- I18n](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/I18n.html)
9. [Infrastructure -- React Native Routing](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/React%20Native%20Routing.html)
10. [Infrastructure -- Local Storage](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/Local%20Storage.html)
11. [Redux -- Redux & React](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Redux%20&%20React.html)
12. [Redux -- Store vs State](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Store%20vs%20State.html)
13. [Redux -- Container vs Component](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Container%20vs%20Component.html)
14. [Redux -- Redux & Reducer & Action creater & Action](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Reducer%20&%20Action%20creater%20&%20Action.html)
15. [Redux -- MapStateToProps & MapDispatchToProps & Connect](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/MapStateToProps%20&%20MapDispatchToProps%20&%20Connect.html)
16. [Redux -- Immutable JS](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/ImmutableJS.html)
17. [Redux -- Middleware](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Middleware.html)
18. [Backend -- Firebase](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/Firebase.html)
19. [Backend -- Data model](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/Data%20Modal.html)
20. [Backend –- API](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/API.html)
21. [Advanced State control -- Promise & Generator Function & Async Await](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Promise%20&%20Generator%20Function%20&%20Async%20Await.html)
22. [Advanced State control -- Redux Thunk](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Redux%20Thunk.html)
23. [Advanced State control -- Redux Saga](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Redux%20Saga.html)
24. [Test -- Flow](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Flow.html)
25. [Test -- Jest](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Jest.html)
26. [Test -- Mocha Chai](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Mocha%20Chai.html)
27. [Other -- iOS Structure](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/iOS%20Structure.html)
28. [Other -- Android Structure](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/Android%20Structure.html)
29. [Other -- Deploy](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/Deploy.html)
30. [Conclusion](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Conclusion/)

## 參考資料
1. [React Native 官網](https://facebook.github.io/react-native/)
2. [一看就懂的 React Native + Firebase Mobile App 入門教學](http://blog.techbridge.cc/2016/09/10/react-native-redux-android-firebase/)
