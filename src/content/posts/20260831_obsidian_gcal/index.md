---
title: ObsidianにGoogle Calendarを同期する
published: 2026-08-31
description: 'ObsidianのCalendarをGoogle Calendarに置き換えて，予定を見れるようにしよう！'
image: './item/thumbnail.webp'
tags: [Obsidian, Google Calendar, Google Cloud]
category: 'ソフトウェア'
draft: false 
lang: 'ja'
---

obsidianを使っている方なら当然デイリーノートを書いているかなと思います  
そしてデイリーノートを確認するときにはObsidianのCalendarプラグインを当然のごとく使ってますよね？

せっかくカレンダーを見るなら，予定とか見れたら良くね？と思ったので，そんなプラグインを導入してみました  
プラグイン名はGoogle Calenderだそうです．そのまんまの名前ですね

導入したら以下の画像のようにObsidianのカレンダーからGoogle Calendarの予定が見れるようになります

![obsidian-calendar](item/obsidian_calendar.webp)

# 導入手順
一応こちらでも紹介しますが，以下のページを参考にした方が確実かもしれません

https://yukigasai.github.io/obsidian-google-calendar/Setup

## プラグインをインストール
まずはコミュニティプラグインストアでお使いのObsidianにプラグインをインストールしてください

https://community.obsidian.md/plugins/google-calendar

有効化もお忘れなく

## Google Calendarを同期するためのプロジェクトの作成
Google CalendarをObsidianに同期するにはGoogle Cloudのプロジェクトを作成し，カレンダーの情報を共有する必要があります

### Google Cloudへのアクセス
まず，Google Cloudへアクセスしてください

https://console.cloud.google.com/welcome

### 新規プロジェクトの作成
1. 左上のプロジェクトの選択(環境によっては作成済みのプロジェクトが出てるかも)を押して，プロジェクト一覧を開きます
2. 新しいプロジェクトを作成を選択します
![新規プロジェクトの作成①②](item/project12.webp)
3. 好きなプロジェクト名をつけます
4. 「作成」を選択します
![新規プロジェクトの作成③④](item/project34.webp)
5. 通知欄から作成したプロジェクトを選択します
![新規プロジェクトの作成⑤](item/project5.webp)
6. 上の検索バーを選択し，「Google Calendar API」と入力します
7. 「Google Calendar API」を選択します
![新規プロジェクトの作成⑥⑦](item/project67.webp)
8. 「有効にする」を選択します
![新規プロジェクトの作成⑧](item/project8.webp)
9. 「OAuth 同意画面」を選択します
![新規プロジェクトの作成⑨](item/project9.webp)
10. 「開始」を選択します
![新規プロジェクトの作成⑩](item/project10.webp)
11. アプリ名に「Obsidian Google Calendar」と入力します
12. ユーザーサポートメールは自分のメールアドレスを選択します
13. 「次へ」を選択します
![新規プロジェクトの作成⑪⑫⑬](item/project111213.webp)
14. 対象を「外部」にします
15. 「次へ」を選択します
![新規プロジェクトの作成⑭⑮](item/project1415.webp)
16. 連絡先情報に自分のメールアドレスを入力します
17. 「次へ」を選択します
![新規プロジェクトの作成⑯⑰](item/project1617.webp)
18. チェックボックスをチェックします
19. 「次へ」を選択します
![新規プロジェクトの作成⑱⑲](item/project1819.webp)
20. 「作成」を選択します
![新規プロジェクトの作成⑳](item/project20.webp)
21. サイドメニューの「クライアント」を選択
22. 「クライアントを作成」を選択
![新規プロジェクトの作成㉑㉒](item/project2122.webp)
23. アプリケーションの種類に「ウェブアプリケーション」を選択します(下の名前の欄はなんでも良いです)
![新規プロジェクトの作成㉓](item/project23.webp)
24. 承認済みのJavaScript生成元に以下のURIを記載します
```
http://127.0.0.1:42813
```
```
https://google-auth-obsidian-redirect.vercel.app
```
25. 承認済みのリダイレクトURIに以下のURIを記載します
```
http://127.0.0.1:42813/callback
```
```
https://google-auth-obsidian-redirect.vercel.app/callback
```
26. 「作成」を選択します
![新規プロジェクトの作成㉔㉕㉖](item/project242526.webp)
27. クライアントIDをコピーしておきます
28. 同じようにクライアントシークレットもコピーしておきます
![新規プロジェクトの作成㉗㉘](item/project2728.webp)
29. 左のメニューの「対象」を選択します
30. テストユーザーの「Add users」を選択します
31. 自分のメールアドレスを入力します
32. 保存を選択します
![新規プロジェクトの作成㉙㉚㉛㉜](item/project29303132.webp)

Google Cloudでの作業は以上です

### ログイン
ObsidianでGoogle Calendarプラグインの設定を開いておいてください
1. 「Use Own authentication client」のトグルをを有効化します
2. 「ClientId」に先ほどコピーしたクライアントIDをペーストします
3. 「ClientSecret」に先ほどコピーしたクライアントシークレットをペーストします
4. 「Login with google」の「login」をクリックします
![ログイン①②③④](item/login1234.webp)
5. Googleのログイン画面が出てくるのでログインしてください(ObsidianのWebビューアーだと上手く行かないことがあります．その場合外部のブラウザで開くように設定を変更してください)
6. 「このアプリはGoogleで確認されていません」とでるので「続行」を押してください
7. 「Obsidian Google Calendar が Google アカウントへのアクセスを求めています」と出るので「すべて選択」し，「次へ」を選択

設定は以上で終わりです．お疲れさまでした！

# 使い方
## calendarの表示
コマンドパレットで「gCal month view」を追加してあげると，Obsidianのカレンダープラグインと近い形で利用できます

下の画像の左はObsidianのgCal month view，右は普通にブラウザでGoogle Calendarを開いた例です  
Google Calendarの予定が，ObsidianのgCal month viewにも反映されていることがわかります
![gcal-month-view](item/obsidian_gcal_month.webp)

もちろん，Create daily noteから，デイリーノートを表示，記入することもできます  
これをObsidian標準のカレンダープラグインの代わりにサイドバーに設置してあげると良い感じになると思います

他にも週での表示や年間での表示，その日のスケジュールなどの表示方式も選べます  
このあたりは自分で，コマンドパレットから探してみてください

## イベントの編集
表示されたイベントを右クリックでイベントの編集が可能です
![gcal-event-edit](item/obsidian_gcal_event_edit.webp)

編集したイベントは，Google Calendarにも同期されます  
Obsidian上でカレンダーを編集できるのはなかなか便利です

## 他の機能について
他にもいろんな機能があるみたいですが，自分は使いこなせてません  
このページにビューやイベントノートについてやコマンド一覧などが載っているので詳しく知りたい人は見てみると良いと思います

https://yukigasai.github.io/obsidian-google-calendar/

# 終わりに
今回はObsidianにGoogle Calendarを導入する方法を紹介しました

プラグインを作ってくださった方には頭が上がりません