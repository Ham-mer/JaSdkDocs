# MoPub
- [MoPub Webサイト](https://app.mopub.com/apps)
- [MoPub 開発者ガイド](https://developers.mopub.com/publishers/ios/get-started/)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDKの導入

AdLime SDK で MoPub を使用するために、 MoPub SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_MoPub'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [MoPubSDKFramework.framework](https://github.com/mopub/mopub-ios-sdk/releases/download/5.11.0/mopub-framework-5.11.0.zip)
- [AdLimeMediation_MoPub.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_MoPub/5.11.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [MoPubSDKFramework.framework](https://github.com/mopub/mopub-ios-sdk/releases/download/5.11.0/mopub-framework-5.11.0.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Mopub"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Mopub > AdLimeMediation_MoPub.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の MoPub フレームワークを追加します。

- AdSupport.framework
- AVFoundation.framework
- CoreGraphics.framework
- CoreLocation.framework
- CoreMedia.framework
- CoreTelephony.framework
- Foundation.framework
- MediaPlayer.framework
- MessageUI.framework
- QuartzCore.framework
- SafariServices.framework
- StoreKit.framework
- SystemConfiguration.framework
- UIKit.framework
- WebKit.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:--------:|:----:|:----------:|:------:|:----:|
|MoPub     |◯     | ◯          |◯       |◯     |

### バナーサイズ
|ネットワーク |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|MoPub    |◯       |◯         |◯        |◯       |◯       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#MoPub) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Mobup の広告枠を配置する前に、 Mobup の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- AdUnit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Mobup を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Mobup 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Mobup 広告を追加してください。

## バージョン情報

### リリースバージョン
| MoPub バージョン    | アダプタ バージョン |
|:-----------------|:----------------|
|5.11.0            |5.11.0.0         |
|5.10.0            |5.10.0.5         |
|5.9.0             |5.9.0.0          |
|5.6.0             |5.6.0.3          |

### バージョン履歴
| バージョン | 日付       | 更新内容                           |
|----------|------------|----------------------------------|
| 5.11.0.0 | 2020/2/18  | - MoPub SDK 5.11.0 に対応<br>- ネイティブ広告はsponsoredをサポートします。AdPrivacyのアイコンをクリックして広告の展示に関する問題を解決します。|
| 5.10.0.5 | 2020/2/5   | 調整モードをサポートします，[初期化](./init.md)を参考してください|
| 5.10.0.3 | 2020/1/22  | 広告イベントのコールバックロジックの改善｜
| 5.10.0.1 | 2019/11/19 | MoPub SDK 5.10.0 バナー に対応     | 
| 5.10.0.0 | 2019/11/7  | MoPub SDK 5.10.0 に対応     | 
| 5.9.0.0  | 2019/10/10 | MoPub SDK 5.9.0 に対応     | 
| 5.6.0.3  | 2019/8/6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
| 5.6.0.1  | 2019/7/15  | 動画リワード広告のイベント最適化|
| 5.6.0.0  | 2019/6/30  | MoPub SDK 5.6.0 に対応     | 
