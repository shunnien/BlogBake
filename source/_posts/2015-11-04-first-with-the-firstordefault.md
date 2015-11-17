---
layout: post
title: 'First() 跟 FirstOrDefault()'
date: 2015-11-04 14:46
comments: true
categories: [C#, Linq]
---
## 緣起
前陣子有個朋友跟我詢問一段 [LINQ][1] 的 code，說輸出不是他想要的值，不過當時我去倒杯水，想說回來再看的時候，他自己搞定了 XD，雖然已經解決了，但是既然都抽出時間了，就還是看一下，看到他使用了 First() 去解決，就問他怎麼不使用 FirstOrDefault ，不過那段 code 還是有些需要調整的地方就是了，以下就先來看看這個問題吧(我憑印象中的 code ，可能跟當時的有點落差)。

## 問題
``` C# C#
Dictionary<string, string> Address = new Dictionary<string, string>(){
	{"zipCode","郵遞區號"},
	{"city","縣市"}
};
string str = Address.Where(p => p.Value == "縣市").Select(x => x.Key).ToString();
Console.WriteLine(str);
```
上面的程式碼會輸出以下的結果，但是其目的是想要輸出為 city

```
System.Linq.Enumerable+WhereSelectEnumerableIterator`2[System.Collections.Generic.KeyValuePair`2[System.String,System.String],System.String] 
```
為什麼會輸出這個，也很簡單，LINQ 的 [Select][5] 回傳的型別是`IEnumerable<TResult>`也就是說是個物件，因此在物件後面直接使用 [ToString()][2] 就是直接輸出該物件的型別狀態

## 解決方法
既然知道了原因，那就有了解決方法，加上個`First()`或是`FirstOrDefault()`就可以了，改正如下
```
Dictionary<string, string> Address = new Dictionary<string, string>(){
	{"zipCode","郵遞區號"},
	{"city","縣市"}
};
string str = Address.Where(p => p.Value == "縣市").Select(x => x.Key).First().ToString();
Console.WriteLine(str);
```

## [First][3] 與 [FirstOrDefault][4]
就是看到朋友是使用`First`解決，才想把`First`跟`FirstOrDefault`一起列出來，不過上面的 code 是示意而已，不要太介意為啥這樣寫。現在先來說明，[First][3] 跟 [FirstOrDefault][4] 差別在哪裡，其實兩者相差的點很簡單，使用`Enumerable.First`找不到資料的時候會出錯，而使用`Enumerable.FirstOrDefault` 找不到資料會給予預設值，使用上述的例子來示範一下
``` c# Enumerable.First(會發生錯誤)
Dictionary<string, string> Address = new Dictionary<string, string>(){
	{"city","縣市"}
};
var queryF = Address.First(p => p.Value =="2");
Console.WriteLine(queryF);
```

![Enumerable.First Result](https://googledrive.com/host/0B24tdidnsV1vdzM5VWJwWWNzbGM)

``` C# Enumerable.FirstOrDefault
Dictionary<string, string> Address = new Dictionary<string, string>(){	
	{"city","縣市"}
};
var query = Address.FirstOrDefault(p => p.Value =="2");
if(query.Equals(default(KeyValuePair<string,string>))){
	Console.WriteLine(query.Key);
}
```

![Enumerable.First Result](https://googledrive.com/host/0B24tdidnsV1vMWEzbFJFZl9CczQ)

[1]: https://msdn.microsoft.com/zh-tw/library/bb397897.aspx "LINQ"
[2]: https://msdn.microsoft.com/zh-tw/library/system.object.tostring(v=vs.110).aspx "Object.ToString"
[3]: https://msdn.microsoft.com/en-us/library/vstudio/bb535050(v=vs.100).aspx "Enumerable.First"
[4]: https://msdn.microsoft.com/zh-tw/library/vstudio/bb340482(v=vs.100).aspx "Enumerable.FirstOrDefault"
[5]: https://msdn.microsoft.com/zh-tw/library/vstudio/bb548891(v=vs.100).aspx "MSDN - Enumerable.Select"