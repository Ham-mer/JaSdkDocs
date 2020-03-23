# Nend
- [Nend Webサイト](https://nend.net/)
- [Nend 開発者ガイド](https://github.com/fan-ADN/nendSDK-iOS)

## 前提条件
- ターゲットバージョン iOS 8.1 以上

## SDKを導入する
AdLime SDK で Nend を使用するためには、最初のステップは Nend SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods
CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Nend'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [NendAd.embeddedframework](https://github.com/fan-ADN/nendSDK-iOS-pub/releases/download/5.4.1/nendSDK_iOS.zip)
- [AdLimeMediation_Nend.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Nend/5.4.1.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [NendAd.embeddedframework](https://github.com/fan-ADN/nendSDK-iOS-pub/releases/download/5.4.1/nendSDK_iOS.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Nend"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Nend > AdLimeMediation_Nend.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
以下のフレームワークを追加する必要があります。

- AdSupport.framework
- Security.framework
- ImageIO.framework
- AVFoundation.framework
- CoreMedia.framework
- SystemConfiguration.framework
- WebKit.framework

以下のフレームワークはオプションです。 広告の詳細情報を取得可能です。
- CoreLocation.framework
- CoreMotion.framework
- CoreTelephony.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:-----:|:----:|:----------:|:------:|:----:|
|Nend   |◯     | ◯          |◯       |◯     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Nend     |◯       |◯         |◯        |        |◯       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Nend) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 注意が必要な事項
ネイティブ広告では静止画と動画があります。動画広告を展示する時に、NativeAdLayoutには必ずMediaViewを設置します。そうしないと、展示とされないです。

## バージョン情報
### 5.4.1
| バージョン    | 日付        | 更新内容                          |
|-------------|------------|----------------------------------|
| 5.4.1.0     | 2020/3/11  | - Nend SDK 5.4.1 に対応<br>- ある場合にネイティブ広告は展示とクリックのコールバックがない問題を解決しました|

### 5.4.0
| バージョン    | 日付        | 更新内容                          |
|-------------|------------|----------------------------------|
| 5.4.0.1     | 2020/2/20  | - Nend SDK 5.4.0 に対応<br>- バナー広告をスワイプされるとクリックと認める問題を解決します |

### 5.3.0
| バージョン    | 日付        | 更新内容                          |
|-------------|------------|----------------------------------|
| 5.3.0.1     | 2020/2/5   | 調整モードをサポートします，[初期化](./init.md)を参考してください |
| 5.3.0.0     | 2019/10/10 | Nend SDK 5.3.0 に対応 |

### 5.1.1
| バージョン    | 日付        | 更新内容                          |
|-------------|------------|----------------------------------|
| 5.1.1.4     | 2019/8/6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応 |
| 5.1.1.2     | 2019/7/6   | クラスが重複する問題を改修 |
| 5.1.1.1     | 2019/7/2   | インターステーシャル広告イベントの最適化 |
| 5.1.1.0     | 2019/6/30  | Nend SDK 5.1.1 に対応 |