# Jest

## 前言

這章要介紹的也是 Facebook 開源計劃的項目 ```Jest```。Jest 和 Flow 不一樣，是一個單元測試的套件，可以完整的測試 UI、component 和 API 的功能。那麼接下來的兩章，我會大概提到撰寫 unit test 的方式。

## 架構

首先，我們要來提一下 Jest 這個套件的優點。 Jest 是由 ```Jasmine``` 這個框架發展而來的，因此在語法撰寫上，並沒有太大的差異。然而，我認為 Jest 在前端開發上有一個非常 OP 的地方，就是可以把 component snapshot 起來。

snapshot 起來是什麼樣的概念呢？就是類似替 component 照相。那麼如果我有動到 component 的樣式的話，我就可以比對到底哪裡不一樣。

接著我們看專案的 test 結構。

```
/src
	/__mocks__
	/components
		/__tests__
			/__snapshots__
```

1. __ mocks __

mocks 這個資料夾放的是第三方套件的 mock function。所謂的 mock，就是假扮的意思。在寫程式的時候，我們常會援引第三方套件，然後第三方套件可能又援引起他套件。但是這樣引來引去，對測試來說一點都不重要，我們只關係 input 丟進這個套件，ouptput 出來會是什麼而已。這時候就可以在這邊寫上我們的function。

例如 ```src/__mocks__/react-native-simpledialog-android.js```，我們並不關心它到底有沒跑出一個提示字窗，所以我們就直接把它 mock 起來。

```
var SimpleAlert = {};

SimpleAlert.alert = jest.genMockFunction();

module.exports = SimpleAlert;
```

2. __ tests __

這個資料夾放的是 component 的邏輯 test，最後一行的 toMatchSnapshot()，會去比對 ```__snapshots__``` 資料夾裡的檔案，如果沒有相對應的檔案，那麼就會自動產生一個。

```
import renderer from 'react-test-renderer'

test('FormButton', () => {
  const props = {
    isDisabled: false,
    onPress: () => {},
    buttonText: 'TestString',
  }
  const tree = renderer.create(<FormButton {...props} />).toJSON()
  expect(tree).toMatchSnapshot()
})
```

3. __ snapshots __

這裡放的就是 test 產生出來的 snapshot 檔案喔。如果想要更新的話，只要刪掉，再跑一次 test就好

寫完測試檔案後，只要在 terminal 輸入 npm test 就可以了。那麼會先跑 Jest，跑完之後，再跑下一章我們要講的 mocha。

## 延伸閱讀

1. [react组件的测试工具jest](http://dj1211.com/?p=673)