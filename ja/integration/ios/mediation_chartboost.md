# Chartboost ドキュメント
- [Chartboost Webサイト](https://www.chartboost.com)
- [Chartboost 開発者ガイド](https://answers.chartboost.com/en-us/child_article/ios)

## 前提条件
- ターゲットバージョン iOS 9.0 以上

## SDK の導入
AdLime SDK で Chartboost を使用するためには、Chartboost SDK と、それに対応した AdLime SDK を導入してください。

### CocoaPods

CocoaPods を使用すると導入が簡単です。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeMediation_Chartboost'
```

コマンドラインから、以下を実行してください。
```objectivec
pod install --repo-update
```

### 手動でダウンロード
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [Chartboost.framework](https://answers.chartboost.com/en-us/articles/download)
- [AdLimeMediation_Chartboost.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Chartboost/AdLimeMediation_Chartboost_8.0.3.1.zip)

### Carthage
SDK を 直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。
- [Chartboost.framework](https://answers.chartboost.com/en-us/articles/download)

プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeMediation_Chartboost"
```

コマンドラインから、以下を実行してください。
```objectivec
carthage update
```

完了後、Carthage フォルダの AdLimeMediation_Chartboost > AdLimeMediation_Chartboost.framework をプロジェクトにインポートします。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インターステーシャル|リワード動画|ネイティブ|
|:--------:|:----:|:----------:|:-------:|:----:|
|Chartboost| ◯    | ◯          |   ◯     |      |


## 広告枠の設置

AdLime を使って Chartboost の広告枠を設置する前に、Chartboost の管理画面上で広告枠を作成し、その広告枠の情報が必要になります。
- APP ID
- APP Signature

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、Chartboost を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Chartboost を表示する広告枠で、「広告のソース追加」をクリックし、Chartboost を追加してください。

- location の設定可能な値
    - Default
    - Startup
    - Home Screen，
    - Main Menu
    - Game Screen
    - Achievements
    - Quests
    - Pause
    - Level Start
    - Level Complete
    - IAP Store
    - Item Store
    - Game Over
    - Leaderboard
    - Settings
    - Quit

デフォルト値 ： **Default**

## バージョン情報

### リリースバージョン
| Chartboost バージョン | アダプタ バージョン |
|:-----------------|:----------------|
| 8.0.3            | 8.0.3.1         |
| 8.0.1            | 8.0.1.2         |

### バージョン履歴
| バージョン        | 日付       | 更新内容                           |
|-----------------|------------|----------------------------------|
| 8.0.3.1         | 2019-11-18  | バナー広告をサポートする|
| 8.0.3.0         | 2019-11-7   | Chartboost 8.0.3 に対応|
| 8.0.1.2         | 2019-09-19  | Chartboost 8.0.1 に対応|