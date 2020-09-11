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
- iOS SDK（20200625）
    - [AdLimeMediation_Five.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Five/20200625.0.zip)
    - [FiveAd.framework](https://s3-ap-northeast-1.amazonaws.com/fivecdm-public/release-sdk/ios/20200625/FiveAd.framework-20200625.zip)

- iOS 14 Beta SDK（20200824）
    - [AdLimeMediation_Five.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Five/20200824.0.zip)
    - [FiveAd.framework](https://s3-ap-northeast-1.amazonaws.com/fivecdm-public/release-sdk/ios/20200824/FiveAd.framework-20200824.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- iOS SDK（20200625）
    - [FiveAd.framework](https://s3-ap-northeast-1.amazonaws.com/fivecdm-public/release-sdk/ios/20200625/FiveAd.framework-20200625.zip)

- iOS 14 Beta SDK（20200824）
    - [FiveAd.framework](https://s3-ap-northeast-1.amazonaws.com/fivecdm-public/release-sdk/ios/20200824/FiveAd.framework-20200824.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Five"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Five > AdLimeMediation_Five.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- AdSupport.framework
- AVFoundation.framework
- CoreMedia.framework
- CoreTelephony.framework
- SystemConfiguration.framework
- AudioToolbox.framework
- WebKit.framework
- StoreKit.framework

iOS 14 Beta SDK（20200824）
- AppTrackingTransparency.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:--------:|:----:|:--------------:|:------:|:----:|
|Five      |◯     | ◯          |◯       |     |

### バナーサイズ
|ネットワーク  |320×50  |300×250   |320×100  |468×60  |728×90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Five    |◯       |◯         |    ◯     |        |       |         |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#Five) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## iOS 14 Beta SDK（20200824）Info.plist の更新

iOS 14 以降ではデバイスの広告識別子( IDFA )の取得が厳しく制限されるため、広告の効果測定が困難になります。Apple は代替の広告効果測定ツールとして、SKAdNetwork を提供します。SKAdNetwork により、広告のコンバージョンの測定が可能になります。このツールを設定することで、広告収益が増加する可能性があります。

FIVE の広告ネットワーク事業者を登録するには Info.plist を開いて編集します。

```objectivec
<key>SKAdNetworkItems</key>
<array>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>VUTU7AKEUR.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>EH6M2BH4ZR.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>4mn522wn87.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>578prtvx9j.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>9T245VHMPL.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>22mmun2rn5.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>V72QYCH5UU.skadnetwork</string>
    </dict>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>7UG5ZH24HU.skadnetwork</string>
    </dict>
</array>
```

## バージョン情報
### 20200824（Beta for iOS 14）
| バージョン | 日付        | 更新情報                           |
|----------|-------------|----------------------------------|
| 20200824.0 | 2020/8/28 | - Five SDK 20200824（β版） に対応：iOS 14 beta に追加された AppTrackingTransparency と SKAdNetwork に対応。**テストには Xcode 12 Betaが必要であり、アプリは AppStore でのリリースができません**|

### 20200625
| バージョン | 日付        | 更新情報                           |
|----------|-------------|----------------------------------|
| 20200625.0| 2020/6/30  | - Five SDK 20200625 に対応：動画の再生と広告の表示を改善します。また、インタースティシャル・動画リワードがUIWindowSceneをサポートします|

### 20191223
| バージョン | 日付        | 更新情報                           |
|----------|-------------|----------------------------------|
| 20191223.0| 2020/2/10  | - Five SDK 20191223 に対応<br>- VideoToolBox.framework および CoreAudio.framework への依存性がなくなりました  |

### 20191016
| バージョン | 日付        | 更新情報                           |
|----------|-------------|----------------------------------|
| 20191016.2| 2020/2/5   | テストモードをサポート。[初期化](./init.md)を参考してください |
| 20191016.1| 2019/11/27 | インタースティシャ広告の表示バグの修正 |
| 20191016.0| 2019/10/30 | Five SDK 20191016 に対応     |