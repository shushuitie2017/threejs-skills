# Director Phase OS

Use this reference only after `threejs-game-director` has attempted to load the relevant sibling public skill files and one or more files were unavailable. This file is the fallback operating system, not a reason to skip sibling skill loading.

## Non-Negotiable Rules

- Do not claim another public skill was invoked unless its `SKILL.md` was actually loaded or the runner explicitly invoked it.
- For broad game work, try to load all five sibling public skill files before implementation: gameplay systems, AAA graphics, UI designer, debug profiler, and QA release.
- When external 3D assets would help, also try to load `threejs-3d-generator`; when 2D concepts/textures/UI art would help, also try to load `threejs-image-generator`; when SFX/ambience/voice would help, also try to load `threejs-audio-generator`.
- For premium/AAA/showcase/high-fidelity/less-basic work with vehicles, ships, characters, creatures, weapons, buildings, signature props, skies/backgrounds, textures, decals, logos, icons, GUI art, SFX, ambience, or voice, load the relevant generator skill before deciding it is not needed.
- Before claiming a missing generator credential, run the director credential probe and paste the literal SET/MISSING output.
- Record an external asset sourcing ledger before the graphics phase.
- Record sibling skill loading paths or failure reasons in the ledger.
- Load each phase's required reference files at phase entry. Do not defer references until final judgment.
- Record every required reference path or failure reason in the reference ledger.
- A phase cannot be marked `done` if its required references were skipped.
- A broad game request is not complete after a first playable slice when the user asked for premium, AAA, polished, showcase, complete, release-ready, or "less basic".
- Keep an execution ledger with phases, evidence, skipped work, and blockers.
- Prefer a small authored vertical slice over a larger placeholder scene.
- Treat primitive-dominant models, box skylines, flat arenas, generic stat-card HUDs, and glow/fog-only detail as prototype placeholders.
- Verify through browser evidence before calling the game done.

## External Asset Sourcing Gate

For broad or premium game work, fill this before the graphics phase:

```text
External asset sourcing:
- Credential probe output:
- Hero/player:
- Enemies/vehicles/weapons:
- Signature props/pickups:
- World/sky/background:
- Materials/textures/decals:
- Logos/icons/GUI art:
- Audio/SFX/voice:
- Chosen sources per surface: procedural / threejs-image-generator / threejs-3d-generator / threejs-audio-generator / hybrid
- 3D generator loaded: yes/no, path or blocker:
- Image generator loaded: yes/no, path or blocker:
- Audio generator loaded: yes/no/not-needed, path or blocker:
- External assets generated: yes/no, outputs or reason:
- Audio assets generated: yes/no/not-needed, outputs or reason:
```

Allowed reasons to skip actual external generation after loading the relevant skills:

- The user explicitly requested no external AI/assets or offline-only output.
- Credential probe output shows the relevant key is `MISSING`.
- A real API/network/quota error occurs after an attempted generation command; include the command and error summary.
- The surface is a repeated low-value prop better handled by instancing/procedural kits.
- A non-hero repeated/support surface is already scoring 2+ and the ledger explains why external generation would not improve the active screenshot.

Do not write `not-needed` for generator skills before loading the relevant skill when trigger surfaces are present.

For premium claims with hero surfaces such as player, enemy, boss, creature, vehicle, ship, weapon, building, or signature prop, procedural-only is not an allowed final answer unless the credential probe or attempted generation shows a real blocker. At least one hero/high-value asset must have real external evidence: a 3D generator task ID, downloaded GLB/GLTF/FBX path, image generator output path, or documented hybrid chain. For premium active gameplay, missing audio assets must be reported as a remaining gap unless the user requested silent/offline-only output or the audio credential/API attempt is blocked.

## Required References

Load these files before the matching phase starts:

