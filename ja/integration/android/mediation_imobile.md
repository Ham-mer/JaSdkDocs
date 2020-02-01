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
    implementation "com.access_company.adlime:mediation_imobile:2.0.20.1"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
}
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

### 設定情報
下記の Imobile の情報が必要になります。  
- Publish ID
- Media ID
- Spot ID

### 注意
Imobileの広告は初期化される時にコンテクストの導入は必要です。

## バージョン情報

### リリースバージョン
| Imobile バージョン | アダプタ バージョン|
|:-----------------|:--------------|
| 2.0.20      | 2.0.20.1     |





### バージョン履歴
| バージョン        | 日付               | 更新内容                |
|-----------------|--------------------|---------------------|
| 2.0.20.1  | 2020-2-1                | 初回リリース  |  
