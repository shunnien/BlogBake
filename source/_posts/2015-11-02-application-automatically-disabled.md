---
layout: post
title: 'Application Automatically Disabled'
date: 2015-11-02 07:26
comments: true
categories: [IIS7.5]
---
以下使用的 Server
> Server：Win2008 R2

記錄一下 Server 的一些小事件，主要是因為早上突然發生了這個畫面
![錯誤畫面](https://googledrive.com/host/0B24tdidnsV1vb1Mya1AyZG1lcEE)
一看就很明顯 Service 停止了，進去 Server 然後到 IIS 將 Application Pool Start 就好了；但是到底是如何自動關閉的，查看 **Event Viewer** 發現 IIS 有設定機制自動關閉的，訊息如下。
![Event Viewer](https://googledrive.com/host/0B24tdidnsV1vZjVudzhfcGs3MUU)

## Rapid-Fail Protection
好吧，得知了有自動關閉機制，應該可以調整設定吧，繼續到 IIS -> Application Pools 如下圖
![Application Pools](https://googledrive.com/host/0B24tdidnsV1vQ241cHAzd0NVazQ)
![Advanced Settings](https://googledrive.com/host/0B24tdidnsV1vNm5wRU5wTXRFY2c)

設定的意義非常簡單，就是幾分鐘內發生幾次錯誤就自動關閉，想要詳細了解的可以參閱一下 [MSDN][1] ；至於怎麼樣的警告會進行自動關閉呢？就是 IIS 發生錯誤，例如：IIS 發送 EMail 發送失敗...等等。此次就是因為信件發送的問題導致。
[1]: https://msdn.microsoft.com/zh-tw/library/cc779875(v=ws.10).aspx "設定 IIS 6.0 中的快速失敗保護"





