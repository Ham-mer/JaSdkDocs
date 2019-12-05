---
sidebar: auto
---

# Creative Macros

## マクロ

AdLime のマクロでは、以下のパラメータに対応しています。

| 型        | マクロ          | 説明                             |
| ----------- | -------------- | --------------------------------- |
| App ID      | %%APPID%%      | アプリ ID		                  |
| AdUnit ID   | %%ADUNITID%%   | 広告ユニット ID               |
| LineItem ID | %%LINEITEMID%% | ラインアイテム ID             |
| Bundle ID   | %%BUNDLE%%     | Android : パッケージ名 / iOS : バンドル ID |
| IP Address  | %%IPADDRESS%%  |                                   |
| Device ID   | %eudid!        |                                   |
| Latitude    | %%LATITUDE%%   |                                   |
| Longitude   | %%LONGITUDE%%  |                                   |
| User Agent  | %%USERAGENT%%  |                                   |

## サンプル

Html：
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>
			Document
		</title>
	</head>
	<style>
		body{margin:0;text-align:center;}
	</style>
	<body>
		<a id="btn" href="https://www.access.com?appid=%%APPID%%&adunitId=%%ADUNITID%%&bundle=%%BUNDLE%%&adid=%eudid!&ua=%%USERAGENT%%">
			<img src="https://www.access.com/static/uploads/press/press1_CEzSDGh.png"
			/>
		</a>
	</body>
</html>
```

Vast：
```xml
<VAST version="3.0">
	<Ad id="1413833">
		<InLine>
			<AdSystem>
				ExoClick
			</AdSystem>
			<AdTitle/>
			<Error>
				<![CDATA[http://main.vagrant.dev/view.php?errorcode=[ERRORCODE]&idzone=2051755]]>
			</Error>
			<Creatives>
				<Creative sequence="1" id="13803673">
					<Linear skipoffset="00:00:11">
						<Duration>
							00:00:13.35
						</Duration>
						<TrackingEvents>
							<Tracking event="progress" offset="00:00:10.000">
								<![CDATA[http://main.vagrant.dev/view.php?tracking_event=progress&progress=00:00:10.000&idzone=2051755]]>
							</Tracking>
						</TrackingEvents>
						<VideoClicks>
							<ClickThrough>
								<![CDATA[https://www.access.com?appid=%%APPID%%&adunitId=%%ADUNITID%%]]>
							</ClickThrough>
						</VideoClicks>
						<MediaFiles>
							<MediaFile delivery="progressive" type="video/mp4">
								<![CDATA[http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4]]>
							</MediaFile>
						</MediaFiles>
					</Linear>
				</Creative>
			</Creatives>
		</InLine>
	</Ad>
</VAST>
```

Track Url：

```
http://www.test.track.url?adid=%eudid!&lat=%%LATITUDE%%&lon=%%LONGITUDE%%&ua=%%USERAGENT%%
```