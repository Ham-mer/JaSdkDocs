# Vungle ドキュメント
- [Vungle Webサイト](https://dashboard.vungle.com/dashboard/login)
- [Vungle 開発者ガイド](https://support.vungle.com/hc/en-us/articles/360002922871-Get-Started-with-Vungle-Android-or-Amazon-SDK-v-6)

## 前提条件
- Android API レベル 16 以上

## maven リポジトリの導入
プロジェクトレベルの build.gradle に、下記のレポジトリを追加します。

```java
allprojects {
    repositories {
        // Vungle
        maven { url 'https://jitpack.io' }
    }
}
```

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Vungle
    implementation "com.access_company.adlime:mediation_vungle:6.4.11.1"
    implementation "com.github.vungle:vungle-android-sdk:6.4.11"  
    // Recommended
    implementation "com.google.android.gms:play-services-basement:16.1.0" 
    // Optional  
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
    // Optional  
    implementation "com.google.android.gms:play-services-location:16.0.0"
}
```
## NetworkConfig の設定
### ネイテブ広告ィ
- VungleNativeNetworkConfig<br>
 ネイティブ広告サイズの単位はDPです。サイズは未設定の場合に、広さはスクリーンの広さと同じです。高さは広さの９/１６です。

    ```java
    VungleNativeNetworkConfig.Builder()
                    .setWidth(300)
                    .setHeight(250)
                    .build()

    ```


## 広告フォーマット
### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Vungle |  ◯   |  ◯         | ◯      | ◯   |

### バナーサイズ
Vungle ではバナー広告はありません。AdLime は Flex-Feed Ads をバナー広告として扱います。
Flex-Feed Ads は Vungle では ネイティブ広告に定義されていますが、レイアウトはカスタマイズできません。サイズのみ設定できます。  

|ネットワーク |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90 |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Vungle |       |        | ◯      |       |       |      |

### 設置情報
下記の Vungle の情報が必要となります。  
- App ID
- Placement Reference ID

## バージョン情報

### リリースバージョン
| Vungle バージョン | アダプタ バージョン|
|:-----------------|:--------------|
|  6.4.11          |  6.4.11.1     |
|  6.3.24          |  6.3.24.2     |

### 更新履歴
| バージョン            | 日付        | 更新内容             |
|-----------------|--------------------|---------------------|
|  6.4.11.1       | 2019-11-15         | 1. Vungle SDK 6.4.11 に対応 <br> 2.ネイティブ広告の追加  |
|  6.3.24.2       |  2019-3-15         | 1. Vungle のサポート |
