# Flurryドキュメント
- [Flurry Webサイト](http://www.flurry.com/)
- [Flurry 開発者ガイド](https://developer.yahoo.com/flurry/docs/publisher/code/android-ad-publishing/)

## 前提条件
- Android API レベル 16 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Flurry
    implementation "com.access_company.adlime:mediation_flurry:11.4.0.2"
    implementation "com.flurry.android:analytics:11.4.0@aar"
    implementation "com.flurry.android:ads:11.4.0@aar"
    // 推奨
    implementation "com.google.android.gms:play-services-base:16.1.0"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- バナー広告を使用する場合、BannerAdView コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Flurry | ◯    | ◯         | ◯      | ◯   |

### バナーサイズ
|ネットワーク |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Flurry | ◯     |        |        |       |       |      |

### 設定情報
下記の Flurry の情報が必要になります。　　　　　　 
- Api Key  
- AdUnit Name

## バージョン情報

### リリースバージョン
| Flurry バージョン| アダプタ バージョン|
|:-----------------|:--------------|
| 11.4.0          |   11.4.0.2    |

### バージョン履歴
| バージョン            | 日付            | 更新内容              |
|-----------------|--------------------|---------------------|
| 11.4.0.2        |   2020/2/10        | 調整モードをサポートします，[初期化](./init.md)を参考してください|
| 11.4.0.0        |   2019/2/20        | Flurry に対応 | 
