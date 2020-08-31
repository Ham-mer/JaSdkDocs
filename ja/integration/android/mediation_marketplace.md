# AdLimeMarketplace ドキュメント

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    // AdLimeMarketplace
    implementation "com.access_company.adlime:mediation_marketplace:1.11.5.0"
    implementation "com.access_company.adlime:marketplace:1.11.5"
}
```

## AndroidManifest は一致
```java
<!-- AdLimeMarketplace は WRITE_EXTERNAL_STORAGE という権限を持っています。もし削除したい場合に、下記のコードを使ってください -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" tools:node="remove" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" tools:node="remove" />
```

## 広告フォーマット

### 利用可能なフォーマット
|ネットワーク |バナー |インタラクション |動画リワード |ネイティブ |
|:---------:|:----:|:------------:|:---------:|:--------:|
| AdLimeMarketplace | ◯ |         |           |          |

### バナーサイズ
|ネットワーク | 320×50 | 300×250 | 320×100 | 468×60 | 728×90 |
|:---------:|:------:|:-------:|:-------:|:------:|:------:|
| AdLimeMarketplace | ◯ | ◯    |         |        |        |

## バージョン情報
### 1.11.5
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 1.11.5.0   | 2020/7/27  | AdLimeMarketplace 1.11.5 に対応|

### 1.11.3
| バージョン   | 日付       | 更新情報                          |
|------------|------------|---------------------------------|
| 1.11.3.0   | 2020/7/21  | AdLimeMarketplace 1.11.3 に対応|