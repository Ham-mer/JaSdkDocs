# AdColony ドキュメント
- [AdColony Webサイト](https://www.adcolony.com)
- [AdColony 開発者ガイド](https://github.com/AdColony/AdColony-iOS-SDK-3/wiki/Project-Setup)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で AdColony を使用するためには、AdColony SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_AdColony'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AdColony.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/AdColony/AdColony_4.1.2.zip)
- [AdLimeMediation_AdColony.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_AdColony/4.1.2.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AdColony.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/AdColony/AdColony_4.1.2.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_AdColony"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_AdColony > AdLimeMediation_AdColony.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- libz.1.2.5.tbd
- AdSupport.framework
- AudioToolbox.framework
- AVFoundation.framework
- CoreMedia.framework
- CoreTelephony.framework
- JavaScriptCore.framework
- MessageUI.framework
- MobileCoreServices.framework
- Social.framework (设置为Optional)
- StoreKit.framework (设置为Optional)
- SystemConfiguration.framework
- WatchConnectivity.framework (设置为Optional)
- WebKit.framework (设置为Optional)

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|リワード動画|ネイティブ|
|:--------:|:----:|:--------------:|:--------:|:----:|
|AdColony  | ◯    | ◯              |   ◯      |      |


## 広告枠の設置

AdLime を使って AdColony の広告枠を設置する前に、AdColony の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID
- Zone ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、AdColony を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、AdColony を表示する広告枠で、「広告のソース追加」をクリックし、AdColony を追加してください。

## バージョン情報

### リリースバージョン
| AdColony バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 4.1.2            | 4.1.2.1         |
| 4.1.1            | 4.1.1.0         |
| 3.3.8.1          | 3.3.8.1.1       |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 4.1.2.1         | 2019-11-18 | バナー広告をサポートする        |
| 4.1.2.0         | 2019-11-7  | AdColony 4.1.2  に対応        |
| 4.1.1.0         | 2019-10-10 | AdColony 4.1.1  に対応        |
| 3.3.8.1.1       | 2019-9-19  | AdColony 3.3.8.1  に対応        |