---
layout: post
title: "JavaScript to Json 基本觀念"
date: 2015-11-17 16:31:15 +0800
comments: true
categories: 
---
## 緣起
有個朋友詢問我`angular.toJson`這 function為什麼不能轉換到[Json][5]，他只是把他的[angularJS][6] 更換到 1.4.7 版本。
經過了解後，才知道他對於[JavaScript][7]一些觀念不是相當清楚，至於他的問題也不是[angularJS][6]的問題，是他套用的某一個對岸套件影響的，所以他才一直以為錯誤的使用方式是可行的 xd。

## Angular JS 部分
一開始想說會不會是更新[angularJs][6]的關係，所以就查看了一下 1.4.7 的[source code][4]
``` javascript toJson
/**
 * @ngdoc function
 * @name angular.toJson
 * @module ng
 * @kind function
 *
 * @description
 * Serializes input into a JSON-formatted string. Properties with leading $$ characters will be
 * stripped since angular uses this notation internally.
 *
 * @param {Object|Array|Date|string|number} obj Input to be serialized into JSON.
 * @param {boolean|number} [pretty=2] If set to true, the JSON output will contain newlines and whitespace.
 *    If set to an integer, the JSON output will contain that many spaces per indentation.
 * @returns {string|undefined} JSON-ified string representing `obj`.
 */
function toJson(obj, pretty) {
  if (typeof obj === 'undefined') return undefined;
  if (!isNumber(pretty)) {
    pretty = pretty ? 2 : null;
  }
  return JSON.stringify(obj, toJsonReplacer, pretty);
}
```
結果發現這段轉換很久沒更動過了，最後一次更改還是 2014/2/15(想查看的，自己在 NG github 切換到 Blame 查看)，而且仔細看看這 function 內容，還是使用[JSON.stringify][1]這函式。

### [JSON.stringify][1]
再看一次[JSON.stringify][1]這函式的意義

> The JSON.stringify() method converts a JavaScript value to a JSON string, optionally replacing values if a replacer function is specified, or optionally including only the specified properties if a replacer array is specified.
    
清楚明白的寫著可以將[JavaScript][7]值序列化成[JSON][2]

## 範例對比
``` JavaScript 錯誤用法
var foo = [];
foo.bar = "new property";
foo.baz = 3;
var jsonString = JSON.stringify(foo);
```
jsonString 會輸出 `[]`
    
![error sample](/files/2015-11-17/2015-11-17_17-22-26.png)


``` JavaScript 正確用法
var foo = {};
foo.bar = "new property";
foo.baz = 3;
var jsonString = JSON.stringify(foo);
```
jsonString 會輸出 `"{\"bar\":\"new property\",\"baz\":3}"`
    
![sample](/files/2015-11-17/2015-11-17_17-23-16.png)

## 說明
兩個範例的差別主要在`foo`一個是 array，一個是 object，所以在宣告完`var foo`之後，以下這兩個動作
```
foo.bar = "new property";
foo.baz = 3;
```
在 array 的範例中，是指定 foo 的屬性，但是該 foo 的值為 []。
在 object 的例子，則是 foo 的值就是一個物件，且`bar`與`baz`都設定是該物件的屬性。
而[JSON.stringify][1]是轉換值為[Json][5]，所以一個是 **[]**，一個是屬性資料。


## 參考資料
- MDN:[json.stringify()][1]
- w3schools:[JavaScript JSON][2]
- AngularJS:[angular.toJson][3]
- Github:[Angular.Js Source Code][4]

[1]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify "MDN:JSON.stringify()"
[2]:http://www.w3schools.com/js/js_json.asp "w3schools:JavaScript JSON"
[3]:https://docs.angularjs.org/api/ng/function/angular.toJson "AngularJS:angular.toJson"
[4]:https://github.com/angular/angular.js/blob/master/src/Angular.js#L1164 "Github:angularJs"
[5]:http://www.json.org/ "Json"
[6]:https://angularjs.org/ "AngularJS"
[7]:https://developer.mozilla.org/zh-TW/docs/Web/JavaScript "MDN:JavaScript"
[8]:https://developer.mozilla.org/zh-CN/docs/Using_native_JSON "MDN:Using native JSON"