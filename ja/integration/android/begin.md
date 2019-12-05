# スタートガイド
このガイドは、AdLime SDK で、Android アプリをマネタイズすることをご希望とする開発者様を対象としています。

アプリに、AdLime SDK を導入することは、広告を表示して収益を獲得するための第一歩です。 SDK を導入したら、広告フォーマット（ネイティブ広告や動画リワード広告など）を選択し、該当する手順に従ってください。

## 前提条件

1. Android Studio 1.0 以上
2. Android API レベル 14 以上
3. AdLime アカウントを作成し、アプリが登録済み

## AdLime SDK を導入する

アプリに AdLime SDK をインストールするには、JFrog の Bintray リポジトリを指す Gradle 依存関係を使用します。このリポジトリを使うには、アプリのプロジェクトレベルの build.gradle ファイルで、このリポジトリを参照する必要があります。ファイルを開き、 allprojects セクションを見つけ、以下を参考にリポジトリを指定します。

### プロジェクトレベルの build.gradle の例（抜粋）

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
次に、アプリレベルの build.gradle ファイルを開き、「dependencies」セクションを開きます。

### アプリレベルの build.gradle の例（抜粋）
現在広告SDKを導入する方法は二つあります。デベロッパーは状況に応じていずれかの方法を自由に選ぶことができます。

#### 方法一
デベロッパーはまずフレームSDKを導入してから、自分のニーズに応じて該当するメディエーションを導入します。メディエーションの導入方法についてはドキュメントをご参照ください。下記のリクエストを追加してください：
```
dependencies {
    implementation 'com.access_company.adlime:adlime:1.9.18'
}
```
この方法はお勧めです。

#### 方法二
この方法はAdMob・Facebook・DFP・ MoPub・TikTok・AppLovinという六つのメディエーションを統合します。デベロッパーは、上記の各メディエーションの導入に必要とされるリクエストを気にかける必要がなく、それぞれのメディエーション導入ドキュメントを閲覧する必要もありません。
```
dependencies {
    implementation 'com.access_company.adlime:adlime_all:1.7.9'
}
```
デベロッパーは、AndroidManifest.xmlに下記の情報を追加する必要があります：
```java
    <provider
        android:name="com.bytedance.sdk.openadsdk.multipro.TTMultiProvider"
        android:authorities="${applicationId}.TTMultiProvider"
        android:exported="false" />
    <meta-data
        android:name="applovin.sdk.key"
        android:value="${applovin_value}" />
```
ここの${applovin_value}はapplovinの申請を行う時のキーバリューです。導入しなかった場合、下記のフィールドをご記入ください： "qTA2uuo2zUQLXHPGDPooTJLZprJIiR6HDcHEgaJq24ErXVwNTqt73MlOFEssXOL9Q1RIFDlR1136
N8uhTlthKc"。 

上記の太字の行（ AdLime SDK の最新バージョンを読み込むように Gradle に指示する行）を追加してください。作業が終わったらファイルを保存し、 Gradle の同期を行います。

## 広告のフォーマットを選択する

これで AdLime SDK の導入が完了し、広告の実装ができるようになりました。 AdLime には、さまざまな広告フォーマットが用意されています。その中からアプリのユーザー エクスペリエンスに最適なフォーマットを選択できます。


### バナー

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-banner.png"  width="100px"  align=left />
バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージまたはテキスト広告です。この種の広告は、ユーザーがアプリを操作している間は画面に広告が残り、一定の時間が経過すると自動的に更新することが特徴です。モバイル広告を初めて掲載する場合は、まずバナー広告から始めることが最適です。
</div>

### インタースティシャル

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-interstitial.png" width="100px" align=left />
インタースティシャル広告とは、ユーザーが広告を閉じるまで、アプリの上にオーバーレイで表示されるフルスクリーン広告です。ゲームのステージが変わる合間や、1つのミッションが完了になった直後など、アプリの画面が切り替わるタイミングで使用するのに適しています。
</div>

### ネイティブ

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-native.png"  width="100px"  align=left />
ネイティブ広告とは、コンポーネントベースの広告フォーマットで、クリエイティブ（タイトルやキャッチコピーなど）をアプリに表示する方法を、自由にカスタマイズできます。フォント・色・その他クリエイティブの詳細設定を行い、コンテンツの邪魔にならないように広告を表示し、ユーザーエクスペリエンスを向上させることができます。
</div>

### 動画リワード

<div class="clearfix cust-image-text">
<img src="./../images/ad_icons/format-rewarded.png"  width="100px"  align=left />
動画リワード広告とは、ユーザーが動画を最後まで視聴することと引き換えに、アプリ内で報酬（インセンティブ）を獲得できるフルスクリーン動画広告です。
</div>



