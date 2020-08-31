# Pangle
-  [Pangle  公式サイト&開発者ガイド](https://ad.toutiao.com/union/media/login/)

## 前提条件
- Android API レベル 14 以上

## 依存関係の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。

```java
dependencies {
    implementation "com.access_company.adlime:mediation_pangle:3.1.0.1.0"
    implementation "com.access_company.adlime:pangle_open_ad_sdk:3.1.0.1"
}
```


## ネットワークセキュリティ構成ファイルを追加する
res/xml ディレクトリに以下の記述で network_security_config.xml を追加する。

```java
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```


## ネットワークセキュリティ構成ファイルを AndroidManifest に設定する
```java
<!-- ユーザーの同意によって位置情報を取得すると、広告のターゲティング精度が向上できる -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

<application android:networkSecurityConfig="@xml/network_security_config"/>
```

すでに application タグに android:networkSecurityConfig が存在する場合は、network_security_config.xml の内容を、指定されている XML ファイルに統合してください。

**Pangle SDK は位置情報を取得しなくても広告を表示可能。位置情報が取得可能な場合には、ターゲティング精確の高い広告配信ができる。**

## リソース難読化
アプリがリソースに対して難読化を行う際（例えば、andResGuard を使う時）、Pangle のリソースに対して難読化を行わないでください。リソースが見つからない場合、アプリがクラッシュする可能性もあります。詳しくは[Pangle リソースリスト](./mediation/config/pangle_whitelist.md)をご参照ください。

## 注意
- 動画リワード広告を使用する場合、RewardedVideoAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること
- インタースティシャル広告を使用する場合、InterstitialAd コンストラクトの引数に、Activity 型を指定するか、もしくは show(activity) で広告を表示すること

## 広告フォーマット
### 利用可能な広告フォーマット

|ネットワーク|バナー|インタースティシャル|動画リワード|ネイティブ|
|:------: |:---:|:----------:|:------:|:----:|
| Pangle |      | ◯          | ◯      | ◯    |

### バージョン情報
下記の Pangle の情報が必要となります。  
- App ID
- Code ID

## バージョン情報
### 3.1.0.1
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 3.1.0.1.0  | 2020/7/31  | - Pangle SDK 3.1.0.1 に対応：プライバシー機能の強化；Https 証明書の検証問題を修正する；GDPR コンプライアンスの強化，SDK 安定性の向上<br><br>- TikTokGlobalConfig：setCustomController() を削除します<br><br>- pangle_network_security_config.xml ファイルを更新します<br><br>- リソース難読化設定における [Pangle リソースリスト](./mediation/config/pangle_whitelist.md)を更新します|

### 2.9.0.3
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 2.9.0.3.0  | 2020/6/18  | - Pangle SDK 2.9.0.3 に対応：バグの修正<br><br>[リソース難読化](#リソース難読化)を追加|

### 2.9.0.1
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 2.9.0.1.2  | 2020/3/31  | - Pangle SDK 2.9.0.1 に対応<br>- ネイティブ広告をサポート|

### 2.1.5.0
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 2.1.5.0.0  | 2020/2/17  | - Pangle SDK 2.1.5.0 に対応<br>- pangle_network_security_config.xml の内容を更新 <br>- GDRPをサポート|

### 2.1.3.0
|バージョン   | 日付        | 更新内容                        |
|------------|------------|-------------------------------|
| 2.1.3.0.2  | 2020/2/10  | - android:networkSecurityConfig 設置の追加<br>- デバッグモードをサポート。[初期化](./init.md)を参考してください|
| 2.1.3.0.0  | 2020/1/19  | Pangle SDK 2.1.3.0 に対応 |
