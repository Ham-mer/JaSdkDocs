# Flurry ドキュメント
- [Flurry Webサイト](https://www.flurry.com/)
- [Flurry 開発者ガイド](https://developer.yahoo.com/flurry/docs/integrateflurry/ios/)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Flurry を使用するためには、Flurry SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Flurry'
```
また "use_frameworks!" も追加します。

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [libFlurry_10.0.2.a](https://github.com/flurry/Flurry-iOS-SDK)
- libFlurryAds_1.3.0.a
- [AdLimeMediation_Flurry.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Flurry/10.0.2.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [libFlurry_10.0.2.a](https://github.com/flurry/Flurry-iOS-SDK)
- libFlurryAds_1.3.0.a

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Flurry"
```

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Flurry > AdLimeMediation_Flurry.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- Security.framework
- SystemConfiguration.framework
- CoreLocation.framework
- AdSupport.framework 
- AVFoundation.framework 
- CoreGraphics.framework 
- CoreMedia.framework 
- Foundation.framework 
- MediaPlayer.framework 
- StoreKit.framework 
- UIKit.framework 
- WebKit.framework 
- CoreTelephony.framework 
- libz.tbd

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|動画リワード|ネイティブ|
|:--------:|:----:|:----------:|:------:|:----:|
|Flurry    | ◯    | ◯          |        | ◯    |

### バナーサイズ
|ネットワーク|320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Flurry   |   ◯    |◯         |◯        |   ◯    |◯       |   ◯     |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Flurry) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。


## 広告枠の設置

AdLime を使って Flurry の広告枠を設置する前に、Flurry の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Api Key
- AdUnit Name

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Flurry を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Flurry を表示する広告枠で、「広告のソース追加」をクリックし、Flurry を追加してください。

## バージョン情報

### リリースバージョン
| Flurry バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 10.0.2           | 10.0.2.1        |
| 10.0.0           | 10.0.0.1        |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 10.0.2.1        | 2019-12-20 | ネイティブ広告のイベント最適化        |
| 10.0.2.0        | 2019-10-10 | Flurry 10.0.2  に対応          |
| 10.0.0.1        | 2019-9-19  | Flurry 10.0.0  に対応          |