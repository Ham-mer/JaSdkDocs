# AdLime SDK の導入
AdLime は "AdLime SDK" と "AdLime ALL SDK" の2種類の SDK を提供しています。これらの SDK の違いは主要なアドネットワークをデフォルトで提供しているかどうかです。

広告ネットワークをカスタムに設定することを希望する場合は "AdLime SDK" を導入することをおすすめします。"AdLime SDK" を導入後は[メディエーション](./mediation.md)のガイドを参考にしてご希望のアドネットワークを追加してください。 


"AdLime SDK" は AdLimeSdk と AdMob・DFP・FaceBook・Mopub・AppLovin・TikTok の広告ネットワークを標準でサポートしています。これらのアドネットワークの導入を希望する場合は、この SDK を組み込むことも選択肢の一つです。"AdLimeSdk_All" の SDK を導入することで、各広告ネットワークごとに必要な SDK を追加する手順などををスキップすることが可能です。


アプリに AdLime SDK をインストールするには、アプリレベルの build.gradle に依存関係を記述します。このリポジトリを使うには、アプリのプロジェクトレベルの build.gradle ファイルで、このリポジトリを参照する必要があります。ファイルを開き、 allprojects セクションを見つけ、以下を参考にリポジトリを指定します。


## 前提条件
1. Android Studio 1.0 以上
2. Android API レベル 14 以上
3. AdLime アカウントを作成し、アプリが登録済み


## AdLime SDK のリポジトリを指定
プロジェクトレベルの build.gradle ファイルに、AdLime のリポジトリを指定します。

```
allprojects {
    repositories {
        // AdLime
        maven { url "https://dl.bintray.com/adlime/AdLime" }

        google()
        jcenter()
        maven { url "https://maven.google.com/"}
    }
}
```

## AdLime SDK の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。
```
dependencies {
    implementation 'com.access_company.adlime:adlime:1.9.28'
}
```

## AdLime All SDK の導入
アプリケーションレベルの build.gradle に、下記の依存関係を追加します。
```
dependencies {
    implementation 'com.access_company.adlime:adlime_all:1.7.9'
}
```
## マニフェストファイルへの記述
マニフェストファイル AndroidManifest.xml に必要な情報を記述します。
```java
    <meta-data
        android:name="applovin.sdk.key"
        android:value="${applovin_value}" />
```
${applovin_value} は Applovin の SDK key です。今回は下記の値を設定します。 **"qTA2uuo2zUQLXHPGDPooTJLZprJIiR6HDcHEgaJq24ErXVwNTqt73MlOFEssXOL9Q1RIFDlR1136
N8uhTlthKc"**

作業完了後に、Gradle の同期を行います。

## 初期化
広告を読み込む前に、AdLime の 'appId' メソッドを呼び出し、AdLime SDK 初期化します。 アプリ ID で初期化を行います。この初期化の処理はできるだけ早く実行する必要があり、アプリ起動時に実行することを強く推奨します。また、初期化は1回だけ実行してください。

### AdLime SDK の初期化

1. 初期化は Activity の onCreate メソッドで実行します。<br>
        - setGdprConsent メソッドを呼び出し、 GDPR を設定します。<br> 
        - AdLimeConfiguration インスタンスを作成し、アプリ ID を設定後、 最後に initialize メソッド で初期化します。

2. Activity のライフサイクル onBackPressed メソッドにおいて、SDK の onBackPressed メソッドを呼び出してください。**任意**

### サンプルコード
アクティビティで `initialize()' メソッドを実行し、AdLime SDK を初期化するサンプルです。

:::: tabs

::: tab Java

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    AdLime.getDefault().setGdprConsent(true);

    // AdLime SDKの設定を行う
    AdLime.getDefault().setGlobalNetworkConfigs(
                NetworkConfigs.Builder()
                        .addConfig(DFPGlobalConfig.Builder()
                                .addTestDevice("テストデバイス ID 1") // 広告の表示テストを行う複数のデバイスの ID を設定する
                                .addTestDevice("テストデバイス ID 2")
                                .build())
                        .addConfig(...)
                        .build());

    AdLime.getDefault().setLogEnable(true);

    AdLime.getDefault().init(this, "YOUR APP ID");
    ...
}
...

```

:::

::: tab Kotlin

```kotlin
    ...
    AdLime.getDefault().setGdprConsent(true)

    // AdLime SDKの設定を行う
    AdLime.getDefault().setGlobalNetworkConfigs(
                NetworkConfigs.Builder()
                    .addConfig(AdMobGlobalConfig.Builder()
                            .addTestDevice("テストデバイス ID 1") // 広告の表示テストを行う複数のデバイスの ID を設定する
                            .build())
                    .addConfig(AppLovinBannerConfig.Builder()
                            .setAutoDestroy(true)
                            .build())
                    .addConfig(DFPGlobalConfig.Builder()
                            .addTestDevice("テストデバイス ID 2") // 広告の表示テストを行う複数のデバイスの ID を設定する
                            .build()
                    ).addConfig(TikTokGlobalConfig.Builder()
                            .setIsDebug(true)
                            .setAllowShowNotify(true)
                            .build()
                    ).build()
            )

    AdLime.getDefault().init(applicationContext, "YOUR APP ID")
    //  以下はデバック時に設定する
    AdLime.getDefault().setTestMode(true)
    AdLime.getDefault().setLogEnable(true)
    ...
```

:::

::::

*** メディエーション時に Chartboost を使用する場合、Chartboost の広告を表示するすべての Activity に、下記のコードを追加する必要があります。***

:::: tabs

::: tab Java

```java
@Override
public void onBackPressed() {
    super.onBackPressed();
    ...
    AdLime.getDefault().onBackPressed(this);
    ...
}
```
:::

::: tab Kotlin

```kotlin
override fun onBackPressed() {
    super.onBackPressed()
    ...
    AdLime.getDefault().onBackPressed(this)
    ...
}
```

:::

::::


## SDK の実装サンプル
各広告の実装サンプルについては、[デモアプリ](https://github.com/Ham-mer/AdLime-Android-Demo)を参考にしてださい。

## 次へのステップ
- 事前に導入予定の広告ネットワークが決定している場合は[メディエーション機能の導入](./mediation.md)を確認し、各広告ネットワークごとに必要な SDK の導入手順に従ってください。
- 広告ネットワークを選択せず、広告を表示したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、Android アプリに実装しましょう。
