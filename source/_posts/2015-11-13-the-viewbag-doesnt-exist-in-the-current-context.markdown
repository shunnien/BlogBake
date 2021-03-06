---
layout: post
title: "Visual Studio 2015 The ViewBag doesn't exist in the current context"
date: 2015-11-13 21:13:41 +0800
comments: true
categories: [visual studio 2015, asp.net mvc 5]
---
## 緣起
今日在操作系統的時候，發現系統不給進行下一個操作，想說怎麼回事？就趕快來查找一下紀錄。
發現原來是新接手負責的人員，資料沒有照要求輸入(這完全不限制的輸入還是照著需求調整的，~~真是自作孽~~)，所以下一環節的處理直接就濾掉了。
所以後來將此環節的處理放鬆並設定預設資料與例外處理，就把這問題處理掉。
但是可能一陣子沒開 **Visual Studio 2015**，我的 cshtml 頁面，都會出現小紅線，仔細去看，都是
**The ViewBag doesn't exist in the current context** 大概這樣的訊息，個人實在討厭這種紅色的訊息，所以還是想把它處理掉。

## 處理過程
印象中，以前 VS2012(Visual Studio 2012) 好像有處理過相同的問題，這一看就是 **ASP.NET MVC** 的元件引用有問題，可是查看 output 居然沒訊息 orz...。
好吧，開個安全模式建立一個新 MVC 專案看看是不是那專案是不是有調整，使用指令碼開啟安全模式，記得要在 VS2015(Visual Studio 2015)執行檔的路徑下執行

```
devenv /safemode
```
![VS2015 safemode](/files/2015-11-14/2015-11-14_00-40-50.png)

開啟結果，還是有紅色訊息。只好去 StackOverflow 找一下，發現了[Why does VS2015RC says...][1](這名稱有點長，我就省略了)，可以在每個`.cshtml`檔案引用
```
@inherits System.Web.Mvc.WebViewPage<dynamic>
``` 

引用後，的確紅線的提醒消失了，但是要每一頁去引用，簡直是無法想像呀，所以這方法果斷放棄。
仔細想一想，要是我重新把 **ASP.NET MVC** 元件重新安裝，應該會好吧，可是不太想進行這動作，查詢了一下，看到[這篇][2]說出解決方式是更新 MVC 元件或是修改 config，把 System.Web.Mvc 手動變更。
原本我已經打算按照這方式進行了，但是後來看到[這篇][3]，抱持著我只進行這重設 userdata 的動作就好，結果我的 VS2015就好了
```
devenv.exe /resetuserdata
```


## 參考資料

- [StackOverflow:Why does VS2015RC says...][1]
- [sign me out:The name 'ViewBag' does not exist in the current context][2]
- [StackOverflow:Visual Studio 2015 Broken Razor Intellisense][3]
- [The ASP.NET Site:How to Upgrade an ASP.NET MVC 4 ... to ASP.NET MVC 5 ...](http://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2)


[1]: http://stackoverflow.com/questions/31232394/why-does-vs2015rc-says-the-viewbag-doesnt-exist-in-the-current-context-where "StackOverflow:Why does VS2015RC says “The ViewBag doesn't exist in the current context”, where as VS2013 says no errors?"
[2]: http://bjkeizer.blogspot.tw/2015/01/the-name-viewbag-does-not-exist-in.html "sign me out:The name 'ViewBag' does not exist in the current context"
[3]: http://stackoverflow.com/questions/31581666/visual-studio-2015-broken-razor-intellisense "StackOverflow:Visual Studio 2015 Broken Razor Intellisense"
