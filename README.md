# learndutch-scripts

Custom JavaScript for the Learn Dutch with Kim Webflow site. Replaces Slater project 15512.

- `staging.js` loads on `learndutch.webflow.io`
- `index.js` loads on `learndutchwithkim.com`
- `webflow-loader.html` is the snippet in the Webflow site footer that picks between them

Both are served by GitHub Pages from the `main` branch.

## Workflow

1. Edit `staging.js`, run `npm run check`, commit and push.
2. Wait about a minute, refresh the webflow.io page and test.
3. To release: `npm run diff` to review, `npm run promote`, commit `index.js` and push. Production updates within about 10 minutes.

To roll back production, revert the last commit that touched `index.js` and push.
