# Three.js QA/Release Prompt Templates

Reusable prompt templates packaged with this skill. Use only templates relevant to the current request, and adapt placeholders to the game/project context.

---

# Release Pass Prompt

Use `threejs-qa-release` to prepare this Three.js game for release.

Release target:
- static host, GitHub Pages, Netlify, Vercel, itch.io, or other:

Requirements:
- Run production build and preview.
- Verify asset paths under the intended base path.
- Check bundle size and large assets.
- Run desktop and mobile visual QA.
- Confirm no debug-only UI leaks unless intentionally enabled.
- Produce final report with commands, artifacts, screenshots, and residual risks.
