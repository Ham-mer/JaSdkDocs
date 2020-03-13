# 広告表示テスト
ここでは、各広告ネットワークの広告の表示テストのための広告枠 ID 一覧を掲載します。各ネットワークの説明に従い SDK をインポート後にテスト用の広告枠 ID を設定し、正しく広告が表示されるかを確認しましょう。

- アプリ ID<br>
    85f1d986-88e3-42f5-bd55-ffedea562215

## AdLime のテスト  

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50    | 52040363-01ed-44c3-b204-154e28cd0a4d   |
| バナー 300 × 250   | 573c18f4-7472-4987-b718-c124b154675f   |
| インタースティシャル      | 03e88f50-f414-41dd-ba19-3702fd360b4c   |
| ネイティブ         | d47cd3c3-b8a7-4902-871a-2a8ca5657626   |
| 動画リワード       | 8ef45a9e-74cf-4fa6-84d8-3c07fdedc0c7   |
| mixView  バナー 320 × 50| 59445d92-28af-41b1-9a3f-7c2a192a3bda   |
| mixView  バナー 300 * 250| 50d1f13e-b076-4578-9500-bd8584881706   |
| mixView  ネイティブ      | 1c4cf101-42f7-450a-b4cc-89a46e0deffd   |
| mixFullScreen バナー 320 * 50| c9d0819a-deef-4bd2-b038-b8686ffd82be   |
| mixFullScreen バナー 300 * 250| 00309e32-186a-46cd-bdd2-010636c73f69   |
| mixFullScreen ネイティブ   | e624f60a-f075-4814-9736-fa2f5c57a90c   |
| mixFullScreen  インタースティシャル | 9094b418-c345-44b9-b5dc-919dbd06b723   |

## 広告ネットワークのテスト
AdLime では、複数の広告ネットワークを管理、配信する[メディエーション機能](./mediation.md)を提供しています。このガイドでは各広告ネットワークが正しく表示されるかを正しくテストするために、広告枠 ID を提供しています。導入予定のSDKを確認、それぞれの導入手順に従い必要な SDK を追加してください。その後に各広告ネットワークの広告枠 ID を設定して、広告が正しく表示されるか確認しましょう。

### [AdColony](./mediation_adcolony.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | d54e608b-e2d7-44ae-aa88-9515d6f8ea9d   |
| インタースティシャル     | bbbffc33-7840-42e4-ab7f-68318385d371   |
| 動画リワード       | cb9e32b5-d21b-443e-a70b-3fd6015e1671   |

### [AdGeneration](./mediation_adgeneration.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | 65d10821-059d-49ad-92d0-08097e5139fb   |
| バナー 300 × 250    | cb846d08-124b-4469-89f9-bac25abd8f9d   |
| インタースティシャル     | e123cd5a-5c7f-40ba-9ba9-49afb404b2a8   |
| ネイティブ         | d1130de7-e972-49b3-8395-2f2f868ae63c   |

### [AdMob](mediation_admob.md)

Info.plist を ソースコードとして開いて編集します。
```objectivec
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-3940256099942544~1458002511</string>
```

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | 4c237306-12c5-4630-8abf-21f81013e4a9   |
| バナー 300 × 250    | e1c9202a-490c-4a82-badc-b996be3e9958   |
| インタースティシャル     | 678a54de-746e-488a-b866-dac81d4eef89   |
| ネイティブ         | f0d18ed5-1d72-4d3e-ba7e-87fec9081cd4   |
| 動画リワード       | ff519879-da39-4223-86aa-e31592f26f09   |
| mixView  バナー 320 x 50| 4f9c1a87-4bde-4c50-80ef-c4ca734348b3   |
| mixView  バナー 300 x 250| 125f01f9-0ce0-4de2-8a94-25ebbbecfa8a   |
| mixView  ネイティブ      | aa6b3f0b-6068-49b2-970d-a3bf2c02adc8   |
| mixFullScreenバナー 320 x 50| f3b3764a-1e10-431a-aa29-fd8c874e66e3   |
| mixFullScreenバナー 300 x 250| fd028949-c283-4322-ab64-185046852d40   |
| mixFullScreenネイティブ   | 69e222c0-b213-4c71-a983-158cf35d4524   |
| mixFullScreen インタースティシャル     | 241017d9-cae2-426b-8fe1-f4ad82d7b8b0   |

