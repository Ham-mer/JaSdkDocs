# 初期化
広告を読み込む前に、AdLime アプリ ID で初期化を行います。この処理は1回だけ実行します。(アプリの起動時に実行することが望ましい)

## AdLime SDK の初期化

1. 初期化は Activity の onCreate メソッドで実行します。<br>
        - setGdprConsent メソッドを呼び出し、 GDPR を設定します。<br> 
        - AdLimeConfiguration インスタンスを作成し、アプリ ID を設定後、 最後に initialize メソッド で初期化します。

2. Activity のライフサイクル onBackPressed メソッドにおいて、SDK の onBackPressed メソッドを呼び出してください。**任意**

## サンプルコード
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
                                .addTestDevice("テストデバイス ID1") // 広告の表示テストを行う複数のデバイスの ID を設定する
                                .addTestDevice("テストデバイス ID2")
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
                            .addTestDevice("テストデバイス ID") // 広告の表示テストを行う複数のデバイスの ID を設定する
                            .build())
                    .addConfig(AppLovinBannerConfig.Builder()
                            .setAutoDestroy(true)
                            .build())
                    .addConfig(DFPGlobalConfig.Builder()
                            .addTestDevice("テストデバイス ID") // 広告の表示テストを行う複数のデバイスの ID を設定する
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

## テスト用の広告枠
Android の各広告フォーマットの、テスト用の広告ユニット ID は、以下の通りです。

テスト アプリ ID           : 14fac732-0853-4f1e-83a4-77db7915fc62

| 広告フォーマット          | テスト広告ユニット ID                 |
|:---------------------- |:------------------------------------- |
|バナー                   |e302ae32-d770-4635-9b2f-97fd024e059e   |
|インタースティシャル        |ecc5a7d7-872b-4c6c-a042-6b0b311ccc04   |
|ネイティブ                |444dd66b-af52-4fd1-9260-5559e7488432   |
|動画リワード               |cca19625-d829-4902-8164-1e75a0e5e6f5   |

## デモアプリ
各広告の実装サンプルについては、[デモアプリ](https://github.com/Ham-mer/AdLime-Android-Demo)を参考にしてださい。