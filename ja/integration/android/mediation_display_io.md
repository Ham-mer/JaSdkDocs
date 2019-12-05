# Display.IOドキュメント
- [Display.IO Webサイト](https://developers.display.io)
- [Display.IO 開発者ガイド](https://support.display.io/hc/en-us/categories/360001149554-Android)

## 前提条件
- Android API レベル 14 以上

## mavenリポジトリの導入
プロジェクトレベルの build.gradle に、下記のレポジトリを追加します。

```java
allprojects {
    repositories {
        // Display.IO
        maven { url "http://maven.display.io/" }
    }
}
```

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // please select one verson from follows:

    // version 3.3.0
    implementation "com.access_company.adlime:mediation_displayio:3.3.0.0"
    implementation "com.brandio.ads:sdk:3.3.0"

    // version 2.0.1.0
    implementation "com.access_company.adlime:mediation_displayio:2.0.1.0.0"
    implementation "io.display:android-sdk:2.0.1.0"
}
```

## 広告フォーマット

### 利用可能なフォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Display.IO | Y    | Y          |       |    |

### バナーサイズ
|ネットワーク     |320 × 50 |300 × 250 |320 × 100 |468 × 60 |728 × 90 |スマート |
|:----------:|:-----:|:------:|:------:|:-----:|:-----:|:----:|
| Display.IO |       | Y      |        |       |       |      |

### 設定情報
下記の Display.IO の情報が必要になります。   
- App ID  
- Placement ID

## バージョン情報

### リリースバージョン
| Display.IO バージョン| アダプタ バージョン|
|:-----------------|:--------------|
| 3.3.0            | 3.3.0.0       |
| 2.0.1.0          | 2.0.1.0.0      |




### バージョン履歴
| バージョン        |  日付          |  更新内容                |
|-------------|-----------------|---------------------|
| 3.3.0.0   |  2019-9-7      |Display.IO SDK 3.3.0 に対応     |
| 2.0.1.0.0   |  2019-4-20      |Display.IO SDK 2.0.1.0 に対応     |
