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
    implementation "com.access_company.adlime:mediation_five:20191029.1"
    implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
}
```

## AndroidManifest の設定
```java
android:hardwareAccelerated="true"
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタラクション|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Five    | ◯   | ◯          | ◯      |      |

### バナーサイズ
|ネットワーク   |320 × 50   |300 × 250   |320 × 100   |468 × 60   |728 × 90   |スマート   |
| :------: | :------: | :--------: | :-------: | :------: | :------: | :-------: |
|Five      | ◯        | ◯          | ◯         |          |          |           |

### 設定情報
下記の Five の情報が必要になります。   
- APP ID  
- SLOT ID

## バージョン情報

### リリースバージョン
| Five バージョン  | アダプタ バージョン|
|:----------------|:------------------|
| 20191029        | 20191029.1        |

### バージョン履歴
| バージョン   | 日付       | 更新情報                      |
|-------------|------------|---------------------------------|
| 20191029.1  | 2019/10/31 | Five SDK 20191029 に対応 |
