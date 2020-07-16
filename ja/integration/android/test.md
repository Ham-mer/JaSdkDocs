# 広告表示テスト
ここでは、各広告ネットワークの広告の表示テストのための広告枠 ID 一覧を掲載します。各ネットワークの説明に従い SDK をインポート後にテスト用の広告枠 ID を設定し、正しく広告が表示されるか確認しましょう。

- アプリ ID<br>
    d13be96e-e172-4645-b761-4827a0ae8c0c

## AdLime のテスト

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 5502dfa5-6652-42fb-9e7e-215337799789 |
| バナー 300×250    | fbc50bd5-b44c-4144-bca1-89e52b6f7dba |
| インターステーシャル     | 5568ac9e-be1e-48d6-90f4-726d2f71bc94   |
| ネイティブ         | 5a28316a-0798-44d1-817e-119998c53643   |
| 動画リワード       | 9c9509b3-b4cf-4354-a515-1e754657ef6e   |
| MixView バナー 320x50| 7ca5421d-4524-4ab8-85e6-bf10fd4c2b6a  |
| MixView バナー 300×250| 1de5608f-aa0a-4626-854e-c387155aedf8 |
| MixView    ネイティブ      | 32bd14c7-c835-41aa-b6ad-31cfe7324236   |
| MixFullScreen バナー 320x50| dabbcc43-128f-450a-a50b-484ebae51eb6   |
| MixFullScreen バナー 300×250| 109d4dd9-4f7c-4226-a148-ff5f810edc41   |
| MixFullScreen ネイティブ   | 03deadef-72bc-4876-a260-5a10dfa34369   |
| MixFullScreen インターステーシャル    | d1ad5508-cf3b-4623-9662-87cff5049af4   |

## 広告ネットワークのテスト
AdLime では、複数の広告ネットワークを管理、配信する[メディエーション機能](./mediation.md)を提供しています。このガイドでは各広告ネットワークが正しく表示されるかを正しくテストするために、広告枠 ID を提供しています。導入予定のSDKを確認、それぞれの導入手順に従い必要な SDK を追加してください。追加後に各広告ネットワークの広告枠 ID を設定して、広告が正しく表示されるか確認しましょう。

### [AdGeneration](./mediation_adgeneration.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 848d76be-4295-43aa-a128-19327a5d95b9   |
| バナー 300×250    | 195db746-30e5-4c7c-b687-de278531ae03   |
| インターステーシャル     | 1df516af-a62f-49ba-9bc6-6ebf032e811e   |
| ネイティブ         | 57d08adf-1358-486e-887f-02a48d7d857a   |

### [AdMob](./mediation_admob.md)

AdMob 17.0.0 以降のバージョンにおいて、meta-data を設定する必要があります。
```java
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-3940256099942544~3347511713"/>
```

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | ea6fe45b-c7a9-4dcd-aab8-89d8fdb4a93c   |
| バナー 300×250    | 1a15e85a-f50f-4d11-99ca-31b14dc97532   |
| インターステーシャル     | 49d0e6fa-e527-42f0-9b1b-770a5b333beb   |
| ネイティブ 静止画 | 304af8d5-8f88-4b3c-a783-aaf3d7d88db4   |
| ネイティブ 動画   | 247eda76-066d-46e4-9847-9089a945b75c  |
| 動画リワード       | 199ad96c-2ab1-43f3-8f7a-c00c99b5f224   |
| MixView バナー 320x50| cb28be5f-89ac-47e8-b8be-cbd495f225ec  |
| MixView バナー 300×250| 3a432270-3d78-4dca-ab76-ae007e2c974b  |
| MixView ネイティブ 静止画 | 71b95bbb-cc6c-48cf-810b-b7a532d1fdfc   |
| MixView ネイティブ 動画   | ef318710-2dbd-484a-93f6-1284b9ab98d9   |
| MixFullScreen バナー 320x50| 284050a4-865a-42ab-8e60-1a0f72c00fd3   |
| MixFullScreen バナー 300×250| ff33ce05-4a98-416c-88ff-d7cdf4e39ecb   |
| MixFullScreen ネイティブ 静止画 | 30860251-6c32-4d32-8c01-1fc828d92e73   |
| MixFullScreen ネイティブ 動画   | 79527c54-d2c8-4dc9-9295-7fb05cbbaa62   |
| MixFullScreen インターステーシャル    | 6b8ed887-75fb-432b-b240-13d701e54a31   |  

