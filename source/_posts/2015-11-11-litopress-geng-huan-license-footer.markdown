---
layout: post
title: "octopress 更換 license(footer)"
date: 2015-11-11 16:44:05 +0800
comments: true
categories: [blog, Octopress]
---
## 緣起
現在網路上大家都很注重產權，因此應該在 footer 標示授權，而且還可以自己更動一下 footer 

## [Creative Commons]
首先建立自己的授權資訊，因此進入 [Creative Commons] 連結，點選 **Licenses** 的選單，出現下拉選單後，選擇 **Choose a License**
![CC Index munu choose](/files/2015-11-11/2015-11-11_16-58-17.png)

此頁面有提供多語言轉換，所以頁面底下可以選擇看的懂的語言。
![CC choose language](/files/2015-11-11/2015-11-11_17-00-41.png)

設定完成後，按照頁面上的指示，複製這一段 code，貼到您想更動的位置就可以
![CC copy area](/files/2015-11-11/2015-11-11_17-04-14.png)

## Octopress footer 更動
首先找到們要更動的頁面，我想要放置到 footer 位置，所以到 *source/_includes/footer.html* 查看一下內容

``` html source/_includes/footer.html
include custom/footer.html
```

可以看出此頁面加入了 *custom/footer.html* 這個檔案，所以查看該檔案

``` html custom/footer.html
<p>
    Copyright &copy; {{ site.time | date: "%Y" }} - {{ site.author }} -
    <span class="credit">Powered by <a href="http://octopress.org">Octopress</a></span>
</p>

```

把剛剛上述複製那段放進去，像以下這樣。

```
<p>
	<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

    Copyright &copy; {{ site.time | date: "%Y" }} - {{ site.author }} -
    <span class="credit">Powered by <a href="http://octopress.org">Octopress</a></span>
</p>
```

最後記得先`rake preview`觀看一下，確認沒問題再行發布，然後記得版控。


## 參考資料
- [Creative Commons]
- [台灣創用CC計畫]
- [Octopress]

[台灣創用CC計畫]: http://creativecommons.tw/
[Creative Commons]: http://creativecommons.org/
[Octopress]: http://octopress.org/