# Tapjoy ドキュメント
- [Tapjoy Webサイト](https://www.tapjoy.com/)
- [Tapjoy 開発者ガイド](https://dev.tapjoy.com/sdk-integration/ios/getting-started-guide-publishers-ios/)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Tapjoy を使用するためには、Tapjoy SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Tapjoy'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [TapjoySDK.embeddedframework](https://s3.amazonaws.com/tapjoy/sdks/TapjoySDK_iOS_v12.3.4.zip)
- [AdLimeMediation_Tapjoy.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Tapjoy/12.3.4.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [TapjoySDK.embeddedframework](https://s3.amazonaws.com/tapjoy/sdks/TapjoySDK_iOS_v12.3.4.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Tapjoy"
```

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Tapjoy > AdLimeMediation_Tapjoy.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- AdSupport
- CFNetwork
- CoreGraphics
- CoreTelephony  (optional)
- Foundation
- ImageIO.framework
- libc++
- libz
- MediaPlayer
- MobileCoreServices
- PassKit     (optional)
- QuartzCore    
- Security
- StoreKit     (optional)
- SystemConfiguration
- UIKit
- WebKit

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|動画リワード|ネイティブ|
|:--------:|:---:|:--------------:|:---------:|:------:|
|Tapjoy    |     | ◯              |    ◯      |        |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Tapjoy) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。


## 広告枠の設置

AdLime を使って Tapjoy の広告枠を設置する前に、Tapjoy の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- SDK Key
- Placement Name

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Tapjoy を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Tapjoy を表示する広告枠で、「広告のソース追加」をクリックし、Tapjoy を追加してください。

## バージョン情報

### リリースバージョン
| Tapjoy バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 12.3.4           | 12.3.4.1        |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 12.3.4.1        | 2020/2/5   | デバッグモードをサポート。[初期化](./init.md)を参考してください|
| 12.3.4.0        | 2019/10/28 | Tapjoy 12.3.4  に対応             |