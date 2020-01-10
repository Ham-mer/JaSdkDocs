# MoPub
- [MoPub Webサイト](https://app.mopub.com/apps)
- [MoPub 開発者ガイド](https://developers.mopub.com/docs/ui/)

## 前提条件
- Android API レベル 16 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
android {
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    // MoPub
    implementation "com.access_company.adlime:mediation_mopub:5.8.0.1"
    implementation "com.google.android.gms:play-services-basement:16.1.0"
    implementation("com.mopub:mopub-sdk:5.8.0@aar") {
        transitive = true
        exclude module: 'moat-mobile-app-kit'
        exclude module: 'mopub-sdk-interstitial'
    }
    implementation "com.access_company.adlime:mopub-moat-mobile-app-kit:2.4.5"
    implementation "com.access_company.adlime:mopub-sdk-interstitial:5.8.0"
}
```

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット
### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------:|:----:|:----------:|:------:|:----:|
| MoPub  | ◯    | ◯          | ◯      | ◯    |

### バナーサイズ
|ネットワーク |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90  |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:------:|:----:|
| MoPub  | ◯     | ◯      |        |       | ◯      |      |

### 設定情報
下記の MoPub の情報が必要となります。  
- AdUnit ID

## バージョン情報

### リリースバージョン
| MoPub バージョン  | アダプタ バージョン |
|:----------------|:-----------------|
| 5.8.0           | 5.8.0.1          |
| 5.7.1           | 5.7.1.3          |
| 5.7.1           | 5.7.1.0          |

### バージョン履歴
| バージョン  | 日付       | 更新内容                   |
|-----------|------------|-------------------------------|
| 5.8.0.1   | 2019/11/24 | 動画リワードのコールバック時の問題を修正 |
| 5.8.0.0   | 2019/11/5  | MoPub SDK 5.8.0 に対応 |
| 5.7.1.3   | 2019/10/5  | SDKの最適化 |
| 5.7.1.0   | 2019/7/19  | MoPub SDK 5.7.1 に対応 |
