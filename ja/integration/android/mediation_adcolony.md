# Adcolony 導入ドキュメント
- [AdColony Webサイト](https://www.adcolony.com/publishers/)
- [AdColony 開発者ガイド](https://github.com/AdColony/AdColony-Android-SDK-3/wiki/Project-Setup)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // AdColony
    implementation "com.access_company.adlime:mediation_adcolony:3.3.7.4"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
}
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク |バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
|AdColony|      | ◯          |◯       |      |

### 設定情報
下記の AdColony の情報が必要になります。
- App ID  
- Zone ID  

## バージョン情報

### リリースバージョン
| AdColony バージョン | アダプタ バージョン|
|:----------------|:-------------|
|3.3.7             |3.3.7.3        |

### バージョン履歴
| バージョン  | 日付        | 更新情報            |
|:---------|:------------|:--------------------|
|3.3.7.3    |2019-2-22  |初期化する際に、Activity の代わりに Application を使用 |
