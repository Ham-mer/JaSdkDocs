﻿# AdMob ドキュメント

- [AdMob Webサイト](https://apps.admob.com/v2/home)
- [AdMob 開発者ガイド](https://developers.google.cn/admob/ios/quick-start)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDK の導入
AdLime SDK で AdMob を使用するためには、AdMob SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_GoogleAds'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [Google-Mobile-Ads-SDK.framework](https://developers.google.cn/admob/ios/download)
- GoogleAppMeasurement.framework
- GoogleUtilities.framework
- nanopb.framework
- PromisesObjC.xcframework
- UserMessagingPlatform.framework
- [AdLimeMediation_GoogleAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_GoogleAds/7.64.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [Google-Mobile-Ads-SDK.framework](https://developers.google.cn/admob/ios/download)
- GoogleAppMeasurement.framework
- GoogleUtilities.framework
- nanopb.framework
- PromisesObjC.xcframework
- UserMessagingPlatform.framework

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_GoogleAds"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Admob > AdLimeMediation_Admob.framework をプロジェクトにインポートします。

## Info.plist の更新
アプリのInfo.plistファイルに：
- Admob App IDの文字列値（AdMob UIから確認できる）が含まれたGADApplicationIdentifierキーを追加してください。
- cstr6suwn9.skadnetworkのGoogle SKAdNetworkIdentifier値が含まれたSKAdNetworkItemsキーを追加してください。

Info.plist を ソースコードとして開いて編集します。
```objectivec
<key>GADApplicationIdentifier</key>
<string>YOUR AdMob APP_ID</string>
<key>SKAdNetworkItems</key>
    <array>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>cstr6suwn9.skadnetwork</string>
        </dict>
    </array>
```

もしくは、プロパティリストエディタ で編集できます。

<img src="./../images/ios/mediation_admob_info_plist.png" height="160" />

**Google Mobile Ads SDK 7.42.0 以降のバージョンでは、上記を追加する必要があります。 Info.plist ファイルに GADApplicationIdentifier キーがない場合、アプリがクラッシュする可能性があります。その際、下記のメッセージが表示されます："The Google Mobile Ads SDK was initialized incorrectly."**

## NetworkConfig 設置
AdMobをカスタマイズで設置します。[AdMob NetworkConfig](./mediation/config/networkconfig_admob.md) を参考してください。

## 広告フォーマット

### 利用可能な広告フォーマット
|ネットワーク |バナー |インタラクション |動画リワード |ネイティブ |
|:---------:|:----:|:------------:|:---------:|:--------:|
| AdMob     | ◯    | ◯            | ◯         | ◯        |

### バナーサイズ
|ネットワーク | 320×50 | 300×250 | 320×100 | 468×60 | 728×90 |
|:---------:|:------:|:-------:|:-------:|:------:|:------:|
| AdMob     | ◯      | ◯       | ◯       | ◯      | ◯      |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#AdMob) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## 広告枠の設置

AdLime を使って Admob の広告枠を設置する前に、AdMob の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App ID  
- AdUnit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、AdMob を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、AdMob を表示する広告枠で、「広告のソース追加」をクリックし、AdMob を追加してください。

## バージョン情報
### 7.64.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 7.64.0.0        |2020/8/24   | - AdMob SDK 7.64.0 に対応：<br>- iOS 14に対応して、[App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency)および [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork)をサポートします<br>- UserMessagingPlatform.frameworkを追加<br>-CocoaPodsユーザーにとって、最小デプロイメントターゲットは9.0です<br><br>- Info.plistにSKAdNetworkItems設定を追加します|

### 7.62.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 7.62.0.0        |2020/7/21   | - AdMob SDK 7.62.0 に対応<br>- バナー広告にてメモリリークが発生するバグを修正します|

### 7.58.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 7.58.0.1        |2020/4/23   | - AdMob SDK 7.58.0 に対応（Xcode 11.0以上必須） <br> - AdLimeNativeAd 等で `setMuted:` を提供する。広告の音をミュートにするかどうかを選択可能 <br>- [AdLimeSdk](./init.md)を 1.8.0 以上のバージョンまでアップデートが必要 |

### 7.56.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 7.56.0.1        |2020/3/4    | アダプティブ バナーをサポート。[AdLimeAdMobBannerConfig](./mediation/config/networkconfig_admob.md) で広告のサイズを設定できます。ドキュメントは [Adaptive Banner 紹介](https://developers.google.com/admob/ios/banner/adaptive) 参照 |

### 7.55.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
|7.55.0.1         |2020/2/14   |- AdMob SDK 7.55.0 に対応<br>- 新たな動画リワードAPIでパラレルロードをサポート |

### 7.52.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
|7.52.0.2         |2020/2/3    |画面が縦から横になると、広告のサイズは自動調整できない問題を解決します |
|7.52.0.0         |2019/11/7   |AdMob SDK 7.52.0 に対応 |

### 7.50.0
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
|7.50.0.0         |2019/10/10  |AdMob SDK 7.50.0 に対応 |

### 7.42.2
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
|7.42.2.6         |2019/8/4    |NativeAdLayout インタラクティブエリアのカスタマイズに対応 |
|7.42.2.1         |2019/7/4    |広告イベントの最適化 |
|7.42.2.0         |2019/6/30   |AdMob SDK 7.42.2 に対応 |
