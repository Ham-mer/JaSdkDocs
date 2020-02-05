# DU Ad Platform ドキュメント
- [DU Ad Platform Webサイト](http://ad.duapps.com)
- [DU Ad Platform 開発者ガイド](http://e.duapps.com/download/sdk/)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDKの導入
AdLime SDK で DU Ad Platform Audience Network を使用するために、 DU Ad Platform Audience Network SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_DUADPlatform'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AdLimeMediation_DUAdPlatform.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_DUAdPlatform/1.1.4.2.zip)
- DUModuleSDK.framework
- DUMRAID.bundle

### Carthage
プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_DUAdPlatform"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_DUAdPlatform > AdLimeMediation_DUAdPlatform.framework, DUModuleSDK.framework, DUMRAID.bundle をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク     |バナー|インタースティシャル|動画リワード|ネイティブ|
|:-------------:|:----:|:--------------:|:--------:|:------:|
|DU Ad Platform |◯     | ◯              |          |◯       |

### バナーサイズ
|ネットワーク     |320 × 50|300 × 250 |320 × 100 |468 × 60|728 × 90|スマート   |
|:-------------:|:------:|:--------:|:--------:|:------:|:------:|:-------:|
|DU Ad Platform |◯       |         |           |        |        |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#DU-Ad-Platform) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って DU Ad Platform Audience Network の広告枠を配置する前に、DU Ad Platform Audience Network の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Placement ID
- App ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 DU Ad Platform を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 DU Ad Platform Audience Network 広告を表示する広告枠で、「広告のソース追加」をクリックし、 DU Ad Platform Audience Network 広告を追加してください。

## バージョン情報

### リリースバージョン
| DU Ad Platform バージョン | アダプタ バージョン |
|:------------------------|:----------------|
| 1.1.4                   | 1.1.4.2         |

### バージョン履歴
| バージョン | 日付       | 更新内容                              |
|----------|------------|-----------------------------------|
| 1.1.4.2  | 2020/2/5   | 調整モード、テストモードの設定をサポートします，[初期化](./init.md)を参考してください|
| 1.1.4.0  | 2019/10/29 | DU Ad Platform SDK 1.1.4 に対応|