### [Amazon](./mediation_amazon.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | 6d258892-8436-47cb-829f-08be71ce31c6   |
| バナー 300 × 250    | 2ecda899-0b1c-424c-a373-2cf15704d3bf   |
| インタースティシャル     | 5c860bb3-9952-4ffd-89de-c8f4845736cf   |

### [AppLovin](./mediation_applovin.md)

info.plist に SDK key を追加してください：<br>
Key：AppLovinSdkKey<br>
Value：qTA2uuo2zUQLXHPGDPooTJLZprJIiR6HDcHEgaJq24ErXVwNTqt73MlOFEssXOL9Q1RIFDlR1136N8uhTlthKc

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | a6c9ecea-fee1-421c-9b8a-4e674e5e4d93   |
| バナー 300 × 250    | a56dd5ae-e02c-4888-92bb-1e84906998a2   |
| インタースティシャル     | 8404f9d7-5a95-4ac2-88cf-7c7965f328a0   |
| ネイティブ         | 660053f8-e3e6-4643-b887-9a2341eddd0b   |
| 動画リワード       | 1deae870-5aee-4423-b535-4e38e7ffbeb6   |
| mixView  バナー 320 x 50| 43875458-06e8-4007-b01b-99f0b3e01745   |
| mixView  バナー 300 x 250| 3ead904a-39b9-4bbf-8b47-36c37738d0d2   |
| mixView  ネイティブ      | 62aa4e04-7d5f-4648-bd2f-e97c10d12ed7   |
| mixFullScreenバナー 320 x 50| cbef286b-24fc-4718-aed5-ac8c2fc5dfaa   |
| mixFullScreenバナー 300 x 250| c1796c98-7a8a-46e1-bd9f-c65ea76b5bf4   |
| mixFullScreenネイティブ   | 1c365c2a-1a66-43dc-a21a-aed715bd8792   |
| mixFullScreen インタースティシャル    | 97cf81f7-245d-4e90-84f1-62b76961a11c   |

### [Chartboost](./mediation_chartboost.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | b667c1c4-d2fd-413e-a0be-214bdb78fc43   |
| インタースティシャル     | dcf40d6e-af32-4710-a808-1083d1125384   |
| 動画リワード       | d81961ef-9c56-4d0c-a8b7-40ec9da79219   |

### [Criteo](./mediation_criteo.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | f69148b6-6bfe-47db-9bad-c7373b43ede7   |
| バナー 300 × 250   | 1bc4c46f-1b08-4137-938b-11c7f97163a5   |
| インタースティシャル     | daf02613-7250-4382-842c-d88a15a776e8   |
｜mixView  バナー 320*50| a5c590eb-fa94-403a-a3ef-246a6423c68e  |
｜mixView  バナー 300*250| 7e2a8db2-76db-471e-b77e-0800f8428832  |
| mixFullScreenバナー 320*50| bdf27f85-c22d-41ee-8127-a945a81681d3   |
| mixFullScreenバナー 300*250| f3049012-06ce-4e1a-b15b-4059eb030a99   |
| mixFullScreen インタースティシャル    | 62e655a0-440c-4682-976a-101e393cc8b1   |

