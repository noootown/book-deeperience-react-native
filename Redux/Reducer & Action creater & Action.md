# Reducer & Action creater & Action

## 前言

這章要開始講解 redux 中重要的三個部分，```reducer```, ```action creator```, ```action```。首先，我會比較兩種不同的檔案架構，接著我們會提到這三者在 boilerplate 的位置。如果還不了解這三者的功能，請看 [連結](https://noootown.gitbooks.io/deeperience-react-native-boilerplate/content/Redux/Redux%20&%20React.html) 。

## 不同的架構

在 Reducer, Action creater, Action 這部分，一般的 boilerplate 有兩種分法。第一種是和這三者去分，另一種是按元件功能分。

如果是按 reducer 和 action creator 下去分，那麼檔案結構會長這個樣子，其中的 global, auth, custom，分別代表各個功能。

```
/src
	/reducers
		/global
			/globalReducer.js
		/auth
		/custom
	/actions
		/global
			/globalAction.js
		/auth
		/custom
```

在我們的檔案結構裡，則是分成如下：

```
/src
	/reducers
		/global
			/globalAction.js
			/globalReducer.js
			/globalInitialState.js
		/auth
		/custom
```
這兩種分法，其實沒有好壞，也沒有誰是 best practice。但我們會選擇下面這種檔案結構，其實有下面幾個原因：

- 因為一個 redux 的操作都含有 action creator, reducer，甚至在初始化的時候，也有 initialState，那把它放在一起比較方便管理，減少上層目錄的數目。
- 除了上面提到的這三個檔案之外，還有可能會有其它檔案幫忙，例如：假數據、helper function、unit test等。寫成這個樣子的話，那麼這一些檔案就可以直接和上述檔案放在一起，方便管理。

## 我們的檔案架構和寫法

在這個小節裡，我會分別的講解一下各個檔案的 code 寫法，注意，code是節錄的。

#### 1. reducer

首先，我們會取得一個 initialState 的實體，如果reducer沒有state的傳入的話，那我們就傳 initialState 進去。接著，根據 aciton type，我們會判斷要更改 store 的哪一個部分。這邊設值時，使用的是 immutableJs 的API ，這部分會在之後的章節做講解。

```
'use strict'
import InitialState from './customInitialState'

const {
  SET_HOTEL_TYPE,
  SET_TRIP_LOCATION,
  SET_TRIP_ELEMENT,
} = require('../../lib/constants').default

const initialState = new InitialState()

export default function customReducer(state = initialState, action) {
  if (!(state instanceof InitialState)) return initialState.mergeDeep(state)

  const tripFee = state.getIn(['tripFee'])
  const residentFee = state.getIn(['residentFee'])
  const day = state.getIn(['day'])
  const tripElement  = state.getIn(['tripElement'])
  switch (action.type) {
    case SET_HOTEL_TYPE:
      return state.setIn(['hotelType'], action.payload.type)

    case SET_TRIP_LOCATION:
      return state.setIn(['tripLocation'], action.payload.tripLocation)

    case SET_TRIP_ELEMENT:
      return state.setIn(['tripElement'], action.payload.tripElement)

	case SET_STATE:
		return state
  }
}
```

#### 2. action creator 和 action

首先，我們先把所有需要的 action type 都 import 進來。接著，我們針對每一個 action type 寫一個 action creator。雖然我們的 boilerplate 沒有強制定義 action 的格式要長什麼樣子，但一般來說，最好都是一個 type 配一個 payload。如果有 paylaod 的話，那讓它成為一個物件。

```
const {
  SET_FEE,
  SET_DAY,
  SET_HOTEL_TYPE,
  SET_TRIP_LOCATION,
  SET_TRIP_ELEMENT,
  TOGGLE_TRIP_ELEMENT,
  SET_OTHER_DEMAND,
  RESET_CUSTOM,
} = require('../../lib/constants').default

export function setTripLocation(tripLocation: number) {
  return {
    type: SET_TRIP_LOCATION,
    payload: {
      tripLocation,
    },
  }
}

export function setTripElement(tripElement: any) {
  return {
    type: SET_TRIP_ELEMENT,
    payload: {
      tripElement,
    },
  }
}
```





