# AdGeneration ドキュメント

- [AdGeneration Webサイト](https://supership.jp/business/adgeneration/)
- [AdGeneration 開発者ガイド](https://developers.google.cn/AdGeneration/ios/quick-start)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で AdGeneration を使用するためには、AdGeneration SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_AdGeneration'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [ADG.framework](https://github.com/AdGeneration/ADG-iOS-SDK/releases/download/2.16.4/ADG.framework.zip)
- [AdLimeMediation_AdGeneration.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_AdGeneration/2.16.4.2.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [ADG.framework](https://github.com/AdGeneration/ADG-iOS-SDK/releases/download/2.16.4/ADG.framework.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_AdGeneration"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_AdGeneration > AdLimeMediation_AdGeneration.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- AdSupport.framework (Optional)
- AVFoundation.framework
- CoreLocation.framework
- CoreMedia.framework
- CoreTelephony.framework
- MediaPlayer.framework
- SystemConfiguration.framework
- SafariServices.framework
- WebKit.framework 


## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|リワード動画|ネイティブ|
|:------------:|:----:|:----------:|:-------:|:----:|
|AdGeneration  |Y     | Y          |         |Y     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |SMART    |
|:-------:|:------:| --------:|:-------:|:------:|:------:|:-------:|
|AdGeneration    |Y       |Y         |Y        |Y       |Y       |Y        |

## 広告枠の設置

AdLime を使って AdGeneration の広告枠を設置する前に、AdGeneration の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Location ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、AdGeneration を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、AdGeneration を表示する広告枠で、「広告のソース追加」をクリックし、AdGeneration を追加してください。

## バージョン情報

### リリースバージョン
| AdGeneration バージョン    | アダプタ バージョン |
|:-----------------|:----------------|
|2.16.4            |2.16.4.2         |
|2.15.2            |2.15.2.0         |

### バージョン履歴
| バージョン        | 日付       | 更新内容                       |
|-----------------|------------|------------------------------|
| 2.16.4.2        | 2019-11-27 | ネイティブ広告のボタンをクリックされないというbugを修正完了 |
| 2.16.4.1        | 2019-11-21 | ネイティブ広告のボタンをクリックされないというbugを修正 |
| 2.16.4.0        | 2019-11-7  | AdGenertaion 2.16.4 に対応 |
| 2.15.2.0        | 2019-10-10 | AdGenertaion 2.15.2 に対応 |