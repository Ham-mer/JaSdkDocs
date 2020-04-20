# i-mobile
- [i-mobile Webサイト](https://sppartner.i-mobile.co.jp/login.aspx)
- [i-mobile 開発者ガイド](https://sppartner.i-mobile.co.jp/webdoc/index.html)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で i-mobile 広告ネットワークを使用するためには、 i-mobile SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Imobile'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [ImobileSdkAds.framework](https://sppartner.i-mobile.co.jp/downloads/sdk/imobile_for_SP_app_iOS_SDK_2.0.31.zip)
- [AdLimeMediation_Imobile.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Imobile/2.0.31.3.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [ImobileSdkAds.framework](https://sppartner.i-mobile.co.jp/downloads/sdk/imobile_for_SP_app_iOS_SDK_2.0.31.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Imobile"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Imobile > AdLimeMediation_Imobile.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- AdSupport.framework
- SystemConfiguraion.framework
- CoreLocation.framework
- WebKit.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー |インタースティシャル |動画リワード|ネイティブ |
|:--------:|:----:|:----------------:|:--------:|:-------:|
|i-mobile  |◯     | ◯                |          |◯        |

### バナーサイズ
|ネットワーク|320×50|300×250 |320×100|468×60|728×90|スマート  |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|i-mobile  |  ◯     |◯         |◯        |        |       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#i-mobile) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って i-mobile の広告枠を配置する前に、 i-mobile の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Publish ID
- Media ID
- Spot ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 i-mobile を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 i-mobile 広告を表示する広告枠で、「広告のソース追加」をクリックし、 i-mobile 広告を追加してください。

**i-mobile にはネイティブが2種類があります，ネイティブを追加する場合に Native Mode を入力してください**
| Native Mode     | 値   | 説明       |
|:----------------|:---- |:-----------|
|Normal Native    |0     |ネイティブ |
|InLine FullScreen|1     |インライン 全画面  |

## バージョン情報

### リリースバージョン
| i-mobile　バージョン| アダプタ　バージョン |
|:----------------- |:------------------|
| 2.0.31            | 2.0.31.3          |

### バージョン履歴
| バージョン        | 日付        | 更新内容                           |
|-----------------|-------------|----------------------------------|
| 2.0.31.3        | 2020/3/4    | ある場合にロードされるバナー広告とネイティブ広告は展示されない問題を解決します|
| 2.0.31.2        | 2020/2/28   | ネイティブ広告は反応ボタンを展示しない問題を解決します|
| 2.0.31.1        | 2020/2/5    | テストモードをサポートします，[初期化](./init.md)を参考してください|
| 2.0.31.0        | 2020/01.08  | 2.0.31 に対応|