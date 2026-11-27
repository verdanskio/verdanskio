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

## MW2019 menus - 27 November 2026

The startup screen now uses the original MW2019 mode-selection background movie and Campaign, Multiplayer and Co-op blade movies. Their positions, invisible hit regions, idle captions and masked 200 ms reveal / 100 ms collapse are reconstructed from the local 1.20 UI scripts. Select Multiplayer to enter the second screen, the tabbed Multiplayer lobby.

Both screens use the actual MW2019 Bio Sans Regular/Bold fonts. The original main-menu theme and 17 original focus, confirmation, back, deny, blade and tab samples were recovered from the local sound banks. The music is imported losslessly; its runtime PCM hash matches the recovered source. The Bink movies were converted to Theora and fully decode-checked.

The Multiplayer lobby offers Play, Weapons, Operators, Barracks, Battle Pass and Store tabs. Quick Play starts the existing local Verdansk prototype; Private Match shows its actual BR map and bot count. Weapons selects the X12 (default), M4 or Kar98k starting weapon. Settings retains graphics, audio, FOV and input options. Keyboard, pointer and gamepad shoulder tab navigation are supported.

This is a reconstruction in Godot, not a complete port of the original UI runtime. The original animated 3D Multiplayer lobby/operator scene is not recovered; its original fallback image is used. Campaign and Co-op gameplay, network challenges, store purchases and a complete original loadout system are not implemented. Not every widget, text effect or submenu has exact original parity.

Validation: native rendered menu snapshots, all three blade videos, lossless music PCM, mode/lobby navigation, controller shoulder tabs, modal focus, Escape, settings and real starting weapon equip. Chromium also reached both new menus and the existing Verdansk scene, and measured audible music. This test does not validate a complete match or 120 bots.
## Drop, pistol and terrain update - 27 November 2026

The default starting weapon is now the recovered X12 / pi_golf17 pistol with its original component meshes, UVs, available textures, source animations and sound samples. Empty reload and last-round fire are connected. The locally available pistol albedos are only 64-128 pixels; this is not a recovered high-resolution texture set. Stationary weapons use recovered moving-idle data; the Kar98k uses shared additive hand/gun motion because a complete Kar-specific idle clip was not recovered.

The altimeter samples the original 4097 x 4097 terrain heightfield under the player, independently of streamed collision loading. It reports terrain distance, not distance to a roof. The airborne loadout panel hides after five seconds. The original sky image is unchanged; cloud cards during the drop reuse that image. Flight runs from DAM toward Prison. Sixty prototype bots are prepared incrementally, frozen during flight, then redeployed after landing using staged clearance checks. They can open shared supply boxes and collect physical loot. This is reconstructed AI, not the native game's complete navigation and event logic.

Original closed-box presence/hum and open samples are connected to supply crates. The source altimeter graphics are used with reconstructed layout. Shader depth bias, terrain coverage and source-height clipping of a specific grass material address observed stretched ground surfaces and z fighting. Explicit caulk/sky helper surfaces are excluded from appropriate visible/collision geometry. Roof-edge vaults can finish in open air while retaining clearance checks. The sky texture itself was not recolored.

Validation: the current browser build reached both menu screens and Verdansk, with a running AudioContext and measured nonzero music. Native component and GPU fixtures passed pistol skinning/audio/reload, source-height sampling, the five-second panel timer, roof-edge vaulting, active idle and depth/grass clipping. Earlier native tests prepared and redeployed all 60 bots. A complete 60-bot browser match and every map location have not been validated; there is no claim of complete original-game parity or 120-bot support.

## Slide, loot and landing update - 27 November 2026

First-person slide: uses original Ghost leg triangles (2674 of the source body's 11755 triangles), original UVs, textures, skin weights and bind poses, driven by sdr_mp_me_strafe_slide_8. The first-person framing is reconstructed. The body also contains a cape that obscured the legs; first-person slide now renders only the existing leg triangles. Full original body remains available in third person.

Bot death: hide the loose weapon immediately, stop firing and collisions, stop the source actor pose, and remove the corpse after eight seconds. The loose receiver now receives its recovered M4 albedo instead of rendering white. Physical drops use recovered weapon, armor plate, ammo, cash and grenade meshes. Inventory is dropped once; collected cash/ammo/plates/grenades are retained in the quantities on the bot. The default prototype bot has M4, 60 ammo, one plate and one grenade. Loot collection uses the existing physical pickup path.

Eliminations award +100 XP once, including melee/grenade kills, with a HEADSHOT label for a fatal headshot. Bullet headshot attribution is cleared for other damage types. The XP value is the requested local rule, not a recovered original native score table. Font assets are original; notification layout/timing and the offline combat rules are reconstructed in Godot.

Audio: the existing recovered ui_hitmarker_classic and armor-break samples remain connected. mp_hit_alert_headshot was found twice in ingame_shared_mp.ff.raw, at offsets 60677956 and 62594036, but its encoded sample reference is not yet resolved. A distinct original kill/headshot cue is NOT claimed recovered; no synthetic replacement sound has been added.

Landing: wait briefly before incremental bot activation, stagger target decisions and source animation advancement, simulate distant bots at 15 Hz and close bots at 30 Hz with distance-preserving movement. Source collider triangles are partitioned into batches of at most 2048 triangles per BVH build. Continuous swept ballistic rays adapt their subdivisions to a 1 cm parabolic chord-error bound rather than performing four identical near-linear sweeps each normal frame. NPC bullet pressure is bounded separately from player shots. Inactive prop/model/collider and world texture-cache references are released during streaming.

Tests: source slide rendered on NVIDIA/OpenGL; inventory/death/XP fixture passed; exact collider triangle preservation passed. Real Verdansk loaded, prepared and redeployed all 60 bots in the headless native fixture. In one local comparison the 95th percentile activation frame changed from 64.81 ms to 22.041 ms (median 16.658 ms). These timings are a local headless measurement, not a guarantee for all browsers or a completed battle royale match. See artifacts/landing-budget-profile.json for the current measurements. Chromium also completed the 60-bot preparation, flight, fall, landing and staged activation, and rendered first-person slide legs without script/JavaScript errors. During the browser landing/activation sample, frame timing was median 16.7 ms, 95th percentile 33.4 ms and maximum 350 ms. Occasional asset-loading spikes remain; a full match was not completed.