### [DFP](./mediation_dfp.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | f1c0f8ae-ae0a-4cc0-99e9-59c9d58e6d28   |
| バナー 300 × 250    | 176f681f-1c7a-4a4b-af87-aa96897817fd   |
| インタースティシャル     | a2bd034b-ac9e-4c5c-a067-ab53ffd97e11   |
| ネイティブ         | 0e00d15a-961c-490b-ba57-ce6fa85573af   |
| 動画リワード       | 02a7ed95-b3c2-48d9-aa8d-3890d57c4f2c   |
| mixView  バナー 320 x 50| 89436cd4-13d9-4cce-a895-71607f4d9320   |
| mixView  バナー 300 x 250| 290216ae-93dd-410f-9c62-382020083c3a   |
| mixView  ネイティブ      | 94a93e62-dae2-4a3e-a534-54ea86413f0c   |
| mixFullScreenバナー 320 x 50| 87fcdded-2ee0-40fd-87ab-4e28535d19c5   |
| mixFullScreenバナー 300 x 250| 70b032d3-f3dc-4953-ab5c-5742d2de2d1e   |
| mixFullScreenネイティブ   | 2b318047-ba5a-4cb3-95f3-3518c2875ffe   |
| mixFullScreen インタースティシャル     | 33b576f0-e34e-49e8-aa8f-6c079ca98cae   |

### [Display.IO](./mediation_display_io.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 300 × 250  | 887e7451-370b-4803-93c1-e419071a208b   |
| インタースティシャル     | 489a37c7-4075-4dce-a3dd-10b754966a37   |
| 動画リワード       | fb0364fc-1072-4e30-abdf-8991ef86a5ee   |

### [DU Ad Platform](./mediation_du_ad_platform.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | 953906c1-862a-429d-925a-c6c5cc794a5f   |
| インタースティシャル     | f92574ad-85c2-47b0-902d-4be949d8e71e   |
| ネイティブ         | 2dc28770-a7c8-42b4-bbba-cc82adcd49e8   |

### [Facebook](./mediation_facebook.md)

