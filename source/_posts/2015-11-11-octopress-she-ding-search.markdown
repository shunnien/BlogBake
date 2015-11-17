---
layout: post
title: "octopress 設定 search"
date: 2015-11-11 10:16:22 +0800
comments: true
categories: [blog, Octopress]
---

## _config 設定

此部分需要注意 **url** 與 **simple_search**，這兩個資料設定，**url** 是您自己的部落格位址，**simple_search** 使用預設值就可以；這些是由 [Octopress] 提供的預設搜尋方式，是透過 google 直接搜尋 **url** 這設定值的網站，再查詢這網站裡面有包含查詢關鍵字的頁面。
![_config.yml setting](/files/2015-11-11/2015-11-11_15-13-17.png)

## navigation.html
除非是想要自訂更動，不然使用預設的搜尋方式的話是不需要變動的，
此檔案位置在 */source/_includes/navigation.html*，需要自訂的話，需要變更 form tag 的部分，如下圖圈選區域。
![navigation.html](/files/2015-11-11/2015-11-11_15-40-25.png)
這些動作都完成後，就可以進行`rake gen_deploy`了，就可以看到部落格可以搜尋了。


## 注意事項
當完成上述動作後，發現搜尋沒有結果，有可能是 google 尚未將您的網站登錄，這是 google 有 [Googlebot][2] 會自動去搜尋網站登錄至 google 名單裡面；當然您也可以主動進行登錄，可由[google webmasters][3] 提交。
提交完成後，可以在 google 搜尋進行搜尋檢查是否成功提交了，搜尋方式示範如下
```
site:yourUrl.github.io
```


## 參考資料
- [Octopress]
- [Google 網站管理員][4]
- [Search Console說明:Googlebot][2]
- [耘想科技網頁設計:SEO 網站優化][5]


[1]: https://github.com/yortz/octopress-lunr-js-search "Lunr.js plugin"
[2]: https://support.google.com/webmasters/answer/182072?hl=zh-Hant "Search Console說明:Googlebot"
[3]: https://www.google.com/webmasters/tools/submit-url "Google 提交網站"
[4]: https://www.google.com/webmasters/ "Google 網站管理員"
[5]: http://www.pkthink.com/knowledge-info.asp?id=4 "耘想科技網頁設計:SEO 網站優化"
[Octopress]: http://octopress.org/