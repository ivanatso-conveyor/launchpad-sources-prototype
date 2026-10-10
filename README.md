# Launchpad · sources prototype

A static build of the Ask ConveyorAI palette on the Launchpad, for reviewing how an answer cites its sources: Memory facts, instructions and feedback alongside documents, Q&A pairs and past answers. Mock data, no API.

**Open it:** https://ivanatso-conveyor.github.io/launchpad-sources-prototype/

Open the palette from the Launchpad's question box or *Get an answer*. The **Inspector** in the corner switches **State** between *Production* (today's palette) and *Updated Design*, and plays a recorded run at real pace: scrub it, change its speed and length, choose how it ends, or jump straight to the answer. The Updated Design's **Sources** tab shows the *Final* rows.

## Source and rebuilding

Source lives in the `comply-ui` repo, branch `claude/memory-sources-prototype`, under `packages/app-sandbox/`. To run it locally there:

```bash
make dev-sandbox
```

To rebuild this site:

```bash
APP_PACKAGE=app-sandbox NODE_ENV=production ARTIFACT_OUT=/tmp/sandbox-site \
  node_modules/.bin/webpack --config webpack/artifact-sandbox.js
```

Then, in the output:

- copy `empty-states/`, `ai/`, the two `.ttf` fonts, `conveyor-favicon.ico` and the two avatar `.jpeg` files from `public/`
- in `index.html`, set the title, drop the `status.conveyor.com` script tag, and make the favicon path relative
- in the main bundle, make the `/empty-states/`, `/ai/conveyor-ai-wheel` and avatar paths relative (`./…`), and in the main stylesheet point the font `url()`s at `../`, since the site is served below the domain root
- swap the `@conveyor.com` people addresses in the main bundle for `@example.com`
