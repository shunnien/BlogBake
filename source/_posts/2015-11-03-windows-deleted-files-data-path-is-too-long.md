---
layout: post
title: 'windows 刪除資料路徑太長的檔案'
date: 2015-11-03 06:04
comments: true
categories: [npm, Windwos]
---
在 windows 系統中用 npm 裝了一些 generator 後，有些路徑長得不像話，很容易就爆了，砍都砍不掉，就像下圖。
![錯誤畫面](https://googledrive.com/host/0B24tdidnsV1veC1vNUc4NUhheWM)
當時又不想靠 7-zip 來刪除檔案，就想找有沒有便利的工具直接下指令刪除了，剛好看到這工具挺方便的

## 問題環境
> npm version:2.11
> OS: win 10

## 問題原因
一方面是 npm 的設計，另一方面是 windows 環境下的問題，windows 下路徑檔名有長度限制。
對於 npm 在 windows 環境下的設定與路徑說明，可以參考[保哥的文章][3]；不是 npm 產生這問題的，也可以考慮以下解決方式，話說以前好像玩遊戲的時候搞出這種問題 ><。

## 解決方式
遇到這種情形，解決方式有幾點
* 改檔名，把路徑改到符合長度限制
* 第三方工具

第一種方式的土法煉鋼，除了真的想嘗試手指運動的人，我想應該不會有人想要這樣做，除非路徑長度剛好超出限制一點點。
工具的部分介紹大家兩種：
* [7-zip][4]，這是圖形化介面，簡單說就是滑鼠操作一下，今天就不說這個工具，想知道怎麼操作的可以參考一下 [demo 哥的文章][5]
* [rimraf][1]，以下介紹這工具

### 第三方工具 [rimraf][1]
這工具是 npm package ，可以直接在 cmd 直接執行，符合我的需求。順便說一下，我使用 npm 預設路徑，套用 Yeoman 的 Hottowel generator，擷取一小部分其檔案結構來看，應該不會有人想要一一刪除檔案
![tree view](https://googledrive.com/host/0B24tdidnsV1vNURfVm1PczF5U2s)

### 操作方式
```
rimraf(f, callback)
```
![cmder view](https://googledrive.com/host/0B24tdidnsV1vbUVhSmVtU0FlM0E)

[1]: https://www.npmjs.com/package/rimraf "rimraf"
[2]: http://www.nikola-breznjak.com/blog/nodejs/how-to-delete-node_modules-folder-on-windows-machine/ 
[3]: http://blog.miniasp.com/post/2015/09/02/Change-npm-default-global-installation-directory-for-nodejs-modules-in-Windows.aspx "保哥 如何在 Windows 平台變更 Node.js / npm 全域模組的預設安裝路徑"
[4]: http://www.7-zip.org/ "7-zip"
[5]: http://demo.tc/post/811 "demoshop - Windows 系統中資料路徑太長無法刪除的解決辦法"