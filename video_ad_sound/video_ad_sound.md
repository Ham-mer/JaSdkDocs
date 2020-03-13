# 動画広告の音について

- 動画広告は様々なフォーマットで展示されます。例えばバナーとインタースティシャです。
- ある広告は音なくて再生されますが、ある広告は再生されるときに音が出ます。
- 音が出るか出ないかについて、あるADNWはユーザー側では調整できてあるADNWは開発者側で調整できます。

本文では、Networkを整理します。

Network：AdMob、AppLovin、Criteo、Facebook、Five、i-mobile、Maio、MoPub、Nend、Pangle、TikTok。

**開発者のコントロール**

- Api
    Some Network has Api to set video sound of Ads.

    For example AdMob:
    ```java
    // https://developers.google.com/admob/android/global-settings
    MobileAds.setAppMuted(true);
    ```

    For example Five:
    ```java
    // https://s3-ap-northeast-1.amazonaws.com/fivecdm-public/release-sdk/document/FIVE-Android-SDK-install-guide.pdf
    FiveAd.getSingleton().enableSound(true);
    ```

- web config

    For example Five:

    <div class="clearfix cust-image-text"><img src="./five_sound_webconfig.png"  width="500px"  align=left />
    </div>


**バナー**
| 番号 | ×etwork          | ビデオ          | 音       | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:--------:|:--------:|:-------------:|
| 1   | AdMob            | ◯ (web config) | mute     | ◯        | ◯ (Api)       |
| 2   | AppLovin         | ×              | ×        | ×        | ×             |
| 3   | Criteo           | ◯              | mute     | ×        | ×             |
| 4   | Facebook         | ×              | ×        | ×        | ×             |
| 5   | Five             | ◯              | sound    | ◯        | ◯ (Api & web config)|
| 6   | i-mobile         | ◯ (web config) | unknown  | ×        | ×             |
| 7   | MoPub            | ◯              | unknown  | ×        | ×             |
| 8   | Nend             | ×              | ×        | ×        | ×             |

**インタースティシャ**
| 番号 | ×etwork          | ビデオ        | 音       | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:------------:|:--------:|:-------------:|
| 1   | AdMob            | ◯ (web config) | unknown      | ◯        | ◯ (Api)       |
| 2   | AppLovin         | ◯              | sound        | x        | ◯ (Api)       |
| 3   | Criteo           | ×              | ×            | ×        | ×             |
| 4   | Facebook         | ◯              | mute (>=5.7.0)<br>sound (<5.7.0)| ◯        | ×             |
| 5   | Five             | ◯              | sound        | ◯        | ◯ (web config)|
| 6   | i-mobile         | ×              | ×            | ×        | ×             |
| 7   | Maio             | ◯              | sound        | ◯        | ×             |
| 8   | MoPub            | ◯              | unknown      | ×        | ×             |
| 9   | Nend             | ◯              | mute         | ◯        | ◯ (Api)       |
| 10  | Pangle           | ◯              | sound        | ◯        | ×             |
| 11  | TikTok           | ◯              | sound        | ◯        | ×             |

**ネイティブ**
| 番号 | ×etwork          | ビデオ        | 音             | ユーザさんのコントロール             | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:------------------:|:------------------:|:--------------:|
| 1   | AdMob            | ◯ (web config) | mute               | ◯                  | ◯ (Api)        |
| 2   | AppLovin         | ◯              | mute               | ×                  | ◯ (Api)        |
| 3   | Facebook         | ◯              | mute (normal)<br>sound (fullscreen) | x                  | ×              |
| 4   | i-mobile         | ×              | ×                  | ×                  | ×              |
| 5   | MoPub            | ◯              | mute (normal)<br>sound (fullscreen) | ◯ (normal)<br>× (fullscreen) | ◯ (Api)        |
| 6   | Nend             | ◯              | mute (normal)<br>sound (fullscreen) | × (normal)<br>◯ (fullscreen)     | × (normal)<br>◯ (fullscreen: Api) |
| 7   | TikTok           | ◯              | mute (normal)<br>sound (fullscreen) | x                  | ×              |

sound (fullscreen)：ネイティブ広告は音なくて再生されますが、ユーザさんがクリックするとフルスクリーンで再生すると音が出ます。

**動画リワード**
| 番号 | ×etwork          | 音        | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:-------------:|:--------:|:--------------:|
| 1   | AdMob            | sound         | ◯        | ◯              |
| 2   | AppLovin         | sound         | ×        | ◯              |
| 3   | Facebook         | mute (>=5.7.0)<br>sound (<5.7.0) | ◯        | ×              |
| 4   | Five             | sound         | ◯        | ◯ (web config) |
| 5   | Maio             | sound         | ◯        | ×              |
| 6   | MoPub            | sound         | x        | ×              |
| 7   | Nend             | sound         | x        | ×              |
| 8   | Pangle           | sound         | ◯        | ×              |
| 9   | TikTok           | sound         | ◯        | ×              |