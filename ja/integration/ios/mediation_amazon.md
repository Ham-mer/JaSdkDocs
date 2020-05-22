# Amazon ドキュメント
- [Amazon Webサイト](https://developer.amazon.com/zh/)
- [Amazon 開発者ガイド](https://developer.amazon.com/apps-and-games/mobile-ads)

## 前提条件
- ターゲットバージョン iOS 10.0 以上

## SDK の導入
AdLime SDK で Amazon 広告ネットワークを使用するために、Amazon SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Amazon'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AmazonAd.framework](https://app-craft-internal.ams3.digitaloceanspaces.com/Frameworks/AmazonAdSDK/AmazonMobileAds-iOS-v2.2.17.0.zip)
- [AdLimeMediation_Amazon.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Amazon/2.2.17.3.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AmazonAd.framework](https://app-craft-internal.ams3.digitaloceanspaces.com/Frameworks/AmazonAdSDK/AmazonMobileAds-iOS-v2.2.17.0.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Amazon"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Amazon > AdLimeMediation_Amazon.frameworkをプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:-----:|:----:|:----------:|:------:|:----:|
|Amazon |◯     | ◯          |        |      |

### バナーサイズ
|ネットワーク  |320×50  |300×250   |320×100  |468×60  |728×90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Amazon   |◯       |◯         |         |        |◯       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Amazon) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Amazon の広告を設置する前に、Amazon の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Application Key

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Amazon を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Amazon 広告を表示する広告枠で、「広告のソース追加」をクリックし、Amazon 広告を追加してください。

## バージョン情報

### リリースバージョン
| Amazon バージョン   | アダプタ バージョン |
|:-----------------|:----------------|
| 2.2.17           | 2.2.17.3        |

### バージョン履歴
| バージョン         | 日付       | 更新内容                             |
|-----------------|------------|----------------------------------|
| 2.2.17.3        | 2020/2/5   | テストモードをサポート。[初期化](./init.md)を参考してください|
| 2.2.17.1        | 2019/8/3   | 不要なヘッダーファイルの削除|
| 2.2.17.0        | 2019/6/30  | Amazon SDK 2.2.17 に対応|
