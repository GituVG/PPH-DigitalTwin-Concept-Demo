[README.md](https://github.com/user-attachments/files/31978051/README.md)
# Female Digital Health Twin — PPH Risk Demo

An interactive, static web demo showing how a **longitudinal Female Digital
Health Twin** could be built for postpartum hemorrhage (PPH) risk modeling —
integrating antepartum, intrapartum, immediate postpartum, and extended
postpartum data into one continuously evolving risk picture, rather than a
single-timepoint assessment.

Built to accompany the *Female Digital Health Twin Global Alliance (FDHT-GA)*
work from the VIHAR Center & PRoBE Lab, University of Pittsburgh.

**Live demo:** once hosted (see below), your app will be at
`https://<your-username>.github.io/<repo-name>/`

## What's inside

Three interactive modes, plus an overview:

- **Explorer** — adjust variables across all four clinical windows and watch
  a composite risk score respond live, with a breakdown of which factors are
  driving it.
- **Scenarios** — five preset patient vignettes. Read the case, predict the
  risk tier, then reveal the underlying data to check your instinct against
  the model.
- **Time-lapse** — watch a single patient's risk score build step by step as
  clinical data "arrives" chronologically across the four windows, including
  the cell-free mitochondrial DNA (mtDNA) biomarker from the extended
  postpartum window.

## Important note on the model

The scoring logic in `js/scoring.js` is a **simplified, illustrative
weighting** of clinically-informed risk factors, built to demonstrate the
four-window digital twin concept. **It is not a statistically fit or
validated clinical instrument**, and should not be used for patient care or
presented as such. It's intended for teaching, internal discussion, and
grant/pitch demonstrations.

## Running locally

No build step, no dependencies. Just open `index.html` in a browser, or serve
the folder locally:

```bash
# Python 3
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Hosting on GitHub Pages

1. Create a new GitHub repository and push this folder's contents to it
   (commit `index.html`, `css/`, `js/` at the repo root):
   ```bash
   git init
   git add .
   git commit -m "Initial commit: FDHT-GA PPH demo"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch."
4. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
5. GitHub will publish the site within a minute or two at
   `https://<your-username>.github.io/<repo-name>/`.

No server-side code or database is required — everything runs client-side in
the browser.

## File structure

```
index.html          Page shell, nav, and section markup
css/style.css        All styling and design tokens
js/data.js           Window definitions, explorer controls, scenario presets
js/scoring.js        The 22-factor scoring engine (single source of truth)
js/explorer.js       Explorer mode
js/scenarios.js      Scenario quiz mode
js/timelapse.js      Time-lapse animation mode
js/app.js            Navigation + hero animation wiring
```

## Extending this demo

- **Add scenarios:** append an entry to `SCENARIOS` in `js/data.js` with a
  `title`, `vignette`, and a `vals` object covering every id in `VARIABLES`.
- **Adjust the model:** edit the `calc` function on any entry in
  `FACTOR_DEFS` in `js/scoring.js`. All three modes read from this one list,
  so changes propagate everywhere automatically.
- **Add a new window or variable:** add it to `WINDOWS`/`VARIABLES` in
  `js/data.js`, add a matching `FACTOR_DEFS` entry in `js/scoring.js`, and add
  its default value to every scenario's `vals` object.

## License

MIT — see `LICENSE`. Free to adapt for teaching, grant materials, or further
prototyping toward the actual validated model described in the project's
Specific Aims.
