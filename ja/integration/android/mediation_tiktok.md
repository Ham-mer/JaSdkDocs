# TikTok
-  [TikTok  公式サイト&開発者ガイド](https://ad.toutiao.com/union/media/login/)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    implementation "com.access_company.adlime:mediation_toutiao:2.5.3.2.2"
    implementation "com.access_company.adlime:toutiao_open_ad_sdk:2.5.3.2"
    implementation 'pl.droidsonroids.gif:android-gif-drawable:1.2.6'  
    implementation 'com.android.support:support-v4:27.1.1'
}
```

## AndroidManifest の設定
```java
<!-- 追加 -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>
<uses-permission android:name="android.permission.GET_TASKS"/>

<!-- 追加，同意を貰って位置情報を取得すると、TikTok はこの権限を基づいて精確にターゲットできる告 -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

**TikTok SDKは上記の権限を強制取得ではない、取得しなくても広告をリクエストできる。上記の権限を取得してから TikTok はもっと精確にターゲットしてユーザ体験改善してecpmを高める。**

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること

## 広告フォーマット
### 利用可能な広告フォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| TikTok |  ◯   |   ◯        | ◯      | ◯   |

### バナーサイズ
|ネットワーク |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90  |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:------:|:----:|
| TikTok | ◯     | ◯      | ◯      | ◯     | ◯      |      |

### バージョン情報
下記の TikTok の情報が必要となります。  
- App ID
- Code ID

## バージョン情報

### リリースバージョン
| TikTok バージョン  | アダプタ バージョン|
|:-----------------|:-----------------|
|2.5.3.2     |2.5.3.2.2      |
|2.5.2.6     |2.5.2.6.1      |
|2.3.0.7     |2.3.0.7.14     |
|2.2.0.2     |2.2.0.2.1      |

### 更新履歴
|バージョン   | 日付        | 更新内容                        |
|------------|------------|--------------------------------------|
| 2.5.3.2.2  | 2020-1-6   | TikTok SDK 2.5.3.2 に対応|
| 2.5.2.6.1  | 2019/12/2  | TikTok SDK 2.5.2.6 に対応|
| 2.3.0.7.14 | 2019/11/21 | デフォルトで位置情報の許可要求を無効化|
| 2.3.0.7.8  | 2019/9/30  | TikTok SDK 2.3.0.7 に対応|
| 2.2.0.2.1	 | 2019/8/6   | TikTok SDK 2.2.0.2 に対応|
