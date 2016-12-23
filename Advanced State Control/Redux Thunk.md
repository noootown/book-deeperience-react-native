# Redux Thunk

## 前言

處理非同步問題，例如發送一個 request 到後端 API server 時，常常需要等回傳值回來，我們才能利用這個回傳值發一個 action 做事。這章要帶各位了解一個套件，叫做 redux-thunk，它會負責處理這個問題。

## 基本寫法

```
const add = () => (dispatch, getState) => {
	dispatch(loginRequest())
    return new ApiFactory().login
      .then(res => {
        
        if(loginSuccess) {
			dispatch(loginSuccess())
			new Promise(() => {
			
			}).then(()=>{
				dispatch(....)
			})
		}
      })
      .catch((error) => {
        dispatch(getTripContentFailure(error))
      })
  }
}

```
從以上程式碼來看

## 延伸閱讀

1. [Thunk 函数的含义和用法](http://www.ruanyifeng.com/blog/2015/05/thunk.html)