- Gameplay systems: `threejs-gameplay-systems/references/gameplay-workflows.md`
- Physics selection, when physics/collision-heavy gameplay is in scope: `threejs-gameplay-systems/references/physics-engine-selection.md`
- New-game checklist, when creating a game or first playable slice: `threejs-gameplay-systems/references/checklists/new-game-definition-of-done.md`
- Endless runner checklist, when building or upgrading an endless runner: `threejs-gameplay-systems/references/checklists/endless-runner-premium-quality.md`
- AAA graphics: `threejs-aaa-graphics-builder/references/visual-scorecard.md`
- AAA graphics: `threejs-aaa-graphics-builder/references/implementation-blueprint.md`
- AAA graphics: `threejs-aaa-graphics-builder/references/model-recipes.md`
- AAA graphics: `threejs-aaa-graphics-builder/references/render-recipes.md`
- AAA graphics checklists, for premium/AAA/showcase claims: `threejs-aaa-graphics-builder/references/checklists/aaa-game-quality-gate.md` and `threejs-aaa-graphics-builder/references/checklists/aaa-visual-scorecard.md`
- UI: `threejs-game-ui-designer/references/ui-patterns.md`
- UI checklists, when UI/HUD/menu/touch layout is in scope: `threejs-game-ui-designer/references/checklists/game-ui-quality.md`, `threejs-game-ui-designer/references/checklists/hud-readability.md`, and `threejs-game-ui-designer/references/checklists/responsive-ui-fit.md`
- Debug/profile: `threejs-debug-profiler/references/debug-profile-checklists.md`
- Debug/profile checklists, when debugging or profiling: `threejs-debug-profiler/references/checklists/scene-debugging.md` or `threejs-debug-profiler/references/checklists/performance-profile.md`
- QA/release: `threejs-qa-release/references/qa-release-checklists.md`
- QA/release checklists, for final verification: `threejs-qa-release/references/checklists/visual-verification.md`, `threejs-qa-release/references/checklists/playtest-qa.md`, and `threejs-qa-release/references/checklists/release.md`
- 3D generator, when loaded by the external asset sourcing gate: `threejs-3d-generator/references/api-notes.md`
- 3D generator, when loaded for a game: `threejs-3d-generator/references/threejs-integration.md`
- 3D plus image generator, when both are loaded: `threejs-3d-generator/references/image-generator-workflows.md`
- Audio generator, when loaded for a game: `threejs-audio-generator/references/audio-workflows.md`

Try paths relative to the loaded skill directory first, then `~/.claude/skills`, `~/.codex/skills`, `~/.agents/skills`, and finally repository `skills`.

## Phase Ledger Template

```text
Director: active
Sibling skill files loaded:
- Gameplay systems: yes/no, path or reason:
- AAA graphics: yes/no, path or reason:
- UI: yes/no, path or reason:
- Debug/profile: yes/no, path or reason:
- QA/release: yes/no, path or reason:
- 3D generator: yes/no/not-needed, path or reason:
- Image generator: yes/no/not-needed, path or reason:
- Audio generator: yes/no/not-needed, path or reason:
External asset sourcing:
- Credential probe output:
- Hero/player source:
- Enemies/vehicles/weapons source:
- Signature props/pickups source:
- World/sky/background source:
- Materials/textures/decals source:
- Logos/icons/GUI art source:
- Audio/SFX/voice source:
- External assets generated or skip reason:
- Audio assets generated or skip reason:
Required references loaded:
- Gameplay workflows: yes/no/not-needed, path or reason:
- Physics engine selection: yes/no/not-needed, path or reason:
- Gameplay/new-game checklists: yes/no/not-needed, path or reason:
- Visual scorecard: yes/no/not-needed, path or reason:
- Graphics implementation blueprint: yes/no/not-needed, path or reason:
- Model recipes: yes/no/not-needed, path or reason:
- Render recipes: yes/no/not-needed, path or reason:
- Graphics checklists: yes/no/not-needed, path or reason:
- UI patterns: yes/no/not-needed, path or reason:
- UI checklists: yes/no/not-needed, path or reason:
- Debug/profile checklists: yes/no/not-needed, path or reason:
- QA/release checklists: yes/no/not-needed, path or reason:
- 3D generator API notes: yes/no/not-needed, path or reason:
- 3D generator Three.js integration: yes/no/not-needed, path or reason:
- 3D/image generator workflows: yes/no/not-needed, path or reason:
- Audio workflows: yes/no/not-needed, path or reason:
Gameplay systems: pending/running/done/skipped - evidence:
External asset sourcing: pending/running/done/skipped - evidence:
AAA graphics: pending/running/done/skipped - evidence:
UI: pending/running/done/skipped - evidence:
Debug/profile: pending/running/done/skipped - evidence:
QA/release: pending/running/done/skipped - evidence:
```

