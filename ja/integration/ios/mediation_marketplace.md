# AdLimeMarketplace ドキュメント

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Marketplace を使用するためには、Marketplace SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Marketplace'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AdLimeMarketplace.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMarketplace/1.1.5.zip)
- AdLimeMarketplaceTemplateAd.framework
- AdLimeMarketplace.bundle
- [AdLimeMediation_Marketplace.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Marketplace/1.1.5.2.zip)

### Carthage
プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMarketplace"
github "Ham-mer/AdLimeMediation_Marketplace"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMarketplace, AdLimeMediation_Marketplace > framework をプロジェクトにインポートします。

## 広告フォーマット

### 利用可能な広告フォーマット
|ネットワーク |バナー |インタラクション |動画リワード |ネイティブ |
|:---------:|:----:|:------------:|:---------:|:--------:|
| AdLimeMarketplace | ◯ |         |           |          |

### バナーサイズ
|ネットワーク | 320×50 | 300×250 | 320×100 | 468×60 | 728×90 |
|:---------:|:------:|:-------:|:-------:|:------:|:------:|
| AdLimeMarketplace | ◯ | ◯    |         |        |        |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#AdLimeMarketplace) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## バージョン情報
### 1.1.5
| バージョン   | 日付       | 更新内容                           |
|------------|------------|----------------------------------|
| 1.1.5.2    | 2020/8/2   | テストモードにおいて広告がロードされないというエラーを修正します|
| 1.1.5.1    | 2020/7/20  | AdLimeMarketplace SDK 1.1.5 に対応|