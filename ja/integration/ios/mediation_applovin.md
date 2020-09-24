# AppLovin
- [AppLovin Webサイト](https://dash.applovin.com/)
- [AppLovin 開発ガイド](https://dash.applovin.com/docs/integration#iosIntegration)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDKの導入
AdLime SDK で Applovin 広告ネットワークを使用するために、AppLovin SDK と AdLime Adapter SDKを導入してください。

### CocoaPods（推奨）
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_AppLovin'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動ダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AppLovinSDK.framework](https://bintray.com/applovin/iOS/download_file?file_path=applovin-ios-sdk-6.12.8.zip)  **（要ログイン）**
- [AdLimeMediation_AppLovin.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_AppLovin/6.12.8.1.zip)
- AdLimeMediation_AppLovin_Resources.bundle

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AppLovinSDK.framework](https://bintray.com/applovin/iOS/download_file?file_path=applovin-ios-sdk-6.12.8.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_AppLovin"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_AppLovin > AdLimeMediation_AppLovin.framework をプロジェクトにインポートします。

## その他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の AppLovin フレームワークを追加します。

- AdSupport
- AVFoundation
- CoreGraphics
- CoreMedia
- CoreTelephony
- SafariServices
- StoreKit
- SystemConfiguration
- UIKit
- WebKit
- libz.tbd

##  Info.plist の更新
Info.plist ファイルに、 AppLovinSdkKey キーと、 AppLovin SDK Key を追加します。 [AppLovin 管理画面](https://dash.applovin.com/docs/integration#iosIntegration)で SDK Key は取得できます。

Info.plist を ソースコードとして開いて編集します。
```objectivec
<key>AppLovinSdkKey</key>
<string>Your AppLovin SDK Key</string>
```

もしくは、プロパティリストエディタ で編集できます。

<img src="./../images/ios/mediation_applovin_sdk_key_plist.png" height="120"/>

## サポートできる広告フォーマット

### 広告フォーマット
|ネットワーク |バナー |インタースティシャル |動画リワード |ネイティブ |
|:--------:|:----:|:---------------:|:--------:|:-------:|
|AppLovin  |◯     | ◯               | ◯        |        |

### バナーサイズ
|ネットワーク |320×50  |300×250   |320×100  |468×60  |728×90  |スマート    |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|AppLovin  |◯       |         |         |        |        |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#AppLovin) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Applovin の広告枠を設置する前に、Applovin の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Zone ID&emsp;&emsp;**※Zone ID はオプションです**

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Applovin を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Applovin 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Applovin 広告を追加してください。

<img src="./../images/ios/mediation_applovin_add_lineitem.png" width="600" />

## バージョン情報
### 6.12.8
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.12.8.1 | 2020/6/27 | AppLovin SDK 6.12.8 に対応：バグの修正とパフォーマンスの向上<br><br>AdLimeAppLovinGlobalConfig、AdLimeAppLovinNativeConfig：muted 属性を削除します。AdLimeNativeAd  などのオブジェクトにおける setMuted: メソッドによって動画広告の音をミュート設定することが可能です。|

### 6.11.4
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.11.4.1 | 2020/3/2  | 広告表示領域外でネイティブ広告は再生されるバグを修正|
| 6.11.4.0 | 2020/2/24 | - AppLovin SDK 6.11.4 に対応<br>- AdLimeMediation_AppLovin_Resources.bundleを追加します<br>- [NetworkConfig 設置](./mediation/config/networkconfig_applovin.md)を追加 |

### 6.11.3
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.11.3.0 | 2020/2/12 | AppLovin SDK 6.11.3 に対応|

### 6.11.0
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.11.0.1 | 2020/2/5  | - AppLovin SDK 6.11.0 に対応<br>- デバッグモードをサポート。[初期化](./init.md)を参考してください。|

### 6.9.4
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.9.4.0  | 2019/10/10| AppLovin SDK 6.9.4 に対応|

### 6.8.0
| バージョン | 日付       | 更新内容                          |
|----------|-----------|----------------------------------|
| 6.8.0.1  | 2019/8/6  | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
| 6.8.0.0  | 2019/6/30 | AppLovin SDK 6.8.0 に対応|