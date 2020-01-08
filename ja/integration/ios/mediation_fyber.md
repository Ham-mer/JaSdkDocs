# Fyber ドキュメント
- [Fyber Webサイト](https://www.fyber.com/)
- [Fyber 開発者ガイド](https://marketplace-supply.fyber.com/docs/new-vamp-ios)

## 前提条件
- ターゲットバージョンを iOS 8.0 以上に設定していること

## SDK の導入
AdLime SDK で Fyber を使用するためには、Fyber SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Fyber'
```
use_frameworks!を使う必要がある

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [IASDKCore.framework](http://inneractive-assets.s3.amazonaws.com/sdk/files/InneractiveAdSDK-iOS-v7.5.0.zip)
- IASDKResources.bundle
- IASDKMRAID.framework
- IASDKVideo.framework
- [AdLimeMediation_Fyber.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Fyber/7.5.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [IASDKCore.framework](http://inneractive-assets.s3.amazonaws.com/sdk/files/InneractiveAdSDK-iOS-v7.5.0.zip)
- IASDKResources.bundle
- IASDKMRAID.framework
- IASDKVideo.framework

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Fyber"
```

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
carthage update
```

実行が完了したら、CarthageフォルダーのAdLimeMediation_FyberにあるAdLimeMediation_Fyber.frameworkをプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- libxml2.2.tbd

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|リワード動画|ネイティブ|
|:--------:|:----:|:----------:|:------:|:----:|
|Fyber    | ◯    | ◯           | ◯       |     |

### バナーサイズ
|ネットワーク|320*50  |300*250   |320*100  |468*60  |728*90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Fyber   |   ◯    |◯         |◯        |   ◯    |◯       |   ◯     |

## 広告枠の設置

AdLime を使って Fyber の広告枠を設置する前に、Fyber の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID
- Spot ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Fyber を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Fyber を表示する広告枠で、「広告のソース追加」をクリックし、Fyber を追加してください。

## バージョン情報

### リリースバージョン
| Fyber バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 7.5.0            | 7.5.0.0         |
| 7.4.1            | 7.4.1.0         |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 7.5.0.0         | 2019-12-18 | 1、Fyber 7.5.0  に対応             |
| 7.4.1.0         | 2019-10-21 | 1、Fyber 7.4.1  に対応             |