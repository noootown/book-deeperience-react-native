# Lint & Coding Style

## 前言

好的 coding style ，對團隊來說是一個莫大的幫助，當所有的人寫法，都像同一個人寫的時候，那麼程式碼就容易讀，也減少彼此之間的磨擦。這篇文我會列舉一些我覺得相對重要的 coding style，跟大家分享。

本 boilerplate 使用的 coding style 絕大部分選自 [Airbnb coding style](https://github.com/airbnb/javascript) ，再加上一些個人的理解，集合而成的。

## Linter

#### 關於 ESLint

所謂的 linter 就是檢查我們程式碼寫法的工具。我們的 boilerplate 選用的 linter ，是 JS 世界裡，最多人使用的 ```ESLint```。我們會選用 ESLint，在於 ESLint 有以下幾個大優勢。

1. 擁有很多的插件
2. 設定起來也十分容易，可以隨時更換設定

另外，設定檔在 [.eslintrc.json](https://github.com/noootown/deeperience-react-native/blob/master/.eslintrc.json)，設定的細項可以參照[這篇](http://eslint.org/docs/rules/)。

#### 使用方法

在 terminal 輸入```npm run lint```，可以自動檢測寫法錯誤。而 ```npm run fix-lint```，可以自動修補程式碼。

## 常見的設定

1. max-len

這個設定是規定一行最多可以塞多少個字元。以 python 來說，上限長度最好是設定80，但JS 就沒有這個規定。80這個數字是在以前螢幕比較小時所留下來的習慣，但現在已沒有這個問題。但一般來說，還是會設到80 ~ 120左右。我們的boilerplate 考慮到80有一點點太短了，所以就設成120。太長的話，程式碼不好看，也不能將營幕切成兩格。太短也不好，因為這樣要一直做沒有意義的換行，這部分全看讀者自己怎麼設定。

2. comma-dangle

comma-dangle 是指物件的最後，是否要多留一個逗號。這部分的話，我個人的建議是留，主要是以下兩個原因：

- github commit 的問題

```
//  初始程式碼
let obj = {
	a: 1,
	b: 2
}

// 修改後的程式碼
let obj = {
	a: 1,
	b: 2,
	c: 3
}
```

如果不加上最後一個 dangle comma 的話，那麼 git 就會自動判定 b 那行也被更改了。反之如果有加上dangle comma 的話，那就會判定成只修改過c。

- 方便問題

	如果沒有加上dangle comma的話，就要一直去記著後面是不是有多的comma，那如果還要再加新的 attribute，就還要為前面的 attribute 補上comma，太麻煩了！

3. 統一風格

這種的 rule 主要是為了統一風格所致，例如 ```space-before-function-paren```、```arrow-spacing```。

```
// Good
	(a) => {}
// Bad
	(a)=>{}
```

4. react class 的規定寫法

這部分是屬於額外的 [插件](https://github.com/yannickcr/eslint-plugin-react)，因為 react 具有很多的 lifecycle，也有獨特的 jsx 寫法，如果沒有規定好的話，可能會造成一團亂。這部分就讀者們自行點連結出來看囉。

## 結語

本篇文是 basic 系列的最後一篇，介紹了代碼品質監控的工具。當然在安裝 JS 的 lint 時，你可以選擇直接照抄 Airbnb 的 style。但我們希望讀者在讀完這篇後，能思考一下，該如何設計自己的 coding style，對團隊最適合，最有幫助。

## 延伸閱讀

1. [淺入淺出 eslint 與實作](http://denny.qollie.com/2016/07/11/eslint-fxcking-setup/)