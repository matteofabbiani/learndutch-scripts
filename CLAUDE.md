# learndutch-scripts

Custom JS for the Learn Dutch with Kim Webflow site (`learndutchwithkim.com`), served by GitHub Pages from `main`.

| File | Loaded on | URL |
|---|---|---|
| `staging.js` | `learndutch.webflow.io` | `https://matteofabbiani.github.io/learndutch-scripts/staging.js` |
| `index.js` | production domains | `https://matteofabbiani.github.io/learndutch-scripts/index.js` |

## ⛔ Strict rule

- Editing and pushing `staging.js` → **staging only**. Safe default.
- Changing `index.js` in any way (`npm run promote`, a direct edit, a revert) and pushing it → **PRODUCTION**, live for all visitors within ~10 minutes. **Never without the user's explicit permission, given per release in the current conversation.** "Deploy", "push", "save", "update the code" all mean STAGING ONLY. One approval covers one release.
- Never stage `index.js` in a commit by accident: commit with explicit paths, not `git add -A`.
- The same per-action permission applies to publishing Webflow to the production domains.

## Working notes

- Every edit goes into `staging.js` first; run `npm run check` before pushing. Pages rebuilds in about a minute; the staging loader adds a timestamp so no cache applies.
- Production is cached for 10 minutes by GitHub Pages (not configurable). A rollback takes the same time to reach returning visitors.
- The code expects these globals, loaded before it: `gsap`, `ScrollTrigger`, `SplitText`, `CustomEase`, `Draggable` (by Webflow) and `Swiper` (script tag in the site footer, above the loader).
- The file is loaded after `DOMContentLoaded`: code added here must not wait for that event (use a `document.readyState` check).
- The about block at the end of the file is gated by path, copied from the Slater loader. Its code does not check for its own elements, so keep the gate.
- The last block of the file is the cookie consent module (Google advanced consent mode). The default consent state is set in the Webflow site head code from `localStorage` key `ldk-consent`; this module shows the "Cookie Banner" component, sends the consent update on Accept/Decline and asks again 30 days after a decline. Test with `qa/consent-test.mjs` in the project folder.
- CSS stays in Webflow embeds. Class and attribute names the scripts toggle (`is-opened`, `is-activated`, `swiper-dragging`, `line-mask`, `eyebrow-text-mask`, …) are styled there; do not rename them.
- `webflow-loader.html` is the copy of the snippet in Webflow → Site settings → Custom code → Footer.
