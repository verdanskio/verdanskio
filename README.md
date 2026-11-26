# Verdanskio browser prototype

Unofficial Godot prototype using the existing reconstructed gameplay and recovered local assets. This is not the original Android engine and is not affiliated with Activision.

Open the GitHub Pages website and click **Load game**. The complete asset download is large; use a recent desktop Chromium/Firefox browser with WebGL 2 and hardware acceleration. First loading can take several minutes. Keep the tab open while loading.

## Controls

- WASD: move; mouse: look; left click: fire; right click: aim.
- R: reload; 1/2: weapons; 3: fists.
- Shift: sprint; double Shift: tactical sprint; Shift while scoped: steady aim.
- Space: jump/vault, leave plane, deploy/cut parachute.
- Hold C: crouch/slide; Z: prone.
- M / AZERTY comma: full map; backtick/tilde: console; type `help`.
- Escape: pause/settings; V: third person; K: noclip.

The browser may release pointer lock on Escape or tab changes. Click inside the game to recapture it. Browser-reserved shortcuts remain controlled by your browser.

## Hosting

All runtime files are at repository root. `assets.json` lists numbered data chunks, sizes and SHA256 hashes. The loader reconstructs the exported game pack before startup. Keep filenames intact. Serve over HTTP(S), not file://. GitHub Pages can use the main branch/root folder; `.nojekyll` is supplied. No APK, emulator, account login or external game CDN is needed.

## Export differences and limits

This is a browser export of the current native Godot prototype. Terrain uses every fourth source grid sample with tile boundaries preserved. Selected large texture imports are capped for the web; native files are unchanged. Browser defaults use shorter draw distances and shadows off. Resource loading is incremental on the main thread, so large geometry/collision loads may still stutter.

Original speech samples are connected to implemented match events, not the complete native event graph. Native movement/IK, full map POI registration and some source meshes/material bindings remain unresolved. The browser version has additional WebGL/memory limitations; a 120-bot match is not promised.

Use the local export report and browser-test report for the actual checks performed on this build.

## Current browser test

The build reached the main menu and local Verdansk warmup with 21 participants. Pointer lock, map and console input were checked. WebGL draw-buffer warnings remain and rendering/performance are experimental. A full browser match and 120 bots have not been validated. See `build-info.json`.
