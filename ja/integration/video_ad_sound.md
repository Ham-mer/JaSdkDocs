# 動画広告の音について

- 動画広告は様々なフォーマットで展示されます。例えばバナーとインタースティシャです。
- ある広告は音なくて再生されますが、ある広告は再生されるときに音が出ます。
- 音が出るか出ないかについて、あるADNWはユーザー側では調整できてあるADNWは開発者側で調整できます。

本文では、Networkを整理します。

Network：AdMob、AppLovin、Criteo、Facebook、Five、i-mobile、Maio、MoPub、Nend、Pangle、TikTok。

**バナー**
| 番号 | ×etwork          | ビデオ        | 音  | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:--------:|:--------:|:-------------:|
| 1   | AdMob            | ◯ (web config) | mute     | ◯        | ◯             |
| 2   | AppLovin         | ×              | ×        | ×        | ×             |
| 3   | Criteo           | ◯              | mute     | ×        | ×             |
| 4   | Facebook         | ×              | ×        | ×        | ×             |
| 5   | Five             | ◯              | sound    | ◯        | ◯ (web config)|
| 6   | i-mobile         | ◯ (web config) | unknown  | ×        | ×             |
| 7   | MoPub            | ◯              | unknown  | ×        | ×             |
| 8   | Nend             | ×              | ×        | ×        | ×             |

**インタースティシャ**
| 番号 | ×etwork          | ビデオ        | 音       | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:------------:|:--------:|:-------------:|
| 1   | AdMob            | ◯ (web config) | unknown      | ◯        | ◯             |
| 2   | AppLovin         | ◯              | sound        | x        | ◯             |
| 3   | Criteo           | ×              | ×            | ×        | ×             |
| 4   | Facebook         | ◯              | mute (>5.7.0)| ◯        | ×             |
| 5   | Five             | ◯              | sound        | ◯        | ◯ (web config)|
| 6   | i-mobile         | ×              | ×            | ×        | ×             |
| 7   | Maio             | ◯              | sound        | ◯        | ×             |
| 8   | MoPub            | ◯              | unknown      | ×        | ×             |
| 9   | Nend             | ◯              | mute         | ◯        | ◯             |
| 10  | Pangle           | ◯              | sound        | ◯        | ×             |
| 11  | TikTok           | ◯              | sound        | ◯        | ×             |

**ネイティブ**
| 番号 | ×etwork          | ビデオ        | 音             | ユーザさんのコントロール             | 開発者のコントロール    |
|:---:|:----------------:|:--------------:|:------------------:|:------------------:|:--------------:|
| 1   | AdMob            | ◯ (web config) | mute               | ◯                  | ◯              |
| 2   | AppLovin         | ◯              | mute               | ×                  | ◯              |
| 3   | Facebook         | ◯              | sound (fullscreen) | x                  | ×              |
| 4   | i-mobile         | ×              | ×                  | ×                  | ×              |
| 5   | MoPub            | ◯              | sound (fullscreen) | ◯ (non-fullscreen) | ◯              |
| 6   | Nend             | ◯              | sound (fullscreen) | ◯ (fullscreen)     | ◯ (fullscreen) |
| 7   | TikTok           | ◯              | sound (fullscreen) | x                  | ×              |

sound (fullscreen)：ネイティブ広告は音なくて再生されますが、ユーザさんがクリックするとフルスクリーンで再生すると音が出ます。

**動画リワード**
| 番号 | ×etwork          | 音        | ユーザさんのコントロール | 開発者のコントロール    |
|:---:|:----------------:|:-------------:|:--------:|:--------------:|
| 1   | AdMob            | sound         | ◯        | ◯              |
| 2   | AppLovin         | sound         | ×        | ◯              |
| 3   | Facebook         | mute (>5.7.0) | ◯        | ×              |
| 4   | Five             | sound         | ◯        | ◯ (web config) |
| 5   | Maio             | sound         | ◯        | ×              |
| 6   | MoPub            | sound         | x        | ×              |
| 7   | Nend             | sound         | x        | ×              |
| 8   | Pangle           | sound         | ◯        | ×              |
| 9   | TikTok           | sound         | ◯        | ×              |