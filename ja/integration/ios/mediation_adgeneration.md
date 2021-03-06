# AdGeneration ドキュメント

- [AdGeneration Webサイト](https://supership.jp/business/adgeneration/)
- [AdGeneration 開発者ガイド](https://github.com/AdGeneration/SDK/wiki)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

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
- [ADG.framework](https://github.com/AdGeneration/ADG-iOS-SDK/releases/download/2.18.0/ADG.framework.zip)
- [AdLimeMediation_AdGeneration.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_AdGeneration/2.18.0.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [ADG.framework](https://github.com/AdGeneration/ADG-iOS-SDK/releases/download/2.18.0/ADG.framework.zip)

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

## 注意事項
AdGenerationのバナー広告を利用する時、UIViewControllerのdeallocメソッドでAdLimeBannerViewのdestroyメソッドを呼び出してください。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|動画リワード|ネイティブ|
|:------------:|:----:|:----------:|:-------:|:----:|
|AdGeneration  |◯     | ◯          |         |◯     |

### バナーサイズ
|ネットワーク  |320×50  |300×250   |320×100  |468×60  |728×90  |SMART    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|AdGeneration    |◯       |◯         |◯        |◯       |◯       |◯        |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#AdGeneration) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置

AdLime を使って AdGeneration の広告枠を設置する前に、AdGeneration の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Location ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、AdGeneration を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、AdGeneration を表示する広告枠で、「広告のソース追加」をクリックし、AdGeneration を追加してください。

## バージョン情報
### 2.18.0
| バージョン        | 日付       | 更新内容                       |
|-----------------|------------|------------------------------|
| 2.18.0.1        | 2020/6/27  | AdGenertaion 2.18.0 に対応 |

### 2.16.4
| バージョン        | 日付       | 更新内容                       |
|-----------------|------------|------------------------------|
| 2.16.4.3        | 2020/2/5   | テストモードをサポート。[初期化](./init.md)を参考してください |
| 2.16.4.2        | 2019/11/27 | ネイティブ広告のボタンをクリックされないバグを修正2 |
| 2.16.4.1        | 2019/11/21 | ネイティブ広告のボタンをクリックされないバグを修正 |
| 2.16.4.0        | 2019/11/7  | AdGenertaion 2.16.4 に対応 |

### 2.15.2
| バージョン        | 日付       | 更新内容                       |
|-----------------|------------|------------------------------|
| 2.15.2.0        | 2019/10/10 | AdGenertaion 2.15.2 に対応 |