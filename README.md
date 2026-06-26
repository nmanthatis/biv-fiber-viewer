# Interactive BiV fiber viewer

Rotatable 3D of the rule-based myocardial fibers at end-diastole, colored by:
- `fibers_stretch.html` — fiber stretch λf (blue = slack, red = engaged; HO fibers are tension-only)
- `fibers_stress.html` — fiber Cauchy stress σf (the load the fibers carry)

Each `.html` is a small `<model-viewer>` page that loads its sibling `.glb`
(~94 MB, binary glTF, ~1400 uniform full-length fibers). Drag to rotate, scroll to zoom.

## View locally
Browsers block the `file://` fetch of the `.glb` (CORS), so **don't double-click** —
serve the folder instead:
```bash
../view_fibers.sh stretch       # or: stress
# or manually:  python3 -m http.server 8000   then open http://localhost:8000/fibers_stretch.html
```

## Host on GitHub (anyone opens it in a browser, no install)
1. Commit this `web/` folder (each `.glb` is < GitHub's 100 MiB limit — commit normally, **not** Git LFS; Pages does not serve LFS files).
2. Repo **Settings → Pages** → Source: your branch, folder `/` (root).
3. Share: `https://<user>.github.io/<repo>/web/fibers_stretch.html`

The `model-viewer` script loads from a CDN, so viewers need internet (they do, to reach the page).
For a fully offline file, regenerate with `export_interactive.py --vendor <local model-viewer.min.js>`.

Regenerate: `PYTHONNOUSERSITE=1 ../.venv/bin/python ../export_interactive.py --vtk ../fibers_stretch.vtk --scalar stretch --external --out fibers_stretch` (see `--spacing` for density).
