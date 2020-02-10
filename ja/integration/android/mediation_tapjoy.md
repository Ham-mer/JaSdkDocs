# Tapjoy ドキュメント
- [Tapjoy Webサイト](https://ltv.tapjoy.com)
- [Tapjoy 開発者ガイド](https://ltv.tapjoy.com/s/5c78bb63-2e0b-8000-8000-b69a15000302/onboarding#guide/placement?os=android)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Tapjoy
    implementation "com.access_company.adlime:mediation_tapjoy:12.2.0.2"
    implementation "com.tapjoy:tapjoy-android-sdk:12.2.0@aar"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット
### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------:|:----:|:----------:|:------:|:----:|
| Tapjoy |      | ◯          | ◯      |      |

### 設定情報
下記の Tapjoy の情報が必要となります。  
- SDK Key  
- Placement Name

## バージョン情報

### リリースバージョン
| Tapjoy バージョン | アダプタ バージョン|
|:-----------------|:--------------|
|  12.2.0          |  12.2.0.2     |

### バージョン履歴
| バージョン  | 日付        | 更新内容                 |
|-----------------|--------------------|---------------------|
|  12.2.0.2       |2020/2/10     |調整モードをサポートします，[初期化](./init.md)を参考してください|
|  12.2.0.0       |2019/3/3      |Tapjoy に対応   | 
