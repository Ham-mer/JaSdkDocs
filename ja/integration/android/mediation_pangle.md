# Pangle
-  [Pangle  公式サイト&開発者ガイド](https://ad.toutiao.com/union/media/login/)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    implementation "com.access_company.adlime:mediation_pangle:2.1.5.0.0"
    implementation "com.access_company.adlime:pangle_open_ad_sdk:2.1.5.0"
}
```

## AndroidManifest の設定
```java
<!-- 追加，同意を貰って位置情報を取得すると、Pangle はこの権限を基づいて精確にターゲットできる告 -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

<application android:networkSecurityConfig="@xml/pangle_network_security_config"/>
```

すでに application タグに android:networkSecurityConfig が存在する場合は、pangle_network_security_config.xml の内容を、指定されている XML ファイルに統合してください。

**Pangle SDKは上記の権限を強制取得ではない、取得しなくても広告をリクエストできる。上記の権限を取得してから Pangle はもっと精確にターゲットしてユーザ体験改善してecpmを高める。**

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること

## 広告フォーマット
### 利用可能な広告フォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Pangle |      |  ◯        | ◯      |     |

### バージョン情報
下記の Pangle の情報が必要となります。  
- App ID
- Code ID

## バージョン情報

### リリースバージョン
| Pangle バージョン  | アダプタ バージョン|
|:-----------------|:-----------------|
|2.1.5.0           |2.1.5.0.0         |
|2.1.3.0           |2.1.3.0.2         |

### 更新履歴
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 2.1.5.0.0  | 2020/2/17  | - Pangle SDK 2.1.5.0 に対応<br>- pangle_network_security_config.xml の内容を更新します<br>- GDRPをサポートします |
| 2.1.3.0.2  | 2020/2/10  | - android:networkSecurityConfig設置の追加<br>- 調整モードをサポートします，[初期化](./init.md)を参考してください |
| 2.1.3.0.0  | 2020/1/19  | Pangle SDK 2.1.3.0 に対応 |
