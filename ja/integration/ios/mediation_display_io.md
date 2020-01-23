# Display.IO ドキュメント
- [Display.IO Webサイト](https://developers.display.io)
- [Display.IO 開発者ガイド](https://support.display.io/hc/en-us/articles/360022373333-Installing-the-SDK)

## 前提条件
- ターゲットバージョン iOS 10.0 以上

## SDKの導入
AdLime SDK で Display.IO Audience Network を使用するために、 Display.IO Audience Network SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods
現時点ではサポートされていません。

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [DIOSDK.framework](https://support.display.io/hc/en-us/article_attachments/360004458000/display.io.iOS.SDK-2.8.0.zip)
- [AdLimeMediation_DisplayIO.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_DisplayIO/2.8.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [DIOSDK.framework](https://support.display.io/hc/en-us/article_attachments/360004458000/display.io.iOS.SDK-2.8.0.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_DisplayIO"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_DisplayIO > AdLimeMediation_DisplayIO.framework をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク  |バナー|インタースティシャル|動画リワード|ネイティブ|
|:----------:|:---:|:--------------:|:---------:|:----:|
|Display.IO  |◯    | ◯              |  ◯        |     |

### バナーサイズ
|ネットワーク|320 × 50 |300 × 250 |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Display.IO|        |◯         |         |        |        |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Display.IO) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Display.IO の広告枠を配置する前に、Display.IO の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID
- Placement ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Display.IO を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Display.IO 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Display.IO 広告を追加してください。

## バージョン情報

### リリースバージョン
| Display.IO バージョン | アダプタ バージョン |
|:--------------------|:-----------------|
| 2.8.0              | 2.8.0.0         |
| 2.6.1              | 2.6.1.0         |

### バージョン履歴
| バージョン | 日付       | 更新内容                              |
|----------|------------|-----------------------------------|
| 2.8.0.0 | 2019-11-26  | Display.IO SDK 2.8.0 に対応 <br> 動画リワード広告をサポートする|
| 2.6.1.0 | 2019-10-10  | Display.IO SDK 2.6.1 に対応|
