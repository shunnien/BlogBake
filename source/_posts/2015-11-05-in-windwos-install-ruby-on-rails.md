---
layout: post
title: '在 Windows 安裝 Ruby on Rails'
date: 2015-11-05 03:10
comments: true
categories: [rubyonrails, Windows10]
---
## 緣起
在 Windows 平台上很久了，今年初為了裝一些套件，就安裝了 Ruby，結果今年都快過完了都沒去玩過，只是為了那些套件安裝順利就裝了 ruby，感覺很浪費呀，所以再裝 Rails 進來玩玩，順手記錄一下安裝的過程，為了記錄，我又重新安裝一次 ruby XD。

## 下載安裝檔案 [Ruby][2]
首先到[RubyInstaller][]下載安裝檔案，請依照下圖指示進行。
![RubyInstaller Index](https://googledrive.com/host/0B24tdidnsV1vLU4yOXk5RzFGbkk)
到這頁面選擇符合您自己系統的版本，以下是我的安裝版本
![RubyInstaller Select Version](https://googledrive.com/host/0B24tdidnsV1vYlhqZjJoaXNUcDQ)
然後順便下載 DevKit，一樣選擇適合自己的版本，我是選擇 **For use with Ruby 2.0 and above (x64 - 64bits only)**這版本
![Ruby DevKit](https://googledrive.com/host/0B24tdidnsV1vN2VCZk5ITkI1OEU)

## 安裝 RubyInstaller
執行剛剛下載的 **RubyInstaller**
![RubyInstaller Install](https://googledrive.com/host/0B24tdidnsV1vd0ZMaGtCa2lUT2c)
勾選接受這** License**
![License](https://googledrive.com/host/0B24tdidnsV1vWUVXNUFFbVdOd1E)
選擇您想要安裝的路徑並勾選 **Add Ruby executables to your PATH** 這個選項，這樣安裝程式會自動設定環境變數，等下就可以直接在指令列上執行。
![Destination](https://googledrive.com/host/0B24tdidnsV1vWUVXNUFFbVdOd1E)
然後稍微等個幾秒
![Installing](https://googledrive.com/host/0B24tdidnsV1vR0dxTFpjSTdOMVk)
就可以看到安裝完成畫面
![Completing](https://googledrive.com/host/0B24tdidnsV1vcW40VFJXelBaWVk)
接著我們開啟命令提示字元，或是```Win + R```輸入```cmd```，我以下畫面是使用 [cmder][]，畫面看起來不太一樣，但是功能是相同的；命令提示字元開啟後，鍵入```ruby -v```查看一下 ruby 安裝的版本，應該會是如下圖顯示。
![Version Check Success](https://googledrive.com/host/0B24tdidnsV1vUUZnTVNoN1lGME0)
如果出現[*不是內部或外部命令、可執行的程式或批次檔。*]這訊息，如下圖所示。
![Version Check Failure](https://googledrive.com/host/0B24tdidnsV1vd19vMmZSRm5yTlE)
可能是剛剛沒有勾選 **Add Ruby executables to your PATH**造成，您可能必須手動設定環境變數，需要進入控制台->系統->進階系統設定->進階->環境變數->系統變數->找尋 **Path** 路徑->編輯，把您的 ruby 安裝路徑增加進去
![Set Path](https://googledrive.com/host/0B24tdidnsV1vd1psdVRFajlZME0)

## 安裝 DevKit
執行 DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe，這檔名超長，選擇您想放置的位置，建議放到```C:\RubyDevKit```
![Set DevKit Path](https://googledrive.com/host/0B24tdidnsV1vdERtRi1jUkdtLTA)

如果都是按照上述建議的話，到```C:\RubyDevKit```資料夾下(您所解壓縮的位置下)```Ctrl + shift + mouse right click```選擇開啟命令視窗

![手動設定](https://googledrive.com/host/0B24tdidnsV1vVDBKY1pEa29pVkk)

執行```ruby dk.rb init```，這指令會產生**config.yml**這檔案，並且會偵測您 ruby 安裝的路徑，直接寫入到 config.yml 檔案中
![執行 ruby dk.rb init](https://googledrive.com/host/0B24tdidnsV1vU2drbjUzZzUyRlU)

假如沒有偵測到您的安裝路徑，請手動更改 config.yml 這檔案，用記事本就可以開啟這檔案，按照下圖修改，請修改為您所安裝的路徑，注意路徑語法是```- C:/yourRubyPath```前面有個小破折號
![設定 Ruby路徑](https://googledrive.com/host/0B24tdidnsV1vQXd0aTdvU0RwX0k)

然後執行以下命令，它會更動您 ruby 安裝路徑下的檔案或產生檔案
```
ruby dk.rb install
```
![DevKit Install](https://googledrive.com/host/0B24tdidnsV1vVkVHQ0VFT0dUcXM)

## 安裝 Rails
接下來使用```gem```來安裝，所以下指令就可以安裝完成了，直接下指令安裝 rails
```
gem install rails --no-ri --no-rdoc
```
安裝完成後，測試一下，看一下 rails 版本編號
```
rails -v
```
出現表示安裝完成了。終於弄完這篇文章了，明明裝的時候很快，弄成文章花了不少時間。

## My Environment
- OS:Win 10

## Reference
- [RubyInstaller]
- [Ruby Programming Language][2]

[RubyInstaller]: http://rubyinstaller.org/downloads/
[2]: https://www.ruby-lang.org/zh_tw/ "Ruby Programming Language"
[cmder]: http://blog.miniasp.com/post/2015/09/28/Useful-tool-Cmder.aspx