### [AppLovin](./mediation_applovin.md)

AndroidManifest.xml に SDK key を設定してください。
```java
<meta-data
    android:name="applovin.sdk.key"
    android:value="qTA2uuo2zUQLXHPGDPooTJLZprJIiR6HDcHEgaJq24ErXVwNTqt73MlOFEssXOL9Q1RIFDlR1136N8uhTlthKc" />
```

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 613c06f7-f48d-4c69-aba7-d453513d7007   |
| バナー 300×250    | da369915-d1b6-4394-916f-b34090def98b   |
| インターステーシャル     | 63d5dbd8-b9ab-4a7a-86d9-406826953da8   |
| ネイティブ         | 5816ab14-be45-4fb4-a1c0-510d7395a1c5   |
| 動画リワード       | b03099ed-ac2b-43d7-82ff-1a7b19d17de9   |
| MixView バナー 320x50| 280037d0-c206-410b-8dda-06a9da3b09b1  |
| MixView バナー 300×250| 378d85af-da2a-4e04-9d6d-35e574b7f596 |
| MixView ネイティブ  | 82c85014-dd96-4660-9260-b03ccd27bb89   |
| MixFullScreen バナー 320x50| 086f40e9-dcf7-44d8-ae0e-ae45dd080727   |
| MixFullScreen バナー 300×250| 02d30bab-0c4a-4847-8d40-405125470953   |
| MixFullScreen ネイティブ   | 7a824b84-f39c-4e06-a649-4290c1214374   |
| MixFullScreen インターステーシャル    | 8bf8de24-972b-4c25-b8ec-38c48baabb6c   |  

### [Criteo](./mediation_criteo.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | a57a4c37-bc7d-435b-921a-ed73f4413c86   |
| バナー 300×250    | 51a2f6cd-bd97-40c9-9832-b7e9a01a9ac7   |
| インターステーシャル     | 28643335-0fef-4268-a1c5-06ecc956a67f   |
| MixView バナー 320x50| e21c1352-cc5d-4fc6-8d1d-1ed88a1feaf6  |
| MixView バナー 300×250| ca6ea99d-47ed-4313-8740-10de42c570ce |
| MixFullScreen  バナー 320x50| 0cb8cf8f-1703-42c2-a11d-2a65315029f3   |
| MixFullScreen  バナー 300×250| 419c7160-8f8f-47ac-a66c-0d6d59b5a895   |
| MixFullScreen インターステーシャル    | e05757d2-3070-4dc8-be11-22a3bd0e0ca1   |  

### [DFP](./mediation_dfp.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 617e49c3-4d6e-4b69-806e-776873fa0c72   |
| バナー 300×250    | 28faadf5-cd14-437f-90bf-b48810d3e570   |
| インターステーシャル   | d6426b6e-9e87-4e73-9634-2fae137fd128   |
| ネイティブ 静止画   | ee27ab16-772d-43e1-acbb-96e87ee0f0c4   |
| ネイティブ 動画     | c05aa109-7695-49cb-942f-7ced1e873a9f   |
| 動画リワード       | ebe8be54-0e95-49ff-9faf-aba17c43b548   |
| MixView バナー 320x50| c504e99c-1ac0-4a9a-9c35-9cdef0e53b65  |
| MixView バナー 300×250| 3cb9fc81-ceab-4e5a-aac2-4c37bf571877 |
| MixView ネイティブ 静止画 | adf15f3d-84c6-459d-8942-a8239cd6db9c   |
| MixView ネイティブ 動画   | 6f9c7cc5-1990-4807-8c0d-0ac929b0b10b   |
| MixFullScreen バナー 320x50| 139020c6-c083-4d73-8b58-dc93def552dc   |
| MixFullScreen バナー 300×250| 72d2c5c6-0247-4da6-987d-323cb72bfa97   |
| MixFullScreen ネイティブ 静止画 | c8ee76c1-58d8-44f9-a54e-0a62cdd8fee6   |
| MixFullScreen ネイティブ 動画   | 92b4427e-f7fb-4b31-a9e6-08e1aee54f97   |
| MixFullScreen インターステーシャル | 747a72c2-1b34-4ddd-9cb4-61026ca2b8a9   |  

