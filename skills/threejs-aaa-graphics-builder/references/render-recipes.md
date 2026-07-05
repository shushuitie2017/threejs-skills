# Render, Lighting, And VFX Recipes

Use this after authored forms exist. Rendering polish cannot compensate for missing models, props, or readable gameplay silhouettes.

## Renderer Setup

- Set `renderer.outputColorSpace = THREE.SRGBColorSpace`.
- Choose tone mapping deliberately. `ACESFilmicToneMapping` often works for cinematic stylized scenes; simpler tone mapping can be better for bright arcade readability.
- Tune exposure against active gameplay, not a static title view.
- Cap DPR, especially on mobile. Start around `Math.min(devicePixelRatio, 1.5 or 2)` and profile.
- Update renderer, camera, composer, and CSS UI dimensions on resize.
- Use a transparent or explicit background only when composition requires it.

## Camera Composition

- Keep the next decision visible. The camera should show player, immediate threat/reward, and route.
- Add depth layers: foreground speed elements, playable midground, background scale cues.
- Use FOV and camera distance to communicate speed without hiding hazards.
- Use camera shake sparingly and clamp intensity.
- Add camera impulses for hits/near misses/boosts, then ease back quickly.
- Check mobile framing separately; vertical and narrow layouts often need different offsets.

## Lighting Stack

Use a small readable stack:

- Key light: defines form and direction.
- Fill light: keeps gameplay objects legible.
- Rim/back light: separates player and hazards from background.
- Practical/emissive lights: authored beacons, engines, pickups, arena markers.
- Contact shadows or shadow blobs: ground important objects.

Avoid many unmeasured dynamic lights. Prefer baked-looking material/emissive cues, light cards, or small unlit decals for repeated signals.

## Shadows And Contact

- Use shadows for hero/player, major hazards, and large world anchors.
- Use smaller shadow maps and limited shadow casters when profiling shows cost.
- Add cheap contact discs or transparent planes for pickups/hovering objects.
- Tune bias to avoid acne and peter-panning.
- Do not let shadows hide collision reads.

## Materials

- Prefer material contrast before post effects: matte vs glossy, metal vs plastic, transparent vs opaque, bright trim vs dark contact.
- Use `MeshStandardMaterial` for most objects and `MeshPhysicalMaterial` only where the premium feature is visible.
- Use emissive maps or small emissive parts for signals instead of making entire objects glow.
- Match material roles across UI and world: danger, reward, shield, boost, objective.

## Fog, Background, And Depth

- Fog should reveal depth and mood, not hide empty worlds.
- Layer background silhouettes at varied scales and heights.
- Add parallax or slow-moving far layers for motion-heavy games.
- Avoid single flat sky colors when the world needs scale; use gradients only as support, not the whole art direction.
- Keep hazards/rewards readable against fog and background values.

## Post-Processing

Use post as a finishing pass:

- Bloom: only authored emissive elements, not all bright materials.
- Vignette: subtle focus, never heavy darkness.
- Film grain/noise: low opacity; avoid compression-like artifacts.
- Chromatic aberration: only brief event-driven impacts or very subtle style.
- Motion blur/trails: prefer geometry trails or particles that preserve gameplay clarity.

Always compare screenshots with post enabled/disabled and profile the cost.

## Event-Driven VFX

Tie effects to state:

- Boost: engine cones, trail ribbons, FOV ease, side streaks, audio pitch.
- Pickup: ring snap, shard particles, score line to HUD, short light pulse.
- Hit: impact ring, debris, damage flash, brief hit pause, camera impulse.
- Near miss/combo: edge spark, badge pulse, streak counter animation.
- Shield: shell mesh, rim pulse, absorbed impact ripple.
- Spawn/despawn: anticipation pulse, telegraph, dissolve or scale snap.

Pool effects and reuse geometries/materials. Permanent particle fields should be cheap and sparse.

## Readability Checks

During active play, confirm:

- Player orientation is clear.
- Threats differ from rewards by both shape and material.
- Important pickups are visible before reaction time expires.
- UI feedback does not cover the play path.
- VFX clarifies state instead of obscuring collisions.
- Background contrast does not swallow dark objects.

## Performance Checks

After render changes, report:

- FPS/frame time if available.
- Draw calls.
- Triangles.
- Geometries, textures, and materials.
- Composer/post passes.
- Shadow casters and shadow map settings.
- DPR cap and mobile notes.

If performance drops, reduce post/shadow cost first, then cull/LOD/instance, then reduce asset density only where it is least visible.
