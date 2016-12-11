# Store vs State

## 前言

上一章，我們大概講完了 redux 的簡單精神和架構。接下來，我們要實際進入 boilerplate，探討 redux 在我們的 boilerplate 裡如何使用。

## Store 和 State 的差別

```Store``` 和 ```State``` 其實功能是一樣的，都是用來控制 component 的 UI 狀態。兩者的主要差別，主要體現在 ```single source of truth```，前者是統一資料源的，由一個 store 控制全部的 UI 狀態，而後者是各自 component 保存各自的 state。

如果只是一個很簡單很簡單的 application，其實使用 local state 是可以的。在這裡我特別強調 local，是因為 state 是由各自的 component 保存。redux 的主要作者 ```Dan Abramov``` 曾在其 [twitter](https://twitter.com/dan_abramov) 提到一句話非常的中肯。[連結](https://twitter.com/dan_abramov/status/642835301929512960)

> Redux: all your state are belong to us.

## createStore

接著我們要介紹 [createStore](http://redux.js.org/docs/api/createStore.html)。在我們的 boilerplate 裡面，我們把這段 code 放在 ```src/index.js``` 和 ```lib/configureStore```，也就是整個 project 的 entry point。

在 createStore 裡面，我們會將 ```initialState```, ```reducer```, ```middleware```，放到 store 的設定裡。initialState 的部分，放在 ```src/reducers``` 的各個資料夾裡，是分門別類的。如果有仔細觀察的話，可以發現裡頭有 ```immutable``` 這個套件，這在之後的章節會談到。

## 是否要使用 setState?

在我們的 boilerplate 裡面，我給的答案是盡量不要，主要有兩個原因。

1. 因為是各個 component 自行 setState，所以會不好管理。
2. (主因) 使用 setState ，我們無法看到 state 的變化。在我們的 boilerplate 裡面，我們裝了一個很好用的套件，叫做 [redux-logger](https://github.com/evgenyrodionov/redux-logger) 。它是以 ```middleware```的形式，灌在 createstore 裡，至於什麼是 middleware，也會在之後的章節提到。有了這個套件，我們就可以輕鬆的 log 出每次 state 改變的情形。這在 local 的 setState 是做不到的﹐除非一個一個 console.log	出來。 

想要使用 redux-logger 的話，可以開啟 chrome 的 debugger。在手機的每個操作都會產生一個action，那麼我們就可以觀察 state 的變化。

![redux-logger]('../images/redux-logger.png)

雖然在單人開發上，偶爾寫個 local state 會很輕鬆，但是在多人開發起來，這會是個臭蟲的開始。維護或修改你的 code 人，很有可能會找不到你的 local state，或者曲解了，這就會浪費很多的時間！

別嫌麻煩，不要寫 local state 吧！

## 埋個伏筆

到目前為止，我們只有了解 store 和 state 的差異，還沒告訴各位要怎麼應用 store 到各個 component 上。但各位可以先看延伸閱讀或文中的連結，了解 store 和 state 的差別。

## 延伸閱讀

1. [通過三張圖了解Redux中的重要概念](https://read01.com/64gPN2.html)
2. [Redux架构实践——Single Source of Truth](http://react-china.org/t/redux-single-source-of-truth/5564)
