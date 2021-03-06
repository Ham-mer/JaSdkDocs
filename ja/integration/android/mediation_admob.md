# AdMob ドキュメント

- [AdMob Webサイト](https://apps.admob.com/v2/home)
- [AdMob 開発者ガイド](https://developers.google.com/admob/android/quick-start?hl=zh-CN)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // AdMob
   implementation "com.access_company.adlime:mediation_admob:19.4.0.0"
   implementation "com.google.android.gms:play-services-ads:19.4.0"
}
```

## AndroidManifest の設定
AdMob 17.0.0 以降のバージョンにおいて、meta-data を設定する必要があります。
ADMOB_APP_ID に AdMob のコンソール画面で登録したアプリの App ID を入れ替えてください。
```java
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="[ADMOB_APP_ID]"/>
```

## NetworkConfig 設置
AdMobをカスタマイズで設置します。[AdMob NetworkConfig](./mediation/config/networkconfig_admob.md) を参考してください。

## 広告フォーマット

### 利用可能なフォーマット
|ネットワーク |バナー |インタラクション |動画リワード |ネイティブ |
|:---------:|:----:|:------------:|:---------:|:--------:|
| AdMob     | ◯    | ◯            | ◯         | ◯        |

### バナーサイズ
|ネットワーク | 320×50 | 300×250 | 320×100 | 468×60 | 728×90 |
|:---------:|:------:|:-------:|:-------:|:------:|:------:|
| AdMob     | ◯      | ◯       | ◯       | ◯      | ◯      |

## バージョン情報

### 19.4.0
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 19.4.0.0   | 2020/9/30  |AdMob SDK 19.4.0 に対応，API30を対象とするアプリのAndroid11デバイスのサポートが追加されました|

### 19.1.0
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 19.1.0.0   | 2020/4/27  |AdMob SDK 19.1.0 に対応|

### 19.0.1
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 19.0.1.0   | 2020/4/20  | - AdMob SDK 19.0.1 に対応（Android APIレベル 16以上必須）。<br> ネイティブ広告などで `setMuted()` API により広告の音声をミュートに設定可能になります。<br>[ - AdLimeSdk](./init.md)を 1.10.3 以上のバージョンにアップデートが必要|

### 18.3.0
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 18.3.0.3   | 2020/3/4   | バナー広告はアダプティブ バナーをサポート。[AdLimeAdMobBannerConfig](./mediation/config/networkconfig_admob.md) で広告のサイズを設定が可能。ドキュメントは [Adaptive Banner 紹介](https://developers.google.com/admob/android/banner/adaptive) 参照|
| 18.3.0.0   | 2020/2/7   |AdMob SDK 18.3.0 に対応。AndroidX に移行 |

### 17.2.1
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 17.2.1.6   | 2019/11/26 |内部ロジックの改善|
| 17.2.1.5   | 2019/10/31 |ネイティブ広告とフィードリスト広告で、Interactive エリアを設定時に、MediaViewLayout がない場合に画像が表示されない問題を修正|
| 17.2.1.2   | 2019/10/2  |ネイティブ広告はクリックエリアのカスタムをサポート|
| 17.2.1.0   | 2019/7/18  |AdMob SDK 17.2.1 に対応。複数のリワード広告の読み込みに対応|

### 17.1.2
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 17.1.2.12  | 2019/11/26 |内部ロジックの改善|
| 17.1.2.11  | 2019/10/31 |ネイティブ広告とフィードリスト広告で、Interactive エリアを設定した場合に、MediaViewLayout を追加しない場合に画像が表示されない問題を修正|
| 17.1.2.7   | 2019/7/16  |動画リワード広告のクリックイベントが通知されない問題を修正 |
| 17.1.2.4   | 2019/6/12  |ネイティブ広告のクリックイベントの改善|

### 15.0.1
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 15.0.1.10  | 2019/11/26 |内部ロジックの改善|
| 15.0.1.9   | 2019/10/31 |ネイティブ広告とフィードリスト広告で、Interactive エリアを設定した場合に、MediaViewLayout を追加しない場合に画像が表示されない問題を修正|
