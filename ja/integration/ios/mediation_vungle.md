# Vungle ドキュメント
- [Vungle Webサイト](https://vungle.com)
- [Vungle 開発者ガイド](https://support.vungle.com/hc/en-us/articles/360002925791--Get-Started-with-Vungle-iOS-SDK-v-6#add-the-vunglesdk-framework-to-your-project-0-1)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDK の導入
AdLime SDK で Vungle を使用するためには、Vungle SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Vungle'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [VungleSDK.framework](hhttps://cdn-lb.vungle.com/sdks/ios/vungle645.zip)
- [AdLimeMediation_Vungle.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Vungle/6.4.5.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [VungleSDK.framework](hhttps://cdn-lb.vungle.com/sdks/ios/vungle645.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Vungle"
```

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Vungle > AdLimeMediation_Vungle.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- Support.framework
- AudioToolbox.framework
- AVFoundation.framework
- CFNetwork.framework
- CoreGraphics.framework
- CoreMedia.framework
- libz.dylib or libz.tbd
- MediaPlayer.framework
- QuartzCore.framework
- StoreKit.framework
- SystemConfiguration.framework
- CoreFoundation.framework (optional)
- Foundation.framework (optional)
- StoreKit.framework (optional)

## NetworkConfig の設定
@import AdLimeMediation_Vungle;

### ネイティブ
- AdLimeVungleInFeedConfig<br>
NetworkConfigによってネイティブ広告のフレームを設定します。デフォルト値：300*250
    ```objectivec
    AdLimeVungleInFeedConfig *vungleInFeedConfig = [[AdLimeVungleInFeedConfig alloc] init];
    [vungleInFeedConfig setFrame:CGRectMake(0, 0, 300, 250)];
    ```

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|リワード動画|ネイティブ|
|:--------------:|:----:|:----------:|:------:|:----:|
|Vungle        | ◯    | ◯           |  ◯     | ◯     |

### バナーサイズ
|ネットワーク|320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Vungle   |        |◯         |       |        |        |         |

## 広告枠の設置

AdLime を使って Vungle の広告枠を設置する前に、Vungle の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- APP ID
- Placement Reference ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Vungle を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Vungle を表示する広告枠で、「広告のソース追加」をクリックし、Vungle を追加してください。

## バージョン情報

### リリースバージョン
| Vungle バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 6.4.5            | 6.4.5.1         |
| 6.3.2            | 6.3.2.0         |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 6.4.5.1         | 2019-11-7  | - MRECタイプのバナー広告が利用可能になります<br>- In-Feed広告がネイティブ広告として表示される場合、フレームを設定できるようになります。       |
| 6.4.5.0         | 2019-10-10  | Vungle SDK v6.4.5 に対応       |
| 6.3.2.0         | 2019-9-20   | Vungle SDK v6.3.2 に対応      |