Mark a phase `done` only after implementation plus verification. If a phase is skipped, state why it is out of scope or blocked.

## Phase 1: Discovery And Playable Contract

- Inspect package scripts, dependencies, app structure, renderer setup, loop ownership, input, camera, UI, diagnostics, and existing screenshots.
- Define the one-sentence loop: player verb, objective, pressure, reward, fail state, restart.
- Define target devices and performance budget. If absent, assume desktop plus mobile browser, WebGL/WebGL2 fallback, and capped DPR.
- Identify the highest-risk surfaces: blank/broken canvas, no playable loop, weak controls, basic graphics, unreadable UI, or unverified release.

Exit evidence:

- Current scripts/dependencies known.
- Playable loop stated.
- Phase ledger initialized.

For a new project, use the gameplay skill's packaged scaffold creator:

```bash
python3 <threejs-gameplay-systems-skill-dir>/scripts/create_threejs_game.py ./my-game
```

## Phase 2: Gameplay Systems

Build or repair the playable loop before visual depth.

- Add renderer, scene, camera, resize, update loop, input intents, state machine, entities, collision or physics, scoring/progression, fail/retry, HUD state, audio/VFX hooks, and diagnostics.
- If the game is physics-heavy, load the physics selection reference, choose an engine explicitly, and prefer Rapier for robust browser physics unless the task fits custom collision or a small cannon-es fallback.
- Keep ownership boundaries clear: `core`, `game`, `entities`, `systems`, `assets`, `ui`, `tests`.
- Tune movement, camera follow, FOV, acceleration, cooldowns, difficulty, and restart through short play loops.
- Keep collision proxies simpler than detailed meshes.
- Avoid multiple animation loops, duplicated state, and per-frame allocations in hot paths.

Exit evidence:

- Build/typecheck passes.
- Browser opens with nonblank canvas.
- Main control path changes state.
- Objective or score progresses.
- Fail/retry path exists when relevant.
- Physics engine choice, timestep, collider strategy, and diagnostics are reported when physics is in scope.
- New-game checklist outcome is reported for new games or first playable slices.

## Phase 3: External Asset Sourcing

Run before the premium graphics pass when trigger surfaces exist.

- Run the credential probe from the director skill scripts and paste output.
- Load `threejs-3d-generator`, `threejs-image-generator`, and/or `threejs-audio-generator` when their trigger surfaces exist.
- Load 3D generator API notes, Three.js integration, image-generator workflow, and audio workflow references when relevant.
- Decide source per high-value surface: procedural / threejs-image-generator / threejs-3d-generator / threejs-audio-generator / hybrid.
- Generate at least one high-value external output for premium hero surfaces unless the probe or attempted generation shows a real blocker.
- Record 3D generator task IDs, downloaded GLB/GLTF/FBX paths, image generator output paths, audio output paths, or blocker evidence.

Exit evidence:

- Credential probe output.
- Skill/reference loading ledger for generator skills.
- Asset sourcing ledger.
- External outputs or blocker evidence.

## Phase 4: AAA Graphics

Use when screenshots look basic or the user asks for premium quality.

- Score active-play screenshot across art direction, hero/player, obstacles/enemies, rewards/interactables, world/environment, materials/textures, lighting/render, VFX/motion, UI/HUD, and performance evidence.
- Add production graphics architecture: material library, procedural textures, decals, model factories, world prop kit, VFX system, lighting/render pipeline, diagnostics.
- Upgrade all visible surfaces, not only the player: hero, hazards, rewards, ground/track/arena, foreground props, background layers, interactable telegraphs, material variation, and state VFX.
- Use `threejs-image-generator` for concept/reference images, texture references, logos, icons, decals, skies, and image-to-3D inputs when 2D source art would improve quality.
- Use `threejs-3d-generator` for high-value 3D assets such as characters, creatures, vehicles, buildings, weapons, hero props, pickups, bosses, rigging, animation, texture, and conversion when procedural code is not enough.
- Use `threejs-audio-generator` for SFX, ambience loops, UI sounds, voice, conversion, and cleanup when generated audio would improve the playable loop.
- If trigger surfaces exist, complete the external asset sourcing phase before deciding procedural code is enough.
- Build authored forms with bevels, extrusions, curves, tubes, lathes, custom geometry, decals, trim, panel lines, repeated detail via instancing, and collision proxies.
- Add lighting, tone mapping, shadows/contact, fog/depth, post-processing, and bloom only after the authored forms exist.

