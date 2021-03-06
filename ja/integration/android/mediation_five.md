# Five ドキュメント

- [Five Webサイト](https://www.five-corp.com/)
- [Five 開発者ガイド](https://partner.fivecdm.com/help/integration)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Five
    implementation "com.access_company.adlime:mediation_five:20200610.1"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
}
```

## AndroidManifest の設定
```java
<application
    android:hardwareAccelerated="true">
    ...
</application>
```

## 広告フォーマット

### 利用可能なフォーマット
|ネットワーク |バナー |インタラクション |動画リワード |ネイティブ |
|:---------:|:----:|:------------:|:---------:|:--------:|
| Five      | ◯    | ◯            | ◯         |          |

### バナーサイズ
|ネットワーク | 320×50 | 300×250 | 320×100 | 468×60 | 728×90 |
|:---------:|:------:|:-------:|:-------:|:------:|:------:|
| Five      | ◯      | ◯       | ◯       |        |        |


## バージョン情報
### 20200610
| バージョン    | 日付       | 更新情報                          |
|-------------|------------|---------------------------------|
| 20200610.1  | 2020/7/4   | Bug Fix |
| 20200610.0  | 2020/6/30  | - Five SDK 20200610 に対応：初期化の時間を短縮化し、動画の再生を改善します|

### 20200423
| バージョン    | 日付       | 更新情報                          |
|-------------|------------|---------------------------------|
| 20200423.0  | 2020/5/12  | - Five SDK 20200423 に対応<br>- バナー広告などで `setMuted()` API により広告の音声をミュートに設定可能。 <br>- [AdLimeSdk](./init.md)を 1.10.3 以上のバージョンまでアップデートする必要があります |

### 20191029
| バージョン    | 日付       | 更新情報                         |
|-------------|------------|---------------------------------|
| 20191029.2  | 2020/2/10  | テストモードをサポート。[初期化](./init.md)を参考してください |
| 20191029.1  | 2019/10/31 | Five SDK 20191029 に対応 |