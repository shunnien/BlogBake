---
layout: post
title: 'Octopress 加上 Github Pages 移動部落格到 Github'
date: 2015-11-05 03:12
comments: true
categories: [blog, github, Octopress]
---
## 我的環境
```
$ systeminfo | findstr /B /C:"作業系統名稱" /C:"作業系統版本" /c:"作業系統設定" /c:"作業系統組建類型" /c:"系統類型" /c:"處理器" /c:"BIOS" /c:"實體記憶體總計" /c:"虛擬記憶體"

作業系統名稱:         Microsoft Windows 10 專業版
作業系統版本:         10.0.10240 N/A 組建 10240
作業系統設定:         獨立工作站
作業系統組建類型:     Multiprocessor Free
系統類型:             x64-based PC
處理器:               已安裝 1 處理器。
BIOS 版本:            American Megatrends Inc. 219, 2015/5/4
實體記憶體總計:       16,264 MB
虛擬記憶體: 大小上限: 18,696 MB
虛擬記憶體: 可用:     10,390 MB
虛擬記憶體: 使用中:   8,306 MB
```

## 安裝 [Octopress][]

### 下載 [Octopress][1]
請先到 [Github][1] 下載或是直接使用指令碼工具，透過指令進行，以下是使用 SSH
```
git clone git@github.com:imathis/octopress.git
```
要是使用 HTTPS 可以採用以下指令
```
git clone https://github.com/imathis/octopress.git
```
![git clone result](https://googledrive.com/host/0B24tdidnsV1vclY0V2JCMTFxems)

### 安裝 Octopress
首先要安裝 [Octopress][] 要透過 ruby，所以請先安裝 ruby，之後透過指令碼工具進行，首先進入剛剛 clone 下來的資料夾位置
```
cd octopress
```
接著透過 ruby 進行安裝
```
rake install
```
![Octoprss install result](https://googledrive.com/host/0B24tdidnsV1vUkhETGpTemhsbnM)
這樣就安裝完成了，可以使用`rake preview`指令在瀏覽器內觀看，這些指令都是在命令提示字元內執行喔。
![Octoprss preview](https://googledrive.com/host/0B24tdidnsV1vNDB0ZWp2UXZpN3c)
![browser preview](https://googledrive.com/host/0B24tdidnsV1vb0dIQy0xV29uWjQ)
按下`Ctrl + C`可以終止執行

### 建立新的 Repository
沒有 [Github] 帳號的請先註冊喔，這邊都是預設已經擁有 Github 帳號。
首先，先建立一個新的 Repository
![New Repository](https://googledrive.com/host/0B24tdidnsV1vT1JMWHh5akRvY1k)
這個 Respository 的名稱必須是`yourGithubName.github.io`，yourGithubName 必須是您在 Github 上面的帳號名稱，然後建立此 Repository
![Repository name setting](https://googledrive.com/host/0B24tdidnsV1vbmt0c0d0Z3FOUkU)
然後請不要關閉完成頁面，等下會用到新建立的 Repository SSH 位址(使用 HTTPS 位址也可以)
![Repository SSH](https://googledrive.com/host/0B24tdidnsV1vUHFnQlBEM0ZERFE)

### 自己電腦中的 Octopress 發佈(Deploy)到 [Github Pages]
繼續使用命令提示字元，必須在 octopress 資料夾下(您所 clone 的 octopress 位置)，執行以下指令
```
rake setup_github_pages
```
![setup_github_pages](https://googledrive.com/host/0B24tdidnsV1vbk5mYVUzbWRhSW8)
接著執行 
```
rake generate
```
![generate](https://googledrive.com/host/0B24tdidnsV1vcVhGMWxVaVRETmc)

完成之後，就可以進行發佈的指令了
```
rake deploy
```
![deploy](https://googledrive.com/host/0B24tdidnsV1vb052aGhYWEJWNmc)

簡單說明一下，這幾個指令，按照字面應該可以猜得出來，generate 就是產生頁面，deploy 則是發佈出去，setup_github_pages 裡面包含許多設定，有興趣的可以參考 [Octopress] 的說明。發佈完成後，檢查一下網址 `http:yourGithubName.github.io/`，yourGithubName 就是你建立 Repository name 
![deploy browser preview](https://googledrive.com/host/0B24tdidnsV1vR1ZxcTBITHFSN1k)

最後，記得把原始檔案進行版控，放到 source branch 吧。
```
git add .
git commit -m "您所要輸入的備註內容"
git push origin source
```
![git to source](https://googledrive.com/host/0B24tdidnsV1vTnRuOVBSWGU1U3c)

這樣就完成您的部落格了，接著就可以使用 markdown 語法撰寫您的文章。

### 部落格設定
有兩個方式，一個是下指令，一個是直接更改 _config.yml 這個檔案，想經由指令進行更動的話，可以參考一下 Octopress 上面的 [Configuring Octopress] 使用方式，以下說明在 octopress 資料夾下更改 _config.yml 檔案的的介紹(這樣更改感覺比較快速一點 XD)。
首先先到您 clone octopress 路徑下，使用 sublimeText(或是notepad、記事本等其他文本編輯器都可以)開啟，然後直接修改，修改時，記得注意每一個冒號後都要空格，不然等下執行`rake generate`產生檔案時會發生錯誤，所以這點要注意。接著更動後記得存檔，並執行下列
```
rake generate
rake deploy
```

![edit _config.yml](https://googledrive.com/host/0B24tdidnsV1vN2gwY09CWkRMOU0)

在執行 `rake deploy`時，我發生了 *LF will be replaced by CRLF* 這些錯誤，如果發生這個錯誤，可以試著執行以下指令，把 git 的 aurtocrlf 取消
```
git config --global core.autocrlf false
```

### 發表文章
此部分可以參考 [Blogging Basics][2]，語法相當簡易，一樣使用指令碼
```
rake new_post["title"]
```
這時候 Octopress 會幫您產生文章檔案，此檔案會放到 `source/_posts/`這路徑底下，接著您可以使用習慣的文字編輯器，編輯這些文章，編輯結束想觀看文章在部落格上的呈現時，可以使用
```
rake preview
```
上述有提到這個指令的功能，此功能就是模擬一個 web 服務，讓您可以在本機端使用瀏覽器觀看執行結果；有寫過 web 開發的應該不會陌生，這就是本機測試。
確認完成編輯後，進行 generate 產生需要的設定與檔案，之後發佈
```
rake generate
rake deploy
```
這兩個語法可以合併使用以下指令，就是上述兩個指令的合併使用
```
rake gen_deploy
```

差點忘了提醒，記得進行版控喔。


#### 參考資料：
- [國王的耳朵是驢耳朵:安裝octopress並佈署到github pages上面](http://wen00072-blog.logdown.com/posts/258497-octopress-installed-and-deployed-on-the-github-pages#oct-env "國王的耳朵是驢耳朵:安裝octopress並佈署到github pages上面")
- [李嘉玲的技術筆記:Github Page + Octopress](http://zerodie.github.io/blog/2012/01/19/octopress-github-pages/ "李嘉玲的技術筆記:Github Page + Octopress")
- [生命之氢:Octopress 搭建流程 – Github Pages](http://shengmingzhiqing.com/blog/setup-octopress-with-github-pages.html/ "生命之氢:Octopress 搭建流程 – Github Pages")
- [Octopress]
- [Github Pages]
- [Blogging Basics][2]
- [Configuring Octopress]

[Configuring Octopress]: http://octopress.org/docs/configuring/
[Github]: https://github.com/
[1]: https://github.com/imathis/octopress "Octopress Github"
[Octopress]: http://octopress.org/
[GitHub Pages]: https://pages.github.com/
[2]: http://octopress.org/docs/blogging/ "Blogging Basics"