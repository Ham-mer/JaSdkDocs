# Chartboostドキュメント
- [Chartboost Webサイト](https://dashboard.chartboost.com/all/publishing)
- [Chartboost 開発者ガイド](https://answers.chartboost.com/en-us/child_article/android)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Chartboost
    implementation "com.access_company.adlime:mediation_chartboost:7.3.1.6"
    implementation "com.google.android.gms:play-services-base:16.1.0"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Chartboost |     | Y          | Y      |    |

### 設定情報
下記の Chartboost の情報が必要になります。  
- App ID  
- App Signature  
- Location&emsp;&emsp;**※Location はオプション**

## バージョン情報

### リリースバージョン
| Chartboost バージョン | アダプタ バージョン|
|:-----------------|:--------------|
| 7.3.1           | 7.3.1.5      |

### バージョン履歴
| バージョン  | 日付          | 更新内容                |
|-----------------|--------------------|---------------------|
| 7.3.1.5 |  2019-3-11 |非 Host Activity ライフサイクルのコールバックによって広告が表示されない不具合の修正 | 
| 7.3.1.4 |  2019-3-11 |Activity の不完全なライフサイクルによって広告が表示されない不具合の修正 |
| 7.3.1.3 |  2019-3-5 |インタースティシャル・動画リワード広告が表示されない際に、コールバックが呼び出されない問題の修正 | 
