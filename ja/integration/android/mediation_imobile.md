# Imobile ドキュメント
- [Imobile Webサイト](https://sppartner.i-mobile.co.jp/login.aspx)
- [Imobile 開発者ガイド](https://sppartner.i-mobile.co.jp/sdk_download.aspx)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Imobile
    implementation "com.access_company.adlime:mediation_imobile:2.0.20.5"
    implementation 'com.google.android.gms:play-services-ads-identifier:16.0.0'
}
```

## AndroidManifest の設定
AndroidManifestでmeta-dataを設置して調整モードの設置はできます。

```java
<application >

    <!-- 調整モード開始，android:valueを trueに設定します -->
    <meta-data android:name="i-mobile_DebugLogging" android:value="false" />
</application>
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Imobile |  ◯   |   ◯        |       | ◯   |

### バナーサイズ
|ネットワーク |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90 |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Imobile | ◯     | ◯      |  ◯       |       |       |      |

### 注意
Imobileの広告は初期化される時にコンテクストの導入は必要です。

## バージョン情報

### 2.0.20
| バージョン        | 日付             | 更新内容             |
|-----------------|------------------|---------------------|
| 2.0.20.5        | 2020-2-21        | コンテナビューアーからロードされるバナー広告を削除してもう一回追加するとバナーはないという問題を解決します|
| 2.0.20.2        | 2020-2-18        | バナー広告とネイティブ広告のコールバックは違うという問題を解決します |
| 2.0.20.1        | 2020-2-1         | 初回リリース  |