# AdLimeAdLoader
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"AdUnit ID"]で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。 

- [バナー広告](./adloader_banner.md)
- [インタースティシャ広告](./adloader_interstitial.md)
- [ネイティブ動画](./adloader_native.md)
- [動画リワード](./adloader_rewardedvideo.md)
- [MixViewAd](./adloader_mixviewad.md)
- [MixFullScreenAd](./adloader_mixfullscreenad.md)