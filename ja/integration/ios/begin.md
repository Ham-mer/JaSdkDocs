# スタートガイド
このガイドは、AdLime SDK を使用することによって iOS アプリをマネタイズすることをご希望の開発者様を対象としています。

アプリに AdLime SDK を導入することは、広告を表示して収益を獲得するための第一歩です。 SDK を導入したら、広告フォーマット（ネイティブ広告や動画リワード広告など）を選び、該当する手順に従ってください。

## 前提条件
- Xcode 9.2 以上のバージョンを使用
- ターゲットバージョンを iOS 8.0 以上に設定
- AdLime アカウントを作成し、アプリが登録済み

## AdLime SDKを導入する
ここで二種類のSDKを提供している。その一つはAdLimeSdkというSDK、このSDKは独立な広告マネタイズアクセスを提供していて、各[mediation](./mediation.md)SDKを結合して、他のネットワークの結合を実現することができる。もう一つはAdLimeSdk_AllというSDK、このSDKはAdLimeSdkとAdMob， DFP， FaceBook，Mopub，appLovin， TikTok等ののマネタイズプラットフォームのmediation SDKをパッキングすることで、他のmediationを単独的に結合する手順を省略することができる。アプリは自分の
需要でSDKを選ぶことができる。

### AdLimeSdk
#### CocoaPods（推奨）
iOS プロジェクトに AdLime SDK を導入するための、最も簡単な方法は CocoaPods を使用することです。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeSdk'
```

コマンドラインから次のコマンドを実行してください:
```objectivec
pod install --repo-update
```

CocoaPods を初めてご利用の場合、 CocoaPods の[公式ドキュメント](https://guides.cocoapods.org/using/using-cocoapods)で Podfile の作成方法と使用方法をご確認ください。

#### 手動ダウンロード
SDK フレームワークを直接ダウンロードして解凍し、下記のフレームワークを Xcode プロジェクトに導入してください。

- [AdLimeSdk.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeSdk/1.5.1.zip)
- AdLimeSdk.bundle

ドラッグ & ドロップ完了後、Build Phases > Copy Bundle Resources に AdLimeSdk.bundle が含まれていることを確認してください。

#### Carthage
プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeSdk"
```

コマンドラインから次のコマンドを実行してください:
```objectivec
carthage update
```

### AdLimeSdk-All
#### CocoaPods（推奨）
iOS プロジェクトに AdLime SDK を導入するための、最も簡単な方法は CocoaPods を使用することです。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeSdk-All'
```

コマンドラインから次のコマンドを実行してください:
```objectivec
pod install --repo-update
```

#### 手動ダウンロード
SDK フレームワークを直接ダウンロードして解凍し、下記のフレームワークを Xcode プロジェクトに導入してください。

- [AdLimeSdk.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeSdk/1.5.1.zip)
- AdLimeSdk.bundle
- [Google-Mobile-Ads-SDK.framework](https://developers.google.cn/admob/ios/download)
- GoogleAppMeasurement.framework
- GoogleUtilities.framework
- nanopb.framework
- [AdLimeMediation_GoogleAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_GoogleAds/7.52.0.0.zip)
- [AppLovinSDK.framework](https://dash.applovin.com/docs/sdk/download?type=ios-main)
- [AdLimeMediation_AppLovin.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_AppLovin/6.9.4.0.zip)
- [FBAudienceNetwork.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/FBAudienceNetwork/FBAudienceNetwork_5.6.0.zip)
- [AdLimeMediation_Facebook.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Facebook/5.6.0.0.zip)
- [MoPubSDKFramework.framework](https://github.com/mopub/mopub-ios-sdk/releases/download/5.10.0/mopub-framework-5.10.0.zip)
- [AdLimeMediation_MoPub.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_MoPub/5.10.0.1.zip)
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.5.1.2.zip)
- BUAdSDK.bundle
- [AdLimeMediation_TikTok.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_TikTok/2.5.1.2.0.zip)

ドラッグ & ドロップ完了後、Build Phases > Copy Bundle Resources に AdLimeSdk.bundle,  BUAdSDK.bundleが含まれていることを確認してください。

##### 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の Tiktok フレームワークを追加します。

- AdSupport
- AVFoundation
- CoreGraphics
- CoreMedia
- CoreTelephony
- SafariServices
- StoreKit
- SystemConfiguration
- UIKit
- WebKit
- libz.tbd
- MobileCoreServices
- MediaPlayer
- CoreMotion
- libresolv.9.tbd
- libc++.tbd
- MessageUI
- QuartzCore

##### Info.plist の更新

Info.plist ファイルに、 GADApplicationIdentifier キーと、 AdMob の管理画面で登録したアプリの ID を追加してください。

Info.plist を ソースコードとして開いて編集します。
```objectivec
<key>GADApplicationIdentifier</key>
<string>Your AdMob APP_ID</string>
```
もしくは、プロパティリストエディタ で編集できます。
<img src="./../images/ios/mediation_admob_app_id_plist.png" height="80" />

#### Carthage
SDK フレームワークを直接ダウンロードして解凍し、下記のフレームワークを Xcode プロジェクトに導入してください。
- [Google-Mobile-Ads-SDK.framework](https://developers.google.cn/admob/ios/download)
- GoogleAppMeasurement.framework
- GoogleUtilities.framework
- nanopb.framework
- [AppLovinSDK.framework](https://dash.applovin.com/docs/sdk/download?type=ios-main)
- [FBAudienceNetwork.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/FBAudienceNetwork/FBAudienceNetwork_5.6.0.zip)
- [MoPubSDKFramework.framework](https://github.com/mopub/mopub-ios-sdk/releases/download/5.9.0/mopub-framework-5.10.0.zip)
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.5.1.2.zip)
- BUAdSDK.bundle

ドラッグ & ドロップ完了後、Build Phases > Copy Bundle Resources に AdLimeSdk.bundle,  BUAdSDK.bundleが含まれていることを確認してください。

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLime-iOS-Carthage"
```

