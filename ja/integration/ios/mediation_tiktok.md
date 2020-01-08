# Tiktok
- [Tiktok Webサイト](https://ad.oceanengine.com/union/media/login/?from=i18n)
- [Tiktok 開発者ガイド](https://ad.oceanengine.com/union/media/union/download)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Tiktok 広告ネットワークを使用するためには、 Tiktok SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_TikTok'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.5.1.2.zip)
- BUAdSDK.bundle
- [AdLimeMediation_TikTok.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_TikTok/2.5.1.2.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.5.1.2.zip)
- BUAdSDK.bundle

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Tiktok"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Tiktok > AdLimeMediation_TikTok.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- StoreKit.framework
- MobileCoreServices.framework
- WebKit.framework
- MediaPlayer.framework
- CoreMedia.framework
- AVFoundation.framework
- CoreTelephony.framework
- SystemConfiguration.framework
- AdSupport.framework
- CoreMotion.framework
- libresolv.9.tbd
- libc++.tbd
- libz.tbd

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー   |インタースティシャル        |動画リワード |ネイティブ |
|:-----:|:----:|:----------:|:------:|:----:|
|Tiktok |◯     | ◯          |◯       |◯     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Tiktok   |        |◯         |◯        |        |◯       |         |

## 広告枠の設置
AdLime を使って Tiktok の広告枠を配置する前に、 Tiktok の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID
- Code ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Tiktok を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Tiktok 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Tiktok 広告を追加してください。

**Tiktok にはネイティブが2種類があります，ネイティブ広告枠を追加する場合に Native Mode Mode を入力してください**
| Native Mode        | 値   | 説明        |
|:-------------------|:--------|:-----------|
|Native Banner       |0        |ネイティブ　バナー   |
|Express Banner      |1        |エクスプレス　バナー  |
|Native Interstitial |1        |ネイティブ　インタースティシャル |

**Tiktok にはインタースティシャルが2種類があります，インタースティシャルを追加する場合に Interstitial Mode を入力してください**
| Interstitial Mode     | 値     | 説明       |
|:----------------------|:--------|:-----------|
|Interstitial           |0        |インタースティシャル |
|FullScreenVideo        |1        |フルスクリーン      |

**Tiktok においてフルスクリーンと動画リワードは縦・横画面があります。設定する場合に、 Orientation を指定してください**
| Orientation     | 値 | 説明        |
|:----------------|:--------|:-----------|
|Vertical         |1        |縦        |
|Horizontal       |2        |横         |

## バージョン情報

### リリースバージョン
| Tiktok　バージョン  | アダプタ　バージョン |
|:----------------- |:----------------|
| 2.5.1.2            | 2.5.1.2.0        |
| 2.4.6.3            | 2.4.6.3.1        |
| 2.1.0.1            | 2.1.0.1.5        |

### バージョン履歴
| バージョン        | 日付       | 更新内容                              |
|-----------------|------------|----------------------------------|
| 2.5.1.2.0       | 2019-11-7   | Tiktok Ads SDK 2.5.1.2 に対応|
| 2.4.6.3.1       | 2019-10-10  | Tiktok Ads SDK 2.4.6.3 に対応|
| 2.1.0.1.5       | 2019-8-6    | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
| 2.1.0.1.2       | 2019-7-15   | 動画リワード広告のイベント最適化             |
| 2.1.0.1.1       | 2019-7-8    | 動画リワード広告の初期化できない問題に対応 |
| 2.1.0.1.0       | 2019-7-5    | Tiktok Ads SDK 2.1.0.1 に対応|
