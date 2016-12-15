# Middleware

## 前言

這章是 Redux 章節的最後一章，我們要講的是 ```middleware```，也是 redux 的一個很重要的概念。在我們的 boilerplate 裡面，也有用到一些 middleware ，有些是為了開發方便，有些是為了開發之用，接著我們會一一介紹。

## middleware 的形式

所謂的 middleware，就是中介的意思。在我們做的所有 action 從開始到結束，都會經這些 middleware。還記得前面章節 ( [傳送門](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Store%20vs%20State.html) ) 有提到 reduxlogger 嗎？他說是一個 middleware。

redux 的 middleware，我們可以寫成下面這個形式：

```
const logger = store => next => action => {
  // do something
  return next(action)
}
```
這邊 store 當然是傳入 redux 的 store，而 next 則是指下一個 middleware 。有興趣的朋友，建議可以直接開 redux 的原始碼來看 middleware 的處理 ( [傳送門](https://github.com/reactjs/redux/blob/master/src/applyMiddleware.js) )。


接著我們只要把它放到 applymiddleware，再 create store 後，之後的action都會經過這個middleware被處裡了。

## 我們使用的 middleware

以下這份 code 放在 ```/src/lib/configureStore.js```。有關整個專案的 middleware 初始都放在這裡。值得注意的是，因為 redux-logger 會拖慢效能，所以我們在 production 版本把它移除了，效能得到很大的增長。

```
const saga = createSagaMiddleware()

const logger = createLoggerMiddleware({
  collapsed: true,
  stateTransformer: state => JSON.parse(JSON.stringify(state)),
})

// const storage = createStorageMiddleware(platformDeps.createStorageEngine)

let middlewares = [
  saga,
  thunk,
  injectMiddleware(platformDeps),
  // storage,
]

if (process.env.NODE_ENV !== 'production') {
  middlewares = [...middlewares, logger]
}
```


## 延伸閱讀
1. [redux的middleware詳解](http://huli.logdown.com/posts/294284-javascript-redux-middleware-details-tutorial)
2. [middleware](http://cn.redux.js.org/docs/advanced/Middleware.html)