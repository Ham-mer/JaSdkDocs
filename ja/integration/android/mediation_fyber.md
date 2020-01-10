# Fyberドキュメント
- [Fyber Webサイト](https://revenuedesk.inner-active.com/dashboard/dates/chart)
- [Fyber 開発者ガイド](http://developer.inner-active.com/docs/welcome)

## 前提条件
- Android API レベル 15 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    implementation "com.access_company.adlime:mediation_fyber:7.2.1.0"
    implementation "com.access_company.adlime:ia-mraid-kit-release:7.2.1"
    implementation "com.access_company.adlime:ia-native-kit-release:7.2.1"
    implementation "com.access_company.adlime:ia-sdk-core-release:7.2.1"
    implementation "com.access_company.adlime:ia-video-kit-release:7.2.1"
    implementation "com.google.code.gson:gson:2.8.4"
    // Add gson to support native ads
    implementation "com.google.android.gms:play-services-base:16.1.0"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
}
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Fyber | ◯    | ◯          |       |  ◯  |

### バナーサイズ
|ネットワーク |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90 |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Fyber  | ◯     | ◯      |        | ◯     | ◯     |      |

### 設定情報
下記の Fyber の情報が必要となります。　　　　　　
- App ID  
- Spot ID

## バージョン情報

### リリースバージョン
| Fyber バージョン | アダプタ バージョン|
|:-----------------|:--------------|
| 7.2.1           |   7.2.1.0    |
| 7.1.7           |   7.1.7.2    |




### バージョン履歴
| バージョン           | 日付              | 更新内容              |
|-----------------|--------------------|---------------------|
|   7.2.1.0     | 2019/4/8      |Fyber SDK 7.2.1 に対応。広告のレンダリングの改善| 
