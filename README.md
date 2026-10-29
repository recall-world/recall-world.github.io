# RecallOcc

A self-contained static project page for RecallOcc.

## Run locally

```powershell
python -m http.server 4173 --bind 127.0.0.1
```

Open `http://127.0.0.1:4173/`.

## Validate

```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File tests/validate-assets.ps1
pwsh -NoProfile -ExecutionPolicy Bypass -File tests/validate-markup.ps1
pwsh -NoProfile -ExecutionPolicy Bypass -File tests/validate-presentation.ps1
pwsh -NoProfile -ExecutionPolicy Bypass -File tests/validate-runtime.ps1
node --test tests/validate-behavior.mjs
node tests/validate-runtime-guard.mjs
node tests/validate-browser.mjs
```

Run these commands from this directory. The PowerShell validators require PowerShell 7 (`pwsh`), and runtime validation requires Python. Stop the local server before runtime validation or its occupied-port regression check: they require port 4173 to be free and clean up their own listeners.

The browser check requires Node.js 22+ and Microsoft Edge installed at `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe` (override with the `EDGE_PATH` environment variable). It launches its own temporary local server and isolated headless Edge profile, checks desktop/mobile interactions and video failure handling, then cleans them up. It uses only Node's built-in modules; no package installation or build is needed.

Screenshots and `browser-results.json` are written outside this repository to `../../work/verification/recall-world-final`. To choose another evidence directory outside the repository:

```powershell
node tests/validate-browser.mjs 'C:\path\to\verification'
```