[Facebook広告のテスト環境での表示設定](./mediation_facebook.md#テスト環境での表示設定)を参考にしてください。

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | 25029c20-873b-42c2-a4e9-51bd81da663c   |
| バナー 300 × 250    | 8f90397e-9882-4af4-8e32-1e6319e9f3be   |
| インタースティシャル     | 44ef6305-0262-46cd-891a-0364a0057643   |
| ネイティブ         | 12da2ed4-75b4-4861-b52f-86a7c1e74927   |
| ネイティブバナー広告 | 28fce0a5-ad80-4a16-8d6a-c4b6a0cec275   |
| 動画リワード       | a0a73c47-9194-4351-8322-460c9d29f5da   |
| mixView  バナー 320 x 50| 34070a5b-bd0c-4ec4-8584-49f100e4adef   |
| mixView  バナー 300 x 250| 606a7e98-f591-4c5e-ab90-4d16db10cb4f   |
| mixView  ネイティブ      | bd1103d1-a579-4988-8f2b-5abfd02a3a06   |
| mixView ネイティブバナー広告 | 2d93e7c1-f274-4e41-b250-b06b08a1fb88   |
| mixFullScreenバナー 320 x 50| e303f544-5eb5-4057-8eba-a03e540889eb   |
| mixFullScreenバナー 300 x 250| fb983b61-4a80-4270-8002-04558a0ee1c4   |
| mixFullScreenネイティブ   | 9deb0518-3505-4190-b03f-cffd161284f7   |
| mixFullScreen インタースティシャル     | b0bf5992-ab9d-48a6-984a-fdb9f527b80c  |

### [Five](./mediation_five.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 300 × 250  | 7ebe3b57-7b4f-42ff-aa31-5e7ac6696295   |
| インタースティシャル     | b628489f-6f1c-4b4c-9ada-7d1d89418fe1   |
| 動画リワード       | 71bd5399-23b0-41e7-8327-cfcf773db410   |
| mixView  バナー 300 x 250| 4dd6f981-7139-4aa0-bb2d-e1a3f8048d97   |
| mixFullScreenバナー 300 x 250| 74dda437-6e6f-4093-a288-171d0a6e3074  |
| mixFullScreen インタースティシャル     | 84fb619d-59d0-4c40-8a63-1b03a8a79603  |

### [Flurry](./mediation_flurry.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | de69e1d0-4382-484a-bfe3-6937f44dc1d9   |
| インタースティシャル     | f6356310-64dd-430c-93ec-49fc9fe75321   |
| ネイティブ         | 430c4b28-5908-4177-8e01-84caa255d687   |
| 動画リワード       | e895a41a-5245-4357-8a27-fcc6f4c9868f   |

### [Fyber](./mediation_fyber.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | 365f6f63-9b57-4379-a930-1fa8479d1781   |
| バナー 300 × 250  | 1bfc10aa-0d67-4da2-89e7-acc288e81998   |
| インタースティシャル     | dbf26e30-6cf0-4ada-b6d5-65aa0a53fb0b   |
| 動画リワード       | 71f3d9b4-143d-4f96-8223-dda0d11d4362   |
| mixView  バナー 320 x 50| 6eb7168a-7309-41c3-a76e-01f3a6350b14   |
| mixView  バナー 300 x 250| 81f20493-75ae-41b5-8c56-c3b13e4b3515  |
| mixFullScreenバナー 320 x 50| 710204af-2101-4e02-b60d-a9b59d16fdd7  |
| mixFullScreenバナー 300 x 250| ec0438c9-635c-4368-934c-d516720a8f4e  |
| mixFullScreen インタースティシャル | 69bc9a61-a52a-41cc-a2cb-ba32206f93b8 |

### [i-mobile](./mediation_imobile.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | 503ed4e2-e766-43cf-b96d-cc6a9ca8d936   |
| バナー 300 × 250  | b72e1caa-5d94-4887-a134-4618d52aa459   |
| インタースティシャル     | 46c0936d-fa7d-40b0-bc4d-59eda44c9bc2   |
| ネイティブ        | ac506365-ebf8-4f6b-b043-8dd73da89210   |
| mixView  バナー 320 x 50| 32c60041-69e4-4166-b265-f2ac7edd7071 |
| mixView  バナー 300 x 250| 40243724-e635-4a94-b640-d88642b7e40e |
| mixView  ネイティブ     | b920e30a-d2ef-4d01-b323-205e044b0e57 |
| mixFullScreenバナー 320 x 50| f82fc910-2bbf-49eb-8d2e-f8d8fe55e67c  |
| mixFullScreenバナー 300 x 250| 19c98957-e767-4718-84c5-614c41395891 |
| mixFullScreen ネイティブ   | 8fadda1a-8ebf-4cce-909b-c5e813010bd4 |
| mixFullScreen インタースティシャル | 9b1a25b7-f87d-436c-b764-5852a9575df3 |

### [IronSource](./mediation_ironsource.md)

| 広告タイプ          | 広告枠 ID                              |
|:-----------------:|:--------------------------------------:|
| バナー 320 × 50      | b0260b4c-4eda-47f9-b770-7b7d28ebb8e9   |
| バナー 300 × 250    | 1337e3e0-23e9-4849-983b-a4260956d21b   |
| インタースティシャル      | c962295d-f7aa-4b5f-ba22-b46731839985   |
| 動画リワード        | ef262b1e-6a0f-47f0-9b6b-3a1f2adf06ff   |

### [Maio](./mediation_maio.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| インタースティシャル     | 99617581-85cf-4f65-8c46-c4470dd20bc2   |
| 動画リワード       | 25e2bebf-a692-4228-803e-82038b56261a   |

### [MoPub](./mediation_mopub.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | 4f7560dc-58c7-433b-a227-7b61aea3d7ae   |
| バナー 300 × 250     | 83914041-0f00-480a-ac76-c574e9be2ab3   |
| インタースティシャル     | 94bcc9c9-ca60-4a06-a84d-e9c893a0b933   |
| ネイティブ         | 10329cb4-6676-4a69-b20c-48736a953dbf   |
| 動画リワード       | 7aba7997-967f-4d83-b7c4-dec97bf684cf   |
| mixView  バナー 320 x 50| d5cdf029-bdbc-48fc-811b-82845af12035   |
| mixView  バナー 300 x 250| f04fbc98-5a9c-4398-badf-cd8655b0c6a3   |
| mixView  ネイティブ      | be11fc9a-d3f4-4abc-946f-189ac41df3d9   |
| mixFullScreenバナー 320 x 50| 6dd950fa-e50b-43f4-b748-0d885950ab59  |
| mixFullScreenバナー 300 x 250| b700e8bd-9423-4213-aa27-e8bbc9afa722  |
| mixFullScreenネイティブ   | 8eeab8ae-6f91-4d8a-8f5b-4d84123bedbb   |
| mixFullScreen インタースティシャル     | 112079e4-01db-435c-8308-ec2b35a8bf1e  |

### [Nend](./mediation_nend.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50     | e1024c92-bf41-4892-a7f1-9971b675181b   |
| バナー 300 × 250    | e41bda79-c924-42f9-89d4-21bfefccf261   |
| インタースティシャル     | ef9c77ea-2fa3-4efe-a107-52e771648e5c   |
| ネイティブ         | f0accbea-1961-4a72-8962-5fcc91609637   |
| 動画リワード       | 79108573-598c-42bc-808b-8569a2cada72   |
| mixView  バナー 320 x 50| f587bcc0-e34d-42b7-9a6b-735038f8f469  |
| mixView  バナー 300 x 250| 9534908a-c253-4481-bfbb-871bb553dfc6 |
| mixView  ネイティブ      | 78e0d33b-1fb9-4de4-b225-9f2161e0a387  |
| mixFullScreenバナー 320 x 50| 76ce7ce9-9fd3-4665-b4b1-86c0f4d8b37f  |
| mixFullScreenバナー 300 x 250| 64d06129-b09a-4a25-9e61-99f9a1f73bfb  |
| mixFullScreenネイティブ   | 1c76ab44-16a2-4971-bb90-f1169ed8f422   |
| mixFullScreen インタースティシャル    |5a5ed4b8-9127-49e5-b3a4-e09e74748814 |

### [Tapjoy](./mediation_tapjoy.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| インタースティシャル     | dacdf765-61e7-4f3b-b21c-c1ec0d81fef2   |
| 動画リワード       | bf9e8efe-eda0-4ec4-9f7f-8543062d9d7e   |

### [TikTok](./mediation_tiktok.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| インタースティシャル      | 66123f13-5a77-4cee-ab21-3bfd27d8b84d   |
| 動画リワード       | 1f1a5107-b710-4969-bb8a-f306a7fcf2b4   |
| ネイティブ         | b3162881-30e7-4526-99f3-956f45167eb3   |
| mixView  ネイティブ      | 1d0a86df-adf6-4b28-a582-2842600ef9fa  |
| mixFullScreenネイティブ  | f48dd1a7-3ae5-483b-ba36-4f226eea8461 |
| mixFullScreen インタースティシャル   | ef5478a7-be57-45b6-8fd1-fde71f7f5107 |

### [Unity Ads](./mediation_unity_ads.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 320 × 50   | 60769db1-6d78-4d92-9875-44cea0d75bdc   |
| インタースティシャル     | f6122590-1b63-4255-b2f6-537282877009   |
| 動画リワード       | c3c312ba-992e-49e2-9d56-f5cab030e550   |

### [Vungle](./mediation_vungle.md)

| 広告タイプ         | 広告枠 ID                              |
|:----------------:|:--------------------------------------:|
| バナー 300 × 250  | 8a9ecfba-6e7c-4ce2-bdda-18fdd0e518ea   |
| インタースティシャル    | af65d340-1ae2-4f57-90cf-bf723bb78a34   |
| ネイティブ        | b474e668-e8db-4353-9c5c-0ee7fe40905a   |
| 動画リワード      | c6a9d2cd-aa6f-4125-9d5e-6ecbb04e6fbc   |
| mixView  バナー 300 x 250| 8d60c382-029b-4d04-9c7b-8dc0f1f58ad9 |
| mixView  ネイティブ |11c30fe4-3423-4f9b-bea8-cafa669b7382 |
| mixFullScreenバナー 300 x 250| a98f821f-7df7-491b-a11c-2a35e36c5c40 |
| mixFullScreen ネイティブ |750cddb6-03d5-49f6-8695-204da4d85d7c |
| mixFullScreen インタースティシャル  | 892ba842-29ed-4900-8ad4-ae6e5fa0fc3c |