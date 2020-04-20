# Facebookドキュメント
- [Facebook Webサイト](https://business.facebook.com/pub/home)
- [Facebook 開発者ガイド](https://developers.facebook.com/docs/audience-network/android)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // Facebook
    implementation "com.access_company.adlime:mediation_facebook:5.7.1.0"
    implementation "com.facebook.android:audience-network-sdk:5.7.1"
    implementation "com.android.support:support-annotations:28.0.0"
}
```

## AndroidManifest の設定
すでに application タグに android:networkSecurityConfig が存在する場合は、 facebook_network_security_config.xml の内容を、指定されている XML ファイルに統合してください。
```java
<application android:networkSecurityConfig="@xml/facebook_network_security_config"/>
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Facebook | ◯    | ◯          |  ◯     | ◯   |

### バナーサイズ
|ネットワーク   |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:--------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Facebook | ◯     | ◯      | ◯      |       |       |      |

### 設定情報
下記の Facebook の情報が必要となります。　　
- Placement ID

## バージョン情報

### リリースバージョン
| Facebook バージョン | アダプタ バージョン|
|:-----------------|:--------------|
|5.7.1         |   5.7.1.0     |
|5.6.1         |   5.6.1.1     |
|5.6.0         |   5.6.0.4     |
|5.5.0         |   5.5.0.1     |
|5.4.1         |   5.4.1.1     |

### バージョン履歴
| バージョン        | 日付         | 更新内容                    |
|-----------------|--------------|----------------------------------|
|5.7.1.0          |2020/3/5    | - Facebook SDK 5.7.1 に対応<br>- プリロードされるバナー広告はクリックされない問題を解決します|
|5.6.1.1          |2020/2/10   | - Facebook SDK 5.6.1 に対応<br>- 調整モード、テストモードの設定をサポートします，[初期化](./init.md)を参考してください|
|5.6.0.4          |2019/11/26  |HeaderBidding をサポート|
|5.6.0.0          |2019/11/13  |Facebook SDK 5.6.0 に対応              |
|5.5.0.1          |2019/10/3   |Facebook SDK 5.5.0 に対応              |
|5.4.1.1          |2019/7/16   |動画リワード広告のクリックイベントが通知されない問題を修正|