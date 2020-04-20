# AdGenerationドキュメント
- [AdGeneration Webサイト](http://out.easycounter.com/external/ad-generation.jp)
- [AdGeneration 開発者ガイド](https://github.com/AdGeneration/ADG-Android-SDK)

## 前提条件
- Android API レベル 14 以上

## mavenリポジトリの導入
プロジェクトレベルの build.gradle に、下記のレポジトリを追加します。

```java
allprojects {
    repositories {
        // AdGeneration
        maven { url 'https://adgeneration.github.io/ADG-Android-SDK/repository' }
    }
}
```

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
  // AdGeneration
  implementation "com.access_company.adlime:mediation_adgeneration:2.16.1.2"
  implementation "com.socdm.d.adgeneration:adg:2.16.1"
  implementation "com.google.android.gms:play-services-ads-identifier:16.0.0"
  implementation "com.google.android.gms:play-services-ads:17.1.2"
}
```

## AndroidManifestの設定
```java
// ハードウェアアクセラレーションを起動する
<application
  android:hardwareAccelerated="true">
   (省略) 
</application>
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インターステーシャル|動画リワード|ネイティブ|
|:------------:|:---:|:----------:|:------:|:----:|
| AdGeneration | ◯    | ◯          |       | ◯   |

### バナーサイズ
|ネットワーク       |320×50 |300×250 |320×100 |468×60 |728×90 |スマート |
|:------------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| AdGeneration | ◯     | ◯      | ◯      |       | ◯     | ◯    |

### 設定情報
下記の AdGeneration の情報が必要になります。
- Location ID  

## バージョン情報

### リリースバージョン
| AdGeneration バージョン | アダプタ バージョン |
|:---------------------|:-----------------|
| 2.16.1           | 2.16.1.2      |
| 2.15.1           | 2.15.1.3      |
| 2.15.1           | 2.15.1.2     |
| 2.15.1           | 2.15.1.1     |

### バージョン履歴
| バージョン    | 日付         | 更新内容                |
|-------------|--------------|-------------------------------|
| 2.16.1.2    | 2020/2/10    | テストモードをサポートします，[初期化](./init.md)を参考してください |
| 2.16.1.1    | 2019/11/1    | AdGeneration SDK 2.16.1 に対応           |
| 2.15.1.3    | 2019/10/23   |  内部のロジックを改善する          |
| 2.15.1.2    | 2019/7/16    | SDKの最適化                  |
| 2.15.1.1    | 2019/7/16    | バナー表示の最適化          |
