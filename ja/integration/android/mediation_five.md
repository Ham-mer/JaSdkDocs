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
    implementation "com.access_company.adlime:mediation_five:20200423.0"
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

### 20200423
| バージョン    | 日付       | 更新情報                          |
|-------------|------------|---------------------------------|
| 20200423.0  | 2020/5/12  | - Five SDK 20200423 に対応<br>- BannerAdViewなどのsetMuted()で動画のおとの調整はできます<br>- [AdLimeSdk](./init.md)到を 1.10.3 以降のバージョンまでアップデートする必要があります|

### 20191029
| バージョン    | 日付       | 更新情報                         |
|-------------|------------|---------------------------------|
| 20191029.2  | 2020/2/10  | テストモードをサポートします，[初期化](./init.md)を参考してください |
| 20191029.1  | 2019/10/31 | Five SDK 20191029 に対応 |