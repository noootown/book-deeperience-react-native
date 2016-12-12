# Container vs Component

##  前言

在 redux 和 react 共同構成的架構下，我們建議將全部的元件分成下面兩類，```presentation container``` 和 ```container component```。在這個章節裡，為了對應到我們的檔案結構，我們會將這兩者分別稱為 component 和 container ，並解釋這兩者的差別，以及他們在我們專案裡相對應的位置。

## Container 和 Component 的差別

[這篇](https://chentsulin.github.io/redux/docs/basics/UsageWithReact.html) 是 redux 的官方文件，描述的是  component 和 container 的差別。大致上來說，我們可以把這兩個的功能用以下這個表格解釋，讀者也可以把它跟上面連結的表格做對應：

| |  component | container |
| -- | -- | -- |
| 是否訂閱 redux store | NO | YES |
| 主要用途 | 定義功能或 style 會重複使用的元件 | 整個 DOM 架構的基底 | 
| 資料來源 | 由 props 傳入 | 訂閱 redux store |
| 改變資料 | 透過傳進來的 callback function，更改外部資料 | dispatch action 並更改 store  |
| 寫法 | 通常為 stateless function | 通常為 class |

1. Container 因為要管理資料的原因，所以多半寫為 class。這是因為我們常會需要完整的 react lifecycle 來操作一些同步或非同步的計算。相反的，因為 component 只被動的接收資料的傳入，所以不需要完整的 lifecycle。我們會盡量寫成 stateless function 來增加效能。

2. 例如像 button, footer, header, 這些通常都常都會包裹一個特定的 style ，然後寫成 component，以便重複利用。而 container 則會組合這些可重複利用的 component ，變成一個完整的頁面。

## 檔案架構

```
/src
	/conponents <- component 
	/containers <- container
```

在這兩個資料下，每個 component 或者 container 都還會另外在開一個資料夾。裡面裝著 ```styles.js``` 和 ```index.js```，分別代表著 css 的部分，和 DOM 的部分。其實也有另外一種寫法是直接寫成 ```XXX.js```，這在 javascript  import 的時候，其實是等價的。

```
/src/components
	/btn
		/index.js
		/styles.js

等價於

/src/components/btn.js

import btn from '/src/components/btn'
```

不過我們可以很明顯的看到，後者必須把 style 寫在 btn 裡面。為了可讀性和模組化，我們選擇前者的結構。

而 container 的部分，我們則放在 containers 資料底下，一樣的原則，有 index.js 和 styles.js。另外，在我們的 boilerplate 裡，其實沒有規畫更細部的資料夾。 如果讀者不嫌麻煩，不妨可以再把這兩個資料夾再依自己的喜好，分得更細。

# 延伸閱讀
1. [Container 與 Presentational Components 入門](https://github.com/kdchang/reactjs101/blob/master/Ch08/container-presentational-component-.md)