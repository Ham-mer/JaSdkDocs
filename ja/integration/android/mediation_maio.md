# Maio
- [Maio Webサイト](https://maio.jp/)
- [Maio 開発者ガイド](https://github.com/imobile-maio)

## 前提条件
- Android API レベル 16 以上

## maven リポジトリの導入
プロジェクトレベルの build.gradle に、下記のレポジトリを追加します。

```java
allprojects {
    repositories {
        // Maio
        maven{ url "https://imobile-maio.github.io/maven" }
    }
}
```

## 依存関係の追加
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Maio
    implementation "com.access_company.adlime:mediation_maio:1.1.11.0"
    implementation ("com.maio:android-sdk:1.1.11@aar")
    implementation "com.google.android.gms:play-services-ads:17.2.1"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Maio |     |  ◯         |   ◯    |    |


### 設定情報
下記の Maio の情報が必要になります。  
- Media ID  
- Zone ID  

## バージョン情報

### リリースバージョン
| Maio バージョン | アダプタ バージョン |
|:--------------|:-----------------|
| 1.1.11        | 1.1.11.0         |
| 1.1.10        | 1.1.10.1         |
| 1.1.9         | 1.1.9.1          |
| 1.1.9         | 1.1.9.0          |
| 1.1.8         | 1.1.8.1          |

### バージョン履歴
|  バージョン  | 日付        | 更新内容       |
|------------|-------------|---------------------|
| 1.1.11.0   | 2020/2/17   | - Maio SDK 1.1.11 に対応<br>- プレイアブル広告で遊べない場合に、キャンセルボタンが押せない問題を修正 |
| 1.1.10.1   | 2020/2/10   | テストモードをサポート。[初期化](./init.md)を参考してください。 |
| 1.1.10.0   | 2019/11/4   | Maio SDK 1.1.10 に対応|
| 1.1.9.1    | 2019/10/23  | 内部のロジックを改善する |
| 1.1.9.0    | 2019/7/18   | Maio SDK 1.1.9 に対応 |
| 1.1.8.1    | 2019/6/28   | 動画リワードに対応      |
