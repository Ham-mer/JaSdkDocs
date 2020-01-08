# Unity Ads ドキュメント
- [Unity Ads Webサイト](https://operate.dashboard.unity3d.com)
- [Unity Ads 開発者ガイド](https://unityads.unity3d.com/help/ios/integration-guide-ios)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDKの導入
AdLime SDK で Unity 広告を使用するためには、 Unity Ads SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods（推奨）
Unity Ads SDK は手動ダウンロードのみ対応しています。[Unity Ads SDK ダウンロード](https://github.com/Unity-Technologies/unity-ads-ios/releases/download/3.3.0/UnityAds.framework.zip)

AdLime SDK に導入するには，プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_UnityAds'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [UnityAds.framework](https://github.com/Unity-Technologies/unity-ads-ios/releases/download/3.3.0/UnityAds.framework.zip)
- [AdLimeMediation_UnityAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_UnityAds/3.3.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [UnityAds.framework](https://github.com/Unity-Technologies/unity-ads-ios/releases/download/3.3.0/UnityAds.framework.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_UnityAds"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_UnityAds > AdLimeMediation_UnityAds.framework をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|動画リワード|ネイティブ|
|:-----:|:----:|:----------:|:------:|:----:|
|Unity Ads |◯     | ◯          |◯       |      |

### バナーサイズ
|ネットワーク   |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Unity Ads |◯       |          |         |        |        |         |

## 広告枠の配置
AdLime を使って Unity Ads の広告枠を設置する前に、 Unity Ads の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- Game ID
- Placement ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Unity Ads を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Unity Ads を表示する広告枠で、「広告のソース追加」をクリックし、 Unity Ads を追加してください。

## バージョン情報

### リリースバージョン
| Unity Ads バージョン| Adapter バージョン |
|:-----------------|:----------------|
|3.3.0             |3.3.0.0          |
|3.1.0             |3.1.0.2          |

### バージョン履歴
| バージョン         | 日付       | 更新内容                             |
|-----------------|------------|----------------------------------|
| 3.3.0.0         | 2019-10-10  | Unity Ads SDK 3.3.0 に対応|
| 3.1.0.2         | 2019-8-4    | 不要なヘッダーファイルの削除|
| 3.1.0.1         | 2019-7-15   | 動画リワード広告のイベント最適化|
| 3.1.0.0         | 2019-6-30   | Unity Ads SDK 3.1.0 に対応|
