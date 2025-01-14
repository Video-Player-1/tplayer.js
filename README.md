![tplayer logo](https://user-images.githubusercontent.com/51857187/161440508-a4cb7d66-fc3c-4202-ad74-4d56a32d1e78.png)

This project is made possible with [Plyr](https://github.com/sampotts/plyr), [Hls.js](https://github.com/video-dev/hls.js/), [Dash.js](https://github.com/Dash-Industry-Forum/dash.js).

## Features 📑

- HLS and DASH playback 🎥
- Multi quality supported 🎬
- Drm with custom header support (Widevine & Playready) 🔐
- Customizable UI ⛏
- Active development 🧱

## Setup and Usage 📚

`tplayer.js` requires a `video` element in the DOM.

### HTML

[See example](https://github.com/tuhinpal/tplayer.js/blob/master/example/html/index.html)

1.  Put the tplayer.js script tag in the `<head>` of your HTML document.

    ```html
    <script src="https://cdn.jsdelivr.net/npm/tplayer.js@latest/dist/index.js"></script>
    ```

2.  Put the video element in the `<body>` of your HTML document.

    ```html
    <video id="tplayer"></video>
    ```

3.  Add some JS to the `<body>` of your HTML document.

    ```html
    <script>
      window.tplayer(options);
    </script>
    ```

### NEXTJS

[See example](https://github.com/tuhinpal/tplayer.js/tree/master/example/nextjs)

You need to import `tplayer.js` into a component which will be dynamically imported (No SSR) to your root.

```bash
# Install tplayer.js
npm install tplayer.js
```

```jsx
// component\player.jsx

import { useRef, useEffect } from "react";
import tplayer, { destroyPlayer } from "tplayer.js";

export default function Player(props) {
  const videoRef = useRef();

  useEffect(() => {
    tplayer({
      ...props,
      playerElem: videoRef.current,
    });

    return () => destroyPlayer({ id: "homeplayer" });
  }, []);

  return <video ref={videoRef}></video>;
}
```

```jsx
// pages\index.jsx

import dynamic from "next/dynamic";
const Player = dynamic(import("../component/player"), { ssr: false });

export default function Home() {
  return <Player {...options} />;
}
```

## Options 📝

| Name                  | Description                          | Default / Requirement / Fallback         | Example                                                               |
| --------------------- | ------------------------------------ | ---------------------------------------- | --------------------------------------------------------------------- |
| id                    | This is the `tplayer.js` instance id | Default: tplayer                         | `'tplayerhtml'`                                                       |
| playerElem            | Video element from DOM               | Required                                 | document.getElementById("tplayer")                                    |
| source                | Source Object                        | At least one DASH or HLS URL is required | {dash:'some.mpd', hls: 'some.m3u8'}                                   |
| source.dash           | MPD URL of your source file          | Required if DRM enabled                  | https://some.mpd                                                      |
| source.hls            | M3U8 URL of your source file         | Not required if Dash is provided         | https://some.m3u8                                                     |
| drm                   | DRM Object                           | Optional                                 | {widevine: {url: '', headers: {}}, playready: {url: '', headers: {}}} |
| drm.widevine          | Widevine Object                      | Optional                                 | widevine: {url: '', headers: {}}                                      |
| drm.widevine.url      | Widevine license URL                 | Required                                 | https://some/proxy                                                    |
| drm.widevine.headers  | Headers object for license requests  | Optional                                 | {"T-Header-One": "Hi", "T-Header-Two": "Hello"}                       |
| drm.playready         | Playready Object                     | Optional                                 | playready: {url: '', headers: {}}                                     |
| drm.playready.url     | Playready license URL                | Required                                 | https://some.asmx                                                     |
| drm.playready.headers | Headers object for license requests  | Optional                                 | {"T-Header-One": "Hi", "T-Header-Two": "Hello"}                       |
| ui                    | Extended UI Object                   | Optional                                 | {mainColor: '#ff002b'}                                                |
| ui.mainColor          | Main color                           | Optional                                 | #ff002b                                                               |

**See this example**

```js
const options = {
  id: "tplayerhtml", // anything
  playerElem: document.getElementById("tplayer"), // grabbing the video element from the DOM
  source: {
    dash: "https://bitmovin-a.akamaihd.net/content/art-of-motion_drm/mpds/11331.mpd",
    hls: "https://bitmovin-a.akamaihd.net/content/art-of-motion_drm/m3u8s/11331.m3u8",
  },
  drm: {
    widevine: {
      url: "https://widevine-proxy.appspot.com/proxy", // Widevine license URL
      headers: {
        // "T-Header": "You can send header like this",
      },
    },
    playready: {
      url: "https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=1&ContentKey=EAtsIJQPd5pFiRUrV9Layw==", // Playready license URL
      headers: {
        // "T-Header": "You can send header like this",
      },
    },
  },
  ui: {
    mainColor: "red",
  },
};
```

## Credits 💖

- [Plyr](https://github.com/sampotts/plyr)
- [Hls.js](https://github.com/video-dev/hls.js/)
- [Dash.js](https://github.com/Dash-Industry-Forum/dash.js).

## License 📝

`tplayer.js` is licensed under the [MIT license](https://github.com/tuhinpal/tplayer.js/blob/master/LICENSE)

## Crafted with 💖 by [Tuhin Kanti Pal](https://thetuhin.com) in 1 day.