### [Facebook](./mediation_facebook.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 5ccb63da-90a8-4a15-80dc-64cfc279a2a2   |
| バナー 300×250    | 543015b0-bd61-4604-9b01-ee6f90003d2d   |
| インターステーシャル  | e6467841-5c74-4fc7-8582-81b44e649dd7   |
| ネイティブバナー広告 | ea6a1cf7-d7a4-489b-bffa-4c4d3f13cce3   |
| ネイティブ 静止画   | 00ea7ad6-bb0a-442c-af30-023f08729fec   |
| ネイティブ 動画     | bfdc34eb-a440-4073-8e0e-8f13352389f1   |
| 動画リワード       | b90cada3-707e-47cc-9875-a39953824090   |
| MixView バナー 320x50| aa927a72-4487-4185-882c-330f6457803a  |
| MixView バナー 300×250| e8b17248-46a8-4410-871b-4347b090d85f |
| MixView ネイティブバナー広告 | 83b94453-dd23-4de9-907d-65f4e7454bde |
| MixView ネイティブ 静止画 | d5274ee3-942b-4053-b65b-3ce68820621f   |
| MixView ネイティブ 動画   | b02a79ee-1529-4ba7-b7d0-d00303b2979a   |
| MixFullScreen バナー 320x50| 5d97fe06-14b3-4338-9a49-77dafa3d2123   |
| MixFullScreen バナー 300×250| 54eab1cb-ff5e-4f8c-9dbf-ca75c6e9bc9e   |
| MixFullScreen ネイティブバナー広告 | 7bbac0a4-ed00-4ff5-a5cf-c802834635eb |
| MixFullScreen ネイティブ 静止画 | 9ae699c9-f97e-44af-a0c2-b52d286c941d   |
| MixFullScreen ネイティブ 動画   | 30c681c3-74c6-4f6a-b44c-dd511844a07a   |
| MixFullScreen インターステーシャル  | c88fa743-3053-42d6-8d89-7efd8c777066   |    

### [Five](./mediation_five.md)

| 広告タイプ          | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50       | 31f2791d-fd12-4189-b64d-6de29693cb93   |
| バナー 300×250      | 241b5c9b-fe13-4fea-8ea5-62e18b696bc8   |
| インターステーシャル            | e6ea6e49-9c23-403b-ad3d-20cca1d5259c   |
| 動画リワード          | eea5bbe3-213e-40c2-93e9-93ead11b22c7   |
| MixView バナー 320x50| 7415e5c9-3d27-42cd-b123-4f3d2e5632ff  |
| MixView バナー 300×250| 9fe14b4c-f040-4eeb-b5e5-a4c9bacd9128 |
| MixFullScreen バナー 320x50| fbc2ac52-a2b8-4efa-910b-ce4500c1f75f   |
| MixFullScreen バナー 300×250| ff281bc3-6293-4f0c-a0f8-ccb3a78983df   |
| MixFullScreen インターステーシャル    | c357a361-d24e-4540-a389-aaa4bc845720   |  

### [i-mobile](./mediation_imobile.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 8c7b02a2-f9ba-43c5-afcf-c3ef256d6af1   |
| バナー 320×100     | 30facee8-622a-4162-9668-6fddecdeeab6   |
| バナー 300×250    | d6e455e1-48c4-4b0b-a33f-09c13a2ead0e  |
| インターステーシャル     | 5eea5825-bc9d-4020-8e07-cfb0f62491ac  |
| ネイティブ 静止画 | f9304209-9280-4c59-84a1-37c1ae16bc97   |
| MixView ネイティブ 静止画 | ec15e1d4-3f59-4361-97a0-9a77e7a17a2e   |

