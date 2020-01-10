# Unity Ads ドキュメント
- [Unity Ads Webサイト](https://operate.dashboard.unity3d.com)
- [Unity Ads 開発者ガイド](https://unityads.unity3d.com/help/android/integration-guide-android)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    implementation "com.access_company.adlime:mediation_unity:3.1.0.1"
    implementation "com.access_company.adlime:unity-ads:3.1.0"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- バナー広告を使用する場合、BannerAdView コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット
### 利用可能なフォーマット

|ネットワーク    |バナー|インタースティシャル|動画リワード|ネイティブ|
|:---------:|:----:|:----------:|:------:|:----:|
| Unity Ads | ◯    | ◯          | ◯      |      |

### バナーサイズ
|ネットワーク    |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90 |スマート |
|:---------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Unity Ads | ◯     |        |        |       |       |      |

### 設定情報
下記の Unity Ads の情報が必要となります。  
- Game ID
- Placement ID

## バージョン情報

### リリースバージョン
| Unity Ads バージョン | アダプタ バージョン |
|:-------------------|:------------------|
| 3.1.0         | 3.1.0.1       |
| 3.1.0         | 3.1.0.0       |

### バージョン履歴
| バージョン  | 日付       | 更新内容      |
|-----------|------------|---------------------|
| 3.1.0.1   | 2019/9/8   | SDKの最適化|
| 3.1.0.0   | 2019/7/19  | Unity Ads SDK 3.1.0 に対応|
