# MoPub
- [MoPub Webサイト](https://app.mopub.com/apps)
- [MoPub 開発者ガイド](https://developers.mopub.com/docs/ui/)

## 前提条件
- Android API レベル 19 以上

## maven リポジトリの導入
プロジェクトレベルの build.gradle に、下記のレポジトリを追加します。

```java
allprojects {
    repositories {
        // MoPub
        maven { url "https://s3.amazonaws.com/moat-sdk-builds" }
    }
}
```

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
    implementation "com.access_company.adlime:mediation_mopub:5.11.1.5"
    implementation("com.mopub:mopub-sdk:5.11.1@aar") {
        transitive = true
        exclude module: 'moat-mobile-app-kit'
    }
    implementation "com.access_company.adlime:mopub-moat-mobile-app-kit:2.4.5"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
    implementation "com.google.android.gms:play-services-base:16.1.0"
}
```

## AndroidManifest は一致
```java
<!— MoPub は ACCESS_COARSE_LOCATIONという権限を持っています。もし削除したい場合に、下記のコードを使ってください—>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" tools:node="remove" />

<application android:networkSecurityConfig="@xml/mopub_network_security_config"/>
```

もしあなたのapplicationラベルにはすでに android:networkSecurityConfigがある場合に mopub_network_security_config.xmlというファイルを既存xmlファイルに追加してください。

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定すること

## 広告フォーマット
### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------:|:----:|:----------:|:------:|:----:|
| MoPub  | ◯    | ◯          | ◯      | ◯    |

### バナーサイズ
|ネットワーク |320×50 |300×250 |320×100 |468×60 |728×90  |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:------:|:----:|
| MoPub  | ◯     | ◯      | ◯      | ◯     | ◯      |      |

### 設定情報
下記の MoPub の情報が必要となります。  
- AdUnit ID

## バージョン情報

### 5.11.1
| バージョン  | 日付       | 更新内容                        |
|-----------|------------|-------------------------------|
| 5.11.1.5  | 2020/3/31  | ある場合にネイティブ広告の表示コールバックがない問題を修正 |
| 5.11.1.1  | 2020/3/12  | - MoPub SDK 5.11.1 に対応 <br>- ネイティブ広告のボタンが押せない問題を修正 |

### 5.11.0
| バージョン  | 日付       | 更新内容                        |
|-----------|------------|-------------------------------|
| 5.11.0.0  | 2020/2/17  | - MoPub SDK 5.11.0 に対応<br>- Android API のレベル 19以上にターゲット。 <br>- ドキュメントには maven と AndroidManifest 配置を追加しました<br>- Android X に移行<br>- Activityでインタースティシャル広告を初期化する必要があります |

### 5.8.0
| バージョン  | 日付       | 更新内容                        |
|-----------|------------|-------------------------------|
| 5.8.0.2   | 2020/2/10  | デバッグモードをサポート。[初期化](./init.md)を参考してください |
| 5.8.0.1   | 2019/11/24 | 動画リワードのコールバック時の問題を修正 |
| 5.8.0.0   | 2019/11/5  | MoPub SDK 5.8.0 に対応 |

### 5.7.1
| バージョン  | 日付       | 更新内容                        |
|-----------|------------|-------------------------------|
| 5.7.1.3   | 2019/10/5  | SDKの最適化 |
| 5.7.1.0   | 2019/7/19  | MoPub SDK 5.7.1 に対応 |