### [Maio](./mediation_maio.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| インターステーシャル     | baa759a1-06f3-42ef-86b2-0631b01fe47f   |
| 動画リワード       | 0e0e2ce7-d255-4ea1-975a-754fed3671c4   |

### [MoPub](./mediation_mopub.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | fa4ed654-95f9-4135-98e0-88001498836e   |
| バナー 300×250    | 30df9771-c372-45e1-9172-d71dedd9eaa7   |
| インターステーシャル     | a71f18ce-7d40-4a2f-b246-d1b60806a435   |
| ネイティブ 静止画  | 96a02419-e2cb-4667-b506-3a15f7702439   |
| 動画リワード       | 95b71076-87f7-4dcd-8b02-c19707f37083   |
| MixView バナー 320x50| a1253827-5930-45f3-b82c-3f55469204da  |
| MixView バナー 300×250| 69c3a864-2b58-4f1c-ba2a-566614b9616c |
| MixView ネイティブ 静止画 | 769594f5-f0b5-4f89-9e8c-e02a9fdff145   |
| MixFullScreen バナー 320x50| c8b01909-1793-4e54-bddf-aaa91f7c06e5   |
| MixFullScreen バナー 300×250| 0455426b-8734-4852-8c5d-5092efcfd61c   |
| MixFullScreen ネイティブ   | 0f82f948-a9d2-4f96-8821-2d12d4cce637   |
| MixFullScreen インターステーシャル    | 81e4b065-8b3d-4718-92a3-80d42f5ed73e   |  

### [Nend](./mediation_nend.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320x50     | 25ba41df-c69b-45f4-a1fd-d25221d3e9d4   |
| バナー 300×250    | e6c9e244-d2fb-4579-bd38-f04e0fdd1175   |
| インターステーシャル  | 9d499190-911a-4b1a-8734-23c2de9a9613   |
| インターステーシャル 全画面 | 5b7cc754-74c0-49ba-bcae-1a43df14fa8a |
| インターステーシャル 動画 | 8a6dab7a-1618-44b3-9f92-a4014f89c55e |
| ネイティブ 静止画 | d7a01bb6-745f-4dab-a86d-fe856a23abc9   |
| ネイティブ 動画 | 81d6e364-6d44-46c2-bbc9-539dbdc3bbfa   |
| 動画リワード       | d794a8f0-b5a3-4bc2-9530-f40893a3f851   |
| MixView バナー 320x50| e870107d-22ba-4f52-aefd-0c51fe360976  |
| MixView バナー 300×250| 61e9945c-519b-4083-9bae-06d5a0b0334f |
| MixView ネイティブ 静止画 | c862374a-587c-4030-a27b-422179d9fc50   |
| MixView ネイティブ 動画   | e17a81e5-213d-4671-9eeb-ef6bd6d46d52   |
| MixFullScreen バナー 320x50| 57872b7a-b4ae-4bd4-b855-ca40571af90b   |
| MixFullScreen バナー 300×250| d6c43bd7-7b7b-4923-8672-3b1f300d2cd1   |
| MixFullScreen ネイティブ 静止画 | 2f5cbe1c-959e-418c-a15d-f31412533d8c   |
| MixFullScreen ネイティブ 動画   | 90304fa0-6694-49fc-8092-d6ee0e7a881d   |
| MixFullScreen インターステーシャル | 85a5e1ce-34df-4b0b-adef-98d725a9c913   |
| MixFullScreen インターステーシャル 全画面 | 6376dd5f-d08f-460a-afbe-559ee9d06f8c |
| MixFullScreen インターステーシャル 動画 | 8465b93f-3f17-4a37-9fad-8fdbb778f2c3 |

### [Pangle](./mediation_pangle.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| ネイティブ         | e554d99d-69e3-4156-aaae-2bf743c0f301 |
| インターステーシャル | 2207389f-5fe4-4dca-9a8c-85c8897991fe   |
| 動画リワード       | 3871e42d-0e5d-4bec-bfe9-de7d4ec7d6fb   |
| MixView ネイティブ | 63b508cc-2fe9-43a9-a81e-557b6a1a92e9 |
| MixFullScreen ネイティブ   | 07b744ff-9bd6-4dd9-a5bc-b8464a55b025 |