# IronSource ドキュメント
- [IronSource Webサイト](https://ironsrc.com/)
- [IronSource 開発者ガイド](https://developers.ironsrc.com/ironsource-mobile/ios/ios-sdk/#step-1)

## 前提条件
- ターゲットバージョン iOS 8.0 以上

## SDKの導入
AdLime SDK で IronSource Audience Network を使用するために、 IronSource Audience Network SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_IronSource'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [IronSource.framework](https://dl.bintray.com/ironsource-mobile/ios-sdk/IronSource6.10.0.zip)
- [AdLimeMediation_IronSource.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_IronSource/6.10.0.0.0.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [IronSource.framework](https://dl.bintray.com/ironsource-mobile/ios-sdk/IronSource6.10.0.zip)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_IronSource"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_IronSource > AdLimeMediation_IronSource.framework をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:-----:|:----:|:----------:|:------:|:----:|
|IronSource  |Y     | Y          |Y       |     |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:| --------:|:-------:|:------:|:------:|:-------:|
|IronSource    |Y       |Y         |Y        |        |        |  Y       |

## 広告枠の設置
AdLime を使って IronSource Audience Network の広告枠を配置する前に、IronSource Audience Network の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- App Key
- Instance ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 IronSource を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 IronSource Audience Network 広告を表示する広告枠で、「広告のソース追加」をクリックし、 IronSource Audience Network 広告を追加してください。

## バージョン情報

### リリースバージョン
| IronSource バージョン | アダプタ バージョン |
|:--------------------|:----------------|
| 6.10.0.0            | 6.10.0.0.0       |
| 6.8.7.0             | 6.8.7.0.0        |

### バージョン履歴
| バージョン  | 日付       | 更新内容                              |
|-----------|------------|-----------------------------------|
| 6.10.0.0.0| 2019-11-7  | IronSource SDK 6.10.0.0 に対応|
| 6.8.7.0.0 | 2019-10-14 | IronSource SDK 6.8.7.0 に対応|
