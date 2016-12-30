# Conclusion

30 天系列結束了，最後這一章來簡單回顧一下這本書的知識範疇，我覺得用 3 個小節來帶過這章是一個很好的方式——分別是「講了什麼」、「沒講什麼」、「缺了什麼」。

「講了什麼」是讓讀者了解讀完這本書後，可以獲得什麼環節的知識，「沒講什麼」則是讓讀者了解還有什麼旁支末節或者較不重要的部分，可以讓讀者自行探索。而最後的「缺了什麼」則是給我們作者，或者給有意幫忙改進 [boilerplate](https://github.com/noootown/deeperience-react-native) 的同好看的，大家來讓這個 boilerplate 更好。

## 這本書講了什麼？

當初寫這本書的目的，是為了記錄一個完整開發流程和架構所必備的東西，所以著重在各部分比較基礎，比較精神的層面。

首先，我們先提到 [Boilerplate (Day 1)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Introduction/React%20Native%20&%20Boilerplate.html) ，帶給讀者們比較大範圍的脈絡。接著，我們講解了寫 React Native 所需要的基本技術和工具 [ES6 (Day 2)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/ES6%20vs%20Babel.html)、[React 基本概念 (Day 3)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Reactjs%20Lifecycle%20&%20State%20vs%20Props.html)、[Flexbox (Day 4)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Flexbox.html)、[Lint (Day 5)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Basic/Lint%20&%20Coding%20Style.html)。

接著，我們帶過了src 內部主要的結構，以及一個 native app 所需要的一些基本功能。包括：[檔案結構 (Day 6)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/File%20Structure.html)、[React Native Style (Day 7)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/React%20Native%20Style.html)、[多國語系 (Day 8)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/I18n.html)、[Routing (Day 9)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/React%20Native%20Routing.html)、[Local Storage (Day 10)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Infrastructure/Local%20Storage.html)。

講完這部分，要開始實戰時，我們講解了整個架構的資料流核心——Redux。提到了這些章節：[Redux 和 React 的關係 (Day 11)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Redux%20&%20React.html)、[Store 和 State 的差異 (Day 12)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Store%20vs%20State.html)、[Container 和 Component 的區分 (Day 13)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Container%20vs%20Component.html)，也提到了 redux 的基本部分在我們的 boilerplate 裡面如何實作的：[Reducer & Action creater & Action (Day 14)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Reducer%20&%20Action%20creater%20&%20Action.html)、[MapStateToProps & MapDispatchToProps & Connect (Day 15)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/MapStateToProps%20&%20MapDispatchToProps%20&%20Connect.html)。提完了以上這些後，我們也帶到了資料的格式 [Immutable JS (Day 16)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/ImmutableJS.html)，以及較為進階的課題——[Redux 的 Middleware (Day 17)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Middleware.html)。

接著，我們把焦點轉向後端的部分，先簡單介紹了 [Firebase (Day 18)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/Firebase.html)，接著設計了我們的 [Data Model (Day 19)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/Data%20Modal.html)，也揭示了我們之後 [API (Day 20)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Backend/API.html) 的改變方向。

講完 backend  的部分後，我們提到 js 較為深入的課題，非同步處理，分三個章節介紹—— [Promise & Generator Function & Async Await (Day 21)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Promise%20&%20Generator%20Function%20&%20Async%20Await.html)、[Redux Thunk (Day 22)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Redux%20Thunk.html)、[Redux Saga (Day 23)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Advanced%20State%20Control/Redux%20Saga.html)。

再來，我們講解了維護程式碼的工具，也就是 test。我們提到了 static type checker [Flow (Day 24)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Flow.html)，在 component test 的部分，我們使用了 [Jest (Day 25)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Jest.html)，在功能 test 的部分，我們則選用了 [Mocha 和 Chai (Day 26)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Test/Mocha%20Chai.html)。

最後，把所有 JS 的部分提完後，我們又提到了 [iOS (Day 27)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/iOS%20Structure.html) 和 [Android (Day 28)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/Android%20Structure.html) 的內部結構，以及 [部署方式 (Day 29)](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Other/Deploy.html)。

## 這本書沒講什麼？

最開始在規畫這本書的規畫時，我特地沒有規畫一個部分，就是好用的 component library 教學。因為我認為這個部分應該由使用者自行去找適合自己專案的，或者試著去做一個。因此，我把把這部分的探索留給讀者們。

## 這本書或這個 boilerplate 還缺了什麼？

這本書在一天一篇的時間限制之下，我真心覺得沒有很仔細。例如 redux 的部分，並沒有實際代讀者去一行一行的完成程式碼，test 的部分，也沒有實際去探究該如何寫出好的 test ，只是匆忙的帶過。

至於 boilerplate，在 API 制定的部分，以及 Immutable 的部分，也還沒有完全統一。 而整體的 coding style 也還有一些小瑕疵，也還沒引入 ES7，讓 code 的可讀性和維護性更高。這是第二版的維改進方向。

## 後記

30天系列結束了，剛好也是一年的最後一天，以這篇文章來記念一下一整年的努力XD。感謝我的好朋友、好伙伴，也是本 boilerplate 的共同作者 [Rae](https://github.com/joey3060) ，常跟我討論 code 和架構的寫法。他對於本 boilerplate 成形有著莫大的幫助，甚至貢獻度比我高。謝謝他的付出，也才有本書的推出。
