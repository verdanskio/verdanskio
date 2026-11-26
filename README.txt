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

Audio update: explicit Web Audio sample playback and gesture resume. Actual menu-music output was measured in Chromium; the earlier stream build produced zero output.

## Interaction update - 26 November 2026

- Mouse wheel zooms the tactical map under the cursor. Drag to pan; left-click to place a local ping; right-click to remove it. The recovered original ping image and location/confirmation audio are used. Pings appear on the map, minimap and in the world.
- Coarse original terrain remains visible until the detailed tile is resident, reducing the blue circular holes. Original cloud texture is retained with capped sky fog blending.
- Step traversal and narrow fence detection are improved. A nine-step staircase and 1.5-metre fence passed the GPU fixture; this does not verify every source building or door.
- Original supply-box opening now ejects 3D loot. Nearby supplies enter inventory; use E to take/equip weapons and G to throw a recovered frag model. Movement, outline, pickup and grenade logic are reconstructed Godot behavior. Some pickup material bindings and the original frag detonation sound remain unresolved.
- Normal sprint includes the recovered original static offset plus movement loop.
- Original dust and bullet-hole textures have not been positively identified. No temporary impact textures have been added.

The updated browser reached the menu and Verdansk with no captured runtime/JavaScript errors. Music output was measured above zero. Known WebGL draw-buffer warnings and streaming stutter remain; full-match and 120-bot stability were not tested.

## Equipment, lighting and loading update - 26 November 2026

- Press 4 to insert a plate; hold 4 to repeat. The original raise, insert-cycle and drop clips replace the earlier gesture. The source open, raise, insertion and close sound events follow the recovered animation notifies. The rifle is hidden throughout the action and restored afterward. Inventory changes at the original insertion notify. Fire/reload/weapon switching can interrupt an unfinished plate without spending it.
- G uses the original two-handed mobile frag preparation, hold and throw clips. It does not use a flashbang animation. Quick taps finish preparation before release; holding G cooks the fuse. The recovered original player pin-pull sample and original bounce samples are connected.
- Five original smoke/spark flipbook atlases were recovered through the original frag particle system's material references. Godot emission, blending and timing are reconstructed. Only low-resolution local stream levels were available; the complete original particle graph is not ported. The exact detonation sound and separate pin/lever skin animation remain unresolved.
- Escape > Settings includes a 60-120 degree FOV slider, applied while paused and saved locally.
- Console commands set_night and set_day change actual directional light, ambient illumination, sky exposure and atmospheric scattering. Day restores the stored daytime state. Night is a reconstructed moonlit preset, not an original recovered night map.
- The deployment countdown is 30 seconds. Streaming continues during this time; this does not guarantee every distant asset is resident.
- Collision generation now includes opaque source bark geometry for all 31 imported tree models. Transparent foliage and billboard impostors remain excluded. This validates the model collision builders, not every placement across the entire map.
- Full player movement without jumping previously passed three original stair meshes. The original world waypoint pin and confirmation sound remain connected.

Validation: native GPU action/inventory/interruption and source-effect cleanup fixtures; 31 tree-model collision builders; reversible light changes; paused FOV; browser main menu and Verdansk startup; pointer lock, map, console commands and FOV interaction; nonzero music output. Known WebGL draw-buffer warnings remain. A full match and 120 bots have not been validated.
