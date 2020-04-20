# DU Ad Platformドキュメント
- [DU Ad Platform Webサイト](http://ad.duapps.com)
- [DU Ad Platform 開発者ガイド](http://ad.duapps.com/zh_CN/sdk)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // DU Ad Platform
    implementation "com.access_company.adlime:mediation_duadplatform:1.2.2.3"
    // AdLime のみを使用する場合、duadplatform_hw 、もしくは duadplatform_cw をインポートする
    implementation "com.access_company.adlime:duadplatform_cw:1.2.2"
    // implementation "com.access_company.adlime:duadplatform_hw:1.2.2"
}
```

## AndroidManifest の設定
[DU_APP_LICENSE] に DU Ad Platform に登録したアプリの App ID を差し替えてください。
```java
<meta-data
    android:name="app_license"
    android:value="[DU_APP_LICENSE]" />
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| DU Ad Platform | ◯   | ◯         |       | ◯  |

### バナーサイズ
|ネットワーク         |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:--------------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| DU Ad Platform | ◯     |        |        |       |       |      |

### 設定情報
下記の DU Ad Platform の情報が必要になります。 
- Placement ID

## バージョン情報

### リリースバージョン
| DU Ad Platform バージョン | アダプタ バージョン|
|:-----------------|:--------------|
| 1.2.2              | 1.2.2.3       |
| 1.2.2              | 1.2.2.1       |

### バージョン履歴
| バージョン            | 日付              | 更新内容              |
|-----------------|--------------------|---------------------|
| 1.2.2.3    |  2020/2/10    |テストモードをサポートします，[初期化](./init.md)を参考してください |
| 1.2.2.2    |  2019/8/19    |ネイティブ広告のクリックエリアのカスタマイズに対応|
| 1.2.2.1    |  2019/5/4     |AndroidManifest.xml 設定の簡素化  |
