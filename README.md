# PartForge

**Designed by Ishaan Bhutda** · [LinkedIn](https://www.linkedin.com/in/ishaanbhutda/)

A self-contained, in-browser **parametric gear & gearbox generator** with an earthy theme.
No build step, no dependencies, no server — a single `index.html` that renders 3D on a
plain `<canvas>` and exports STL.

**[▶ Live demo](#)** — _(enable GitHub Pages, then drop your URL here)_

## Features

- **Single Gear** — spur, helical, and herringbone gears with true involute tooth flanks,
  parametric module / teeth / pressure angle / face width / bore, and helical & herringbone twist.
- **Planetary Gearbox** — enter a target reduction ratio and number of planets; PartForge solves
  the sun / planet / ring tooth counts (ring fixed, carrier output, `i = 1 + R/S`) honouring the
  meshing constraints `R = S + 2P`, equal planet spacing, and the no-collision neighbour condition.
  Export the assembly or any single gear (sun, planet, internal ring).
- **Cycloidal Gearbox** — cycloidal disc generated directly from the parametric equations
  (see below); reduction ratio = pins − 1. Export the full drive or the disc on its own.
- **Two exports per part** — a nominal **STL**, and a **3D-print STL** that enlarges the bore and
  trims the OD / tooth thickness by user-set clearances for printable fits and backlash.
- Orbit (drag), zoom (scroll), spin, and reset.

## Cycloidal disc equation

The disc profile uses the standard cycloidal parametrisation (with `atan2` for quadrant safety):

```
R = D/2          % pin-circle radius
r = d/2          % pin radius
N                % number of ring pins   (lobes = N-1, ratio = N-1)
e                % eccentricity

psi(t) = atan2( sin((N-1)t),  cos((N-1)t) - R/(e*N) )
x(t)   =  R*cos(t) - r*cos(t + psi) - e*cos(N*t)
y(t)   = -R*sin(t) + r*sin(t + psi) + e*sin(N*t)
```

## Run locally

Just open `index.html` in any modern browser. That's it.

## Deploy on GitHub Pages

1. Create a repo and add `index.html` (and this `README.md`).
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pick `main` / root.
3. Your site appears at `https://<user>.github.io/<repo>/`.

## Notes & limits

- Exports are **STL meshes**, not STEP solids. For a precise B-rep STEP, use a CAD kernel.
- The planetary preview's planet meshing phase is cosmetic; individually exported gears are exact.
- Cycloidal output-pin holes are not modelled (centre bore only).

## License

MIT — do whatever you like.
