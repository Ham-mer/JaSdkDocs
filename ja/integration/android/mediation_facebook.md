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
    implementation "com.access_company.adlime:mediation_facebook:6.2.0.0.alpha"
    implementation "com.facebook.android:audience-network-sdk:6.2.0"
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
### 6.2.0
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|6.2.0.0.alpha |2021/1/10   | - Facebook SDK 6.2.0 に対応<br>- インタースティシャルおよびネイティブカルーセル広告のデザインを改善します<br>- クラッシュの問題を修正しました |

### 5.7.1
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|5.7.1.0     |2020/3/5    | - Facebook SDK 5.7.1 に対応<br>- プリロードされたバナー広告がタップできない問題を修正 |

### 5.6.1
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|5.6.1.1     |2020/2/10   | - Facebook SDK 5.6.1 に対応<br>- テストモード、デバッグモードをサポート；[初期化](./init.md)を参考してください |

### 5.6.0
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|5.6.0.4     |2019/11/26  |HeaderBidding をサポート |
|5.6.0.0     |2019/11/13  |Facebook SDK 5.6.0 に対応 |

### 5.5.0
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|5.5.0.1     |2019/10/3   |Facebook SDK 5.5.0 に対応 |

### 5.4.1
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
|5.4.1.1     |2019/7/16   |動画リワード広告のクリックイベントが通知されない問題を修正 |