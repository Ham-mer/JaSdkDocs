# InMobi ドキュメント
- [InMobi Webサイト](https://www.inmobi.com/)
- [InMobi 開発者ガイド](https://support.inmobi.com/monetize/getting-started/)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // InMobi
    implementation "com.access_company.adlime:mediation_inmobi:7.2.2.7"
    implementation "com.inmobi.monetization:inmobi-ads:7.2.2"
    implementation "com.google.android.gms:play-services-base:16.1.0"
    implementation "com.google.android.gms:play-services-ads:17.1.2"
    implementation "com.google.android.gms:play-services-location:16.0.0"
    implementation "com.google.android.gms:play-services-plus:16.0.0"
    implementation "com.squareup.picasso:picasso:2.5.2"
    implementation "com.android.support:support-v4:26.1.0"
    implementation "com.android.support:recyclerview-v7:27.1.0"
}
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| InMobi |  ◯   |   ◯        |  ◯     | ◯   |

### バナーサイズ
|ネットワーク |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| InMobi | ◯     | ◯      |        |       |       |      |

### 設定情報
下記の InMobi の情報が必要になります。  
- Account ID  
- Placement ID

## バージョン情報

### リリースバージョン
| InMobi バージョン | アダプタ バージョン|
|:-----------------|:--------------|
| 7.2.2           |   7.2.2.7    |


### バージョン履歴
| バージョン        | 日付               | 更新内容                |
|-----------------|--------------------|---------------------|
| 7.2.2.7	      | 2020/2/10          | デバッグモードをサポート。[初期化](./init.md)を参考してください。|
| 7.2.2.4	      | 2019/8/19	       | ネイティブ広告のクリックエリアのカスタマイズに対応 |
| 7.2.2.3         | 2019/3/20          | 初回リリース  |  