コマンドラインから次のコマンドを実行してください:
```objectivec
carthage update
```
##### 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の Tiktok フレームワークを追加します。

- AdSupport
- AVFoundation
- CoreGraphics
- CoreMedia
- CoreTelephony
- SafariServices
- StoreKit
- SystemConfiguration
- UIKit
- WebKit
- libz.tbd
- MobileCoreServices
- MediaPlayer
- CoreMotion
- libresolv.9.tbd
- libc++.tbd
- MessageUI
- QuartzCore

##### Info.plist の更新

Info.plist ファイルに、 GADApplicationIdentifier キーと、 AdMob の管理画面で登録したアプリの ID を追加してください。

Info.plist を ソースコードとして開いて編集します。
```objectivec
<key>GADApplicationIdentifier</key>
<string>Your AdMob APP_ID</string>
```
もしくは、プロパティリストエディタ で編集できます。
<img src="./../images/ios/mediation_admob_app_id_plist.png" height="80" />

## Linker Flags の追加
プロジェクトのビルド設定で、以下のように [Other Linker Flags] に -ObjC を追加します。

<img src="./../images/ios/begin_objc.png" height="140"/>


## App Transport Security
iOS 9 では、App Transport Security（ATS）というプライバシー機能が導入されました。この機能は新しいアプリでデフォルトで有効になり、安全な接続を要求します。

広告が ATS の影響を受けないようにするには、次の作業を行ってください：

NSAllowsArbitraryLoads の例外をアプリの Info.plist ファイルに追加して、ATS による制限を無効にします。

<img src="./../images/ios/begin_ats.png" height="60"/>

```objectivec
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

## 広告フォーマットを選択する
これで AdLime SDK の導入が完了し、広告を配信できるようになりました。AdLime には様々な広告フォーマットが用意されていますので、その中からアプリのユーザー エクスペリエンスに最適なものを選択できます。

### バナー

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-banner.png"  width="100px"  align=left />
バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージ広告、またはテキスト広告です。この種の広告は、ユーザーがアプリを操作している間にスマホ画面に残り、一定の時間が経過すると自動的に更新することが特徴です。モバイル広告を初めて掲載する場合は、まずバナー広告から始めることが最適です。
</div>

### インタースティシャル

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-interstitial.png"  width="100px"  align=left />
インタースティシャル広告とは、ユーザーが消すまで、アプリの上にオーバーレイで表示されるフルスクリーン広告です。ゲームのステージが変わる合間や一つのミッションが完了になった直後など、アプリの画面が切り替わるタイミングでの使用に適しています。
</div>

### ネイティブ

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-native.png"  width="100px"  align=left />
ネイティブ広告とは、コンポーネントに基づくフォーマットで、クリエイティブ（タイトルやキャッチコピーなど）をアプリに表示する方法を自由にカスタマイズできる広告です。フォント・色・その他クリエイティブの詳細設定を行い、コンテンツの邪魔にならないように広告を表示し、ユーザーエクスペリエンスを向上させることができます。
</div>

### 動画リワード

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-rewarded.png"  width="100px"  align=left />
動画リワード広告とは、ユーザーが動画を視聴することと引き換えに、アプリ内で報酬（インセンティブ）を獲得できるフルスクリーン動画広告です。
</div>
