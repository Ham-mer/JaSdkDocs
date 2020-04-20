# Criteo 導入ドキュメント
- [ Criteo Webサイト](https://www.criteo.com/)
- [ Criteo 開発者ガイド](https://publisherdocs.criteotilt.com/sdk-android/3.0/inhouseauction/)

## 依存関係の導入
アプリケーションレベルの build.gradle に下記の依存関係を追加します。

```java
implementation "com.access_company.adlime:mediation_criteo:3.1.0.3"
implementation "com.access_company.adlime:criteopublishersdk:3.1.0"
implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
implementation "com.google.android.gms:play-services-base:16.1.0"
```

## 広告フォーマット

### 利用可能なフォーマット
|ネットワーク |バナー  |インタースティシャル  |動画リワード |ネイティブ  |
|:-------|:-----:|:-----:|:-------:|:-----:|
|  Criteo   | ◯      | ◯    |     |        |

### バナーサイズ
|ネットワーク   |320×50   |300×250   |320×100   |468×60   |728×90   |スマート   |
|:-------:|:------:|:-------:|:-------:|:------:|:------:|:-----:|
|   Criteo    |  ◯      |     ◯     |   ◯       |  ◯       |  ◯       |        |

### 設定情報
下記の Criteo の情報が必要になります。  
- Publisher ID

## バージョン情報

### リリースバージョン
|  Criteo バージョン | アダプタ バージョン |
|:----------|:-------------|
|  3.1.0    | 3.1.0.3      |
|  3.1.0    | 3.1.0.2      |
|  3.0.1    | 3.0.1.0      |
|  3.0.1    | 3.0.1.1      |
|  3.0.1    | 3.0.1.0      |

### バージョン履歴
| バージョン       | 日付      | 更新内容               |
|:--------------|------------|------------------------|
|   3.1.0.3     |  2019/11/5  | 外部のアプリに遷移する際に、広告を閉じるコールバックの追加|
|   3.1.0.2     |  2019/11/4  | バナーのコールバックの修正  |
|   3.1.0.0     |  2019/11/1  | Criteo SDK 3.1.0 に対応  |
|   3.0.1.1     |  2019/10/23 | 内部ロジックの改善   |
|   3.0.1.0     |  2019/9/5   | 初期バージョン            |
