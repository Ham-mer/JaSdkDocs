# Tiktok
- [Tiktok Webサイト](https://ad.oceanengine.com/union/media/login/?from=i18n)
- [Tiktok 開発者ガイド](https://ad.oceanengine.com/union/media/union/download)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Tiktok 広告ネットワークを使用するためには、 Tiktok SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）
**TikTok　2.7.5.2 から、Bytedance-UnionADのクラスは大きくてpod installの前にGIT-LFSをインストールしてください。https://github.com/git-lfs/git-lfs で確認をお願いします。もしGit-LFSをインストールしてもエラーが出る場合に、PODのキャッシュをクリアしてPOD INSTALLをお願いします。**

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_TikTok'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.9.0.7.zip)
- BUAdSDK.bundle
- [AdLimeMediation_TikTok.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_TikTok/2.9.0.7.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.9.0.7.zip)
- BUAdSDK.bundle

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Tiktok"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Tiktok > AdLimeMediation_TikTok.framework をプロジェクトにインポートします。

## 他のフレームワークの追加
Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

- StoreKit.framework
- MobileCoreServices.framework
- WebKit.framework
- MediaPlayer.framework
- CoreMedia.framework
- AVFoundation.framework
- CoreTelephony.framework
- SystemConfiguration.framework
- AdSupport.framework
- CoreMotion.framework
- libresolv.9.tbd
- libc++.tbd
- libz.tbd

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー   |インタースティシャル        |動画リワード |ネイティブ |
|:-----:|:----:|:----------:|:------:|:----:|
|Tiktok |      | ◯          |◯       |◯     |

## テスト広告の表示
SDK を導入し、広告を実装したら広告が正しく表示されるかテストしましょう。[広告表示テスト](./test.md#TikTok) の App ID と広告枠 ID を設定して広告が正しく表示されるか確認してください。

## バージョン情報

### 2.9.0.7
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.9.0.7.0       | 2020/4/24  | - 2.9.0.7 に対応，iOS 12以上のバージョンでAppStoreのクラッシュが発生するというエラーを修正します<br><br>- [AdLimeSdk](./init.md)到を 1.8.0 以降のバージョンまでアップデートする必要があります|

### 2.8.0.1
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.8.0.1.1       | 2020/2/28   | ネイティブ広告ロード失敗の問題を解決します|
| 2.8.0.1.0       | 2020/2/21   | 2.8.0.1 に対応|

### 2.7.5.2
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.7.5.2.5       | 2020/2/5    | - 2.7.5.2 に対応<br><br>- 調整モードをサポートします，[初期化](./init.md)を参考してください|

### 2.5.1.5
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.5.1.5.1       | 2019/12/8   | 2.5.1.5バージョンに適応してカスタマイズモデルのフールスクリングと動画リワードをサポートする|

### 2.5.1.2
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.5.1.2.0       | 2019/11/7   | Tiktok Ads SDK 2.5.1.2 に対応|

### 2.4.6.3
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.4.6.3.1       | 2019/10/10  | Tiktok Ads SDK 2.4.6.3 に対応|

### 2.1.0.1
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 2.1.0.1.5       | 2019/8/6    | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
| 2.1.0.1.2       | 2019/7/15   | 動画リワード広告のイベント最適化             |
| 2.1.0.1.1       | 2019/7/8    | 動画リワード広告の初期化できない問題に対応 |
| 2.1.0.1.0       | 2019/7/5    | Tiktok Ads SDK 2.1.0.1 に対応|