Exit evidence:

- Before/after scorecard.
- Filled categories from `visual-scorecard.md`: Art direction, Hero/player, Obstacles/enemies, Rewards/interactables, World/environment, Materials/textures, Lighting/render, VFX/motion, UI/HUD, Performance evidence.
- Average score and automatic failures remaining.
- Active desktop and mobile screenshots.
- Renderer diagnostics: calls, triangles, geometries, textures, and material count when possible.
- Imported asset diagnostics when generated 3D was used: task IDs, file paths, file size, scale/bounds, collision proxy, animation clips, triangles/materials/textures when possible.
- No scorecard category below 2 for premium claims.

## Phase 5: UI

Use when HUD/menu/interface craft affects quality or readability.

- Inventory gameplay, pause, settings, fail/retry, milestone/win, loading/error, and touch states.
- Replace utility stat-card grids with game-specific meters, compact clusters, icons, badges, alerts, cooldown rings, reticles, diegetic labels, and stateful overlays.
- Use stable dimensions, safe-area padding, fixed-width numeric fields, text fit, and responsive constraints.
- Wire UI to game state. Avoid duplicated game rules inside UI code.
- Ensure UI never blocks the player, threats, pickups, next decision, or critical touch controls.

Exit evidence:

- Desktop and mobile screenshots for relevant states.
- Text-fit and overlap check.
- Touch target and safe-area check when mobile is in scope.
- UI checklist outcomes are reported.

## Phase 6: Debug And Profile

Use whenever the canvas is blank/broken, interaction fails, mobile behavior breaks, or visual changes add cost.

- Reproduce locally and read console/page/network errors.
- Check canvas CSS size and drawing-buffer size, renderer/context, loop ownership, camera, near/far, lights, fog, transforms, materials, loaders, asset paths, and resize behavior.
- For performance, measure production preview where possible: FPS/frame time, draw calls, triangles, geometries, materials, textures, memory, bundle, and expensive post/shadows.
- Optimize one bottleneck at a time using instancing, shared resources, culling, LOD, pooling, adaptive DPR, cheaper shadows/post, and explicit disposal.

Exit evidence:

- Root cause or measured bottleneck stated.
- Baseline/post metrics when optimizing.
- Broken path retested.

## Phase 7: QA And Release

Use before calling broad work complete.

- Run build/typecheck.
- Start dev or preview server and open the correct URL.
- Check console/page/network errors.
- Capture active desktop and mobile screenshots.
- Sample canvas pixels for nonblank and varied output.
- Use the generated game's `npm run inspect:canvas` when available, or the QA skill's packaged inspector:

```bash
node <threejs-qa-release-skill-dir>/scripts/inspect-threejs-canvas.mjs --url http://127.0.0.1:5188
```

- Trigger main input, objective progression, fail/retry, and recent risky paths.
- Verify HUD text fit, safe areas, touch targets, resize, and mobile input.
- For release, verify production preview, base path, static assets, debug gating, bundle/large assets, and deployment assumptions.

Exit evidence:

- Commands run and pass/fail.
- URL used.
- Screenshots/artifact paths.
- Issues fixed or listed with likely owners.
- Residual risks.

## Completion Gate

For premium/AAA/showcase claims, all of these must be true:

- Skill-loading ledger and reference ledger are present.
- External asset sourcing ledger is present for premium/AAA/showcase graphics work.
- Credential probe output plus external output evidence or blocker evidence is present for premium asset-category claims.
- Playable loop works through real input.
- Active-play screenshots exist for desktop and mobile.
- Visual scorecard has no category below 2 and average is at least 2.3.
- Visual scorecard uses the authored rubric, not an improvised rubric.
- HUD/menu states are readable and responsive.
- Renderer diagnostics exist after graphics changes.
- Build and browser QA passed or blockers are clearly reported.
- Physics-heavy games include engine choice, timestep, collider strategy, sensors, CCD use, and body/collider diagnostics.

If any gate fails, continue iterating or report the exact blocker instead of calling the game premium.
