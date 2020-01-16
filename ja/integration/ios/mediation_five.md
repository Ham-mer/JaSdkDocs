# Five
- [Five Webサイト](hhttps://www.five-corp.com/)
- [Five 開発者ガイド](https://partner.fivecdm.com/help/integration)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDKの導入

AdLime SDK で Five を使用するために、 Five SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Five'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [AdLimeMediation_Five.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Five/20191016.1.zip)
- FiveAd.framework

### Carthage
プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Five"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Five > AdLimeMediation_Five.framework,FiveAd.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- AdSupport.framework
- AVFoundation.framework
- CoreMedia.framework
- CoreTelephony.framework
- SystemConfiguration.framework
- VideoToolbox.framework
- AudioToolbox.framework
- CoreAudio.framework
- WebKit.framework
- StoreKit.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:--------:|:----:|:--------------:|:------:|:----:|
|Five      |◯     | ◯          |◯       |     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Five    |◯       |◯         |    ◯     |        |       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Five) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置
AdLime を使って Mobup の広告枠を配置する前に、 Five の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID
- Slot ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Five を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Five 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Five 広告を追加してください。

## バージョン情報

### リリースバージョン
| Five バージョン    | アダプタ バージョン |
|:-----------------|:----------------|
|520191016         |20191016.1        |

### バージョン履歴
| バージョン | 日付       | 更新内容                           |
|----------|------------|----------------------------------|
| 20191016.1| 2019-11-27 | インタースティシャ広告の展示バグの修正 | 
| 20191016.0| 2019-10-30 | Five SDK 20191016 に対応     | 
