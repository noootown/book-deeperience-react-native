# React Native Routing

## 前言

```Routing``` 指的是各個畫面之間的路由。如果使用原生 React Native 的 [Navigator](http://facebook.github.io/react-native/releases/0.39/docs/using-navigators.html#using-navigators) ，其實有一點不太方便。這邊我們使用 react-native-router-flux 這個插件，來幫助我們做整個 app 的  routing。

## 架構

Router 的部分，我們寫在 ```src/index.js```。格式大約如下：

```
  class Deeperience extends React.Component {

    constructor(props) {
      super(props)
      this.exitOrNot = false
    }

    render() {
      const store = configureStore({
        initialState: getInitialState(),
        platformDeps: { createStorageEngine },
      })
      // configureStore will combine reducers from snowflake and main application
      // it will then create the store based on aggregate state from all reducers
      store.dispatch(setPlatform(platform))
      store.dispatch(setVersion(VERSION))
      store.dispatch(setStore(store))

      // setup the router table with App selected as the initial component
      // note: See https://github.com/aksonov/react-native-router-flux/issues/948

      return (
        <Provider store={store}>
          <Router
            onExitApp={() => {
              if (!this.exitOrNot) {
                ToastAndroid.show(I18n.t('Toast.pressAgainExit'), ToastAndroid.SHORT)
                this.exitOrNot = true
                setTimeout(() => { this.exitOrNot = false }, 3000)
                return true
              } else return false
            }}
          >
            <Scene key="root"
                   hideNavBar={true}
            >
              <Scene key="LoadingApp"
                     component={LoadingApp}
              />
              <Scene key="Main"
                     component={Main}
              />
              <Scene key="Custom"
                     component={Custom}
              />
            </Scene>
          </Router>
        </Provider>
      )
    }
  }

  Deeperience.childContextTypes = {
    store: React.PropTypes.object,
  }

  AppRegistry.registerComponent('deeperience', () => Deeperience)
```
上面這個 code 可以分成以下幾個部分講解：
1. 先拿到整個專案的 redux store，並傳進provider 。
2. 接著才在裡頭包一個 Router，這個 Router 會負責整個專案的 routing。詳細的routing和換頁用法可以參考 [API](https://github.com/aksonov/react-native-router-flux/blob/master/docs/API_CONFIGURATION.md) 和 [tutorial](https://github.com/aksonov/react-native-router-flux/blob/master/docs/MINI_TUTORIAL.md)。
3. 最後，這部分都設定完後，把整個專案的根，也就是 ```Deeperience``` 給掛載起來。