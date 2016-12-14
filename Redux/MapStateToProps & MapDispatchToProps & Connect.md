# MapStateToProps & MapDispatchToProps & Connect

## 前言

我們已經了解了資料可以透過 props 的方式傳入 component，但還沒了解 container 如何獲得資料。這張我們會講到這個部分，然後帶入一些 code 做為講解。

## High order component

首先，我們要大致講解一下 high order component 是什麼。high order component 有一點像是 ES7 的 decorator，我們在 function 傳入一個  class，然後給他加上一點特性後，再傳出一個修飾後的 component。這部分牽涉到很多很細的講解，所以有興趣的讀者，可以看延伸閱讀。

## Connect

react-redux（注意！這是邊是 react-redux，不是redux，因為是連結 react 和 redux） 的 connect ，就是一個 high order component。我們傳入一個 react object，他會替我們的 object 加上一些修飾後，傳出一個新的 object。我們就是利用這個方法，使我們的 container 訂閱 redux store。connect 的寫法如下：

```
class LoginMain extends React.Component {
  render() {
    return (
      <View style={styles.container}/>
    )
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(LoginMain)
```

要注意的是 connect 傳回來的是一個 function，所以我們把 LoginMain 這個 container 放到這個回傳 function 的參數裡面。

connect 共有4個參數，而這邊我們只會講到前兩個，想要了解詳細的讀者，可以參考 [連結](http://cn.redux.js.org/docs/react-redux/api.html)。

## mapStateToProps

mapStateToProps 的功能如名，就是把 store 的資料，一一對應成 container 的 props，寫法如下：

```
const mapStateToProps = state => {
  return {
    device: {
      platform: state.device.platform,
    },
    global: {
      currentUser: state.global.currentUser,
    },
  }
}
```
## mapDispatchToProps

mapDispatchToProps 的功能則是把 redux 的 disptach 注入到 container 裡面。如果 connect 省略 mapDispatch 這個 parameter 的話，那麼預設會注入 dispatch。所以我們可以這樣使用它。

```
this.props.dispatch(actionCreator())
```

但這樣的寫法我個人認為不太好。有以下兩個原因：
1. this.props.dispatch 太冗長，可讀性不佳。
2. dispatch 還要再傳入一個 action creator，這樣的寫法也太過冗長。

因此，我們使用了 redux 的輔助函數 ```bindActionCreators```來解決這個問題。程式碼如下：

```
import { bindActionCreators } from 'redux'
import * as authActions from '../../reducers/auth/authActions'

const actions = [
  authActions,
]

const mapDispatchToProps = dispatch => {
  const creators = Map()
    .merge(...actions)
    .filter(value => typeof value === 'function')
    .toObject()

  return {
    actions: bindActionCreators(creators, dispatch),
    dispatch,
  }
}
```

這段程式碼的意思是，把action creator 直接綁在我們的 props 上。當我們這樣寫之後，我們就可以直接呼叫 action creator 來直接 dispatch action 了，因為這些 action creator 已經綁了 dispatch。

至於 connect 的程式碼，有興趣的讀者可以直接看 react-redux 的原始碼，並不會很難懂。
 
## 結語
這邊，我們只是很簡單的介紹 connect, mapStateToProps, mapDispatchToProps 的功能，根據不同的情況，我們會需要用不同的寫法，那這個部分可以參考 [延伸閱讀3](http://cn.redux.js.org/docs/react-redux/api.html)

## 延伸閱讀

1. [React Higher Order Components in depth](https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e#.dnxwusu5u)
2. [初识React中的High Order Component](https://leozdgao.me/chushi-hoc/)
3. [React-redux API](http://cn.redux.js.org/docs/react-redux/api.html)
4. [connect 原始碼](https://github.com/reactjs/react-redux/blob/master/src/components/connect.js)