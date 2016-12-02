# ES6 vs Babel

## 前言

接下來的幾篇文章，會先介紹一些基本的技術和觀念。這一些觀念不僅在本 boilerplate 適用，對 Reactjs, React Native 而言，也都是相當重要的。如果能徹底了解這些常用的觀念，會比較好上手我們的架構。

## ES6 —— JavaScript 由史以來最大的變革

#### 關於 ES6

```ES6```，是 ```ECMAScript 2016``` 的簡稱。在整個 JS 的演化史中，可以說是最重要的一次變革。筆者剛接觸 JS 時，ES6 尚未出來，那時的 JS 在整個風格而言，仍然非常類似其它 C like 語言。怎麼會這麼說呢？請看以下的程式碼。

	// 如果要把下列陣列 [1, 2, 3, 4, 5] 全部都 +1 的話
	// ES5會這麼做：
	
	var arr = [1, 2, 3, 4, 5] 
	for(var i=0; i< arr.length; i++)
		arr[i] += 1

	// ES6 會這麼做：
	arr = arr.map(value => value + 1)

在短短的這一行程式碼裡，隱含很多較新的概念，下面會一一做解釋。

#### 1. 語法糖

所謂的```語法糖（Syntactic sugar）```，就是在程式語法上簡化，讓工程師更好寫程式的寫法。這種表示方法，不影響程式執行的結果，但透過這樣的寫法，程式碼可以變得更簡潔。

在我們的範例程式碼中，其實也有這樣的語法糖。例如 ES5 的函式我們會這樣寫：

	function addOne (value) {
		return value + 1
	}

也就是說我們上述的 ES6 寫法，用 ES5 來寫就是這個樣子：

		arr = arr.map(
			function addOne (value) {
				return value + 1
			}
		)

但是經由語法改寫之後，我們就可以把程式碼改寫成這個樣子：

	let addOne = (value) => value + 1

是不是簡單許多？

如果你有仔細注意的話，會發現上下兩個的寫法有一點不太一樣，前者的參數沒有小括號，後者有，這是因為 ES6 的函式寫法允許我們在只有一個參數的情況下，連小括號都可以不用寫。

除了這個以外，還有一些像是以下的ES6寫法，也都希望各位讀者能去研究。

	// destructuring assignment
	let exampleObj = { a: 1, b: 2 } 
	const { a, b } = exampleObj
	
	const func = (a, b, ...rest) {
		// code
	}

	// template string
	let a = 1
	let str = `a = ${a}`
	console.log(str) // a = 1 	

#### 2. functional programming

所謂的 functional programming，就是把所有的動作，用一個一個的 function ，實作出來，不需要過問過程是怎麼實作的，只要把答案給我就可以了。在上面的第一段程式碼中，我們使用 for 迴圈來親自迭代，但在下面的程式碼中，我們只把我們想實作的功能，丟到 map 這個迭代函式裡，那麼程式碼就給我們正確的結果。

正確來說，functional programming 並不是 ES6 的專利。但因為 ES6 簡潔的寫法，使得 functional programming 的威力，又更大幅度的提高。 除了 map 之外，javascript 還提供了一些有用的函式，像是 [filter](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), [reduce](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 。關於這方面的資料，都可以在 [Mozilla Developers](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript)、[W3C School](http://www.w3schools.com/)、[JavaScript核心](http://weizhifeng.net/javascript-the-core.html) 找到喔。

#### 3. Module 的整合

在 ES6  問世之前，javascript 世界的 module 有很多種，最常見的就是 ```CommonJS``` 和 ```AMD``` 。但話雖如此，還是其它種模組化的方法，和其它語言相比，可說是非常的亂。

模組的好處有非常的多，以下列舉3種：

1. 彈性，容易維護
2. 程式碼重複利用
3. 獨立命名空間

想了解這3個分別是什麼意思的話，建議可以看以下這三篇文章，[文章1](https://github.com/kdchang/reactjs101/blob/master/Ch02/webpack-dev-enviroment.md#javascript-模組化)、[文章2](http://huangxuan.me/2015/07/09/js-module-7day/)、[文章3](https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc#.8nqv7awhg)

ES6 的出現，解決了這個混亂，所有的模組引入引出，全部使用 ```import``` 、 ```export```。這部分想要了解的，可以看[這篇文章](http://www.infoq.com/cn/articles/es6-in-depth-modules)。

#### 4. ES6 Class

在 ES6 問世之前，其實 JavaScript 對於 class 的概念是非常模糊的。雖然我們依然可以使用 Object.defineProperties、object prototype、 object property descriptor 等特性，來實作類似 Java class 的概念，但是總是非常的麻煩。雖然操作起來麻煩，有關 JS object 的基本特性，仍然是非常重要的，有興趣的可以參考 [這一篇](http://www.codedata.com.tw/javascript/essential-javascript-7-ecmascript5-object-properties/)

```ES6 class``` 的來到，解決了這個問題，它把所有有關 Object 的基本特性，全部都封裝起來。關於 class 的用法，可以參考 [這一篇](http://www.codedata.com.tw/javascript/es6-4-maximally-minimal-classes/) 。

## Babel ES6 —— 的經紀人

為什麼說 ```Babel``` 是ES6 的經紀人呢？這是因為 ES6 是很新的標準，尚未所有的瀏覽器都實作，為了讓我們的程式碼可以在瀏覽器中正常運作，我們需要將程式碼轉為 ```ES5```，瀏覽器才看得懂。

那麼轉的這個過程有誰效勞呢？就是```Babel Compiler```。幸運的是，React Native 內建了 babel compiler，所以我們可以用比較好寫的 ES6 來寫我們的 APP。

## 結語
這章簡單介紹了 ES6 和 Babel。關於更深入的用法，就請讀者動動手 Google 囉。

## 延伸閱讀

1. [Functional programming](https://github.com/js-functional/js-funcional)
2. [Babel Compiler](https://babeljs.io/)





