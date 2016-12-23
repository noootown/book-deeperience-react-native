# Redux Thunk

## 前言

處理非同步問題，例如發送一個 request 到後端 API server 時，常常需要等回傳值回來，我們才能利用這個回傳值發一個 action 做事。這章要帶各位了解一個套件，叫做 redux-thunk，它會負責處理redux 和非同步的問題。

## 基本寫法

```
const login = () => (dispatch, getState) => {
	dispatch(loginRequest())
    return new ApiFactory().login
      .then(res => {      
        if(loginSuccess) {
			dispatch(loginSuccess())
			new Promise(() => {
			
			}).then(()=>{
				dispatch(....)
			})
		} else {
			dispatch(loginError())	
		}
      })
      .catch((error) => {
        dispatch(getTripContentFailure(error))
      })
  }
}

```
以上程式碼是一個負責處理 login 的 function，首先，在 login 的整個流程，我們必須送出3個 action ，分別是 ```loginRequest```、```loginSuccess``` 或者 ```loginError```  。在各個不同的階段，我們可以根據不同的 action 做不一樣的事。

由於上述這些動作都是在不同的時期所做的 action ，這時候 thunk 就能完美的發揮它的威力。首先，我們把 dispatch 包進 function 裡面，這樣就能在 function 裡面使用 dispatch 。剛進到 function 的時候，我們先發一個 loginRequest 的 action ，代表整個流程的開始。接著，我們會判斷是否 loginSuccess ，來決定我們要發什麼 action 做什麼事。

如果再進一步的思考，會發現一整個流程下來，因為有很多的 promise 傳來傳去，會使得函數一層一層的包起來。因此，如果 promise 一多的話，就會變得很難維護。遇到這種情況，下一章會提供另外一個處理方法，叫做 ```Redux-Saga```。

## 延伸閱讀

1. [Thunk 函数的含义和用法](http://www.ruanyifeng.com/blog/2015/05/thunk.html)
2. [Redux-thunk](https://github.com/gaearon/redux-thunk)