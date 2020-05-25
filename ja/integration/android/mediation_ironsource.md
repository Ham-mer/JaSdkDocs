# IronSource ドキュメント
- [IronSource Webサイト](https://platform.ironsrc.com/partners)
- [IronSource 開発者ガイド](https://developers.ironsrc.com/ironsource-mobile/android/android-sdk/#step-1)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // IronSource
    implementation "com.access_company.adlime:mediation_ironsource:6.8.0.1.6"
    implementation "com.android.support:support-v4:26.1.0"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
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
| IronSource | ◯    |   ◯        |  ◯     |    |

### バナーサイズ
|ネットワーク     |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:----------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| IronSource | ◯     | ◯      | ◯      |       |       |      |

### 設定情報
下記の IronSource の情報が必要となります。   
- App Key  
- Instance ID&emsp;&emsp;**※Instance ID はオプションです**

## バージョン情報

### リリースバージョン
| AdColony バージョン | アダプタ バージョン|
|:-----------------|:--------------|
|     6.8.0.1       |  6.8.0.1.5      |

### バージョン履歴
| バージョン  | 日付        | 更新内容            |
|-----------------|--------------------|---------------------|
|   6.8.0.1.5     |  2019/5/5      |混在するファイルの改善  | 
