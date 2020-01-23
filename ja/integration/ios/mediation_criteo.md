# Criteo ドキュメント
- [Criteo Webサイト](https://www.criteo.com)
- [Criteo 開発者ガイド](https://publisherdocs.criteotilt.com/sdk-ios/3.0/inhouseauction/)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDKの導入
AdLime SDK で Criteo Audience Network を使用するために、 Criteo Audience Network SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Criteo'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [CriteoPublisherSdk.framework](https://pubsdk-bin.criteo.com/publishersdk/ios/CriteoPublisherSdk_iOS_v3.2.0.Release.zip)
- [AdLimeMediation_Criteo.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Criteo/3.2.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [CriteoPublisherSdk.framework](https://pubsdk-bin.criteo.com/publishersdk/ios/CriteoPublisherSdk_iOS_v3.2.0.Release.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Criteo"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後に、Carthage フォルダの AdLimeMediation_Criteo > AdLimeMediation_Criteo.framework をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク  |バナー|インタースティシャル|動画リワード|ネイティブ|
|:----------:|:---:|:--------------:|:---------:|:----:|
|Criteo      |◯    | ◯              |           |     |

### バナーサイズ
|ネットワーク|320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート   |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Criteo    |◯       |  ◯       |   ◯     |  ◯     |    ◯   | ◯       |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Criteo) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Criteo の広告枠を配置する前に、Criteo の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Publish ID
- Unit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Criteo を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Criteo 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Criteo 広告を追加してください。

## バージョン情報

### リリースバージョン
| Criteo バージョン | アダプタ バージョン |
|:----------------|:-----------------|
| 3.2.0           | 3.2.0.0         |

### バージョン履歴
| バージョン | 日付       | 更新内容                              |
|----------|------------|-----------------------------------|
| 3.2.0.0 | 2019/10/17  | Criteo SDK 3.2.0 に対応|