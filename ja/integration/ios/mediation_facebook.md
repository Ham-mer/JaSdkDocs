# Facebook ドキュメント
- [Facebook Webサイト](https://business.facebook.com/pub/home)
- [Facebook 開発者ガイド](https://developers.facebook.com/docs/audience-network/ios)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDKの導入
AdLime SDK で Facebook Audience Network を使用するために、 Facebook Audience Network SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Facebook'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [FBAudienceNetwork.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/FBAudienceNetwork/FBAudienceNetwork_5.6.0.zip)
- [AdLimeMediation_Facebook.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Facebook/5.6.0.2.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [FBAudienceNetwork.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/FBAudienceNetwork/FBAudienceNetwork_5.6.0.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Facebook"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Facebook > AdLimeMediation_Facebook.framework をプロジェクトにインポートします。

## テスト環境での表示設定
Facebook 広告をテスト環境で利用する場合にはいくつか準備をする必要があります。ここではその準備方法を紹介します。

### 配信条件
Facebook 広告が配信されるには以下のような条件を満たす必要があります。  

1. Facebookアプリが端末にインストールしてあり、ログイン済みである。
1. 端末側で広告ターゲッティングの制限をしない。  
    - "設定" -> "プライバシー" -> "広告" で "追跡型広告を制限"をオフにする。

### 広告が配信されない場合には
アプリ起動時に `AdLime` の `setLogEnable` を `YES` にしてデバッグログ表示設定をしてください。デバッグログを確認し、エラーメッセージを確認してください。
```
ad load failed, error is:
ErrorCode is [3], Message is [No Fill]...
```

上記のようにエラーコード 3、エラーメッセージ No Fill の場合は以下が原因の可能性が高いです。 

1. [配信条件](#配信条件)を満たしていない。
1. Facebook 広告を短時間に多数リクエストをした。<br>
    &rArr; しばらく時間をおいて再度リクエストしてください。
1. Facebook がそのデバイスに配信できる広告がない。


## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:-----:|:----:|:----------:|:------:|:----:|
|Facebook  |◯     | ◯          |◯       |◯     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Facebook    |◯       |◯         |◯        |        |        |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Facebook) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。


## 広告枠の設置
AdLime を使って Facebook Audience Network の広告枠を配置する前に、Facebook Audience Network の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Placement ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Facebook を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Facebook Audience Network 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Facebook Audience Network 広告を追加してください。

## バージョン情報

### リリースバージョン
| Facebook バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 5.6.0            | 5.6.0.2         |
| 5.5.1            | 5.5.1.0         |
| 5.4.0            | 5.4.0.4         |

### バージョン履歴
| バージョン | 日付       | 更新内容                              |
|----------|------------|-----------------------------------|
| 5.6.0.2  | 2020/2/5   | 調整モード、テストモードの設定をサポートします，[初期化](./init.md)を参考してください|
| 5.6.0.0  | 2019/10/10 | Facebook Audience Network SDK 5.6.0 に対応|
| 5.5.1.0  | 2019/10/10 | Facebook Audience Network SDK 5.5.1 に対応|
| 5.4.0.4  | 2019/8/6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
| 5.4.0.2  | 2019/7/15  | 動画リワード広告のイベント最適化        |
| 5.4.0.1  | 2019/7/9   | ネイティブ広告のクリックイベントの改善 |
| 5.4.0.0  | 2019/6/30  | Facebook Audience Network SDK 5.4.0 に対応|
