# PartForge

**Designed by Ishaan Bhutda** · [LinkedIn](https://www.linkedin.com/in/ishaanbhutda/)

PartForge is a little gear workshop that lives in your browser. You type in a few
numbers, watch the part take shape in 3D, and download an STL you can drop straight
into a slicer or CAD program. No installs, no accounts, no sign-ups — it's one HTML
file that does all the maths and 3D rendering on its own.

I built it because I kept rewriting the same gear equations in MATLAB every time I
wanted to print something, and I wanted a faster way to go from "I need a 19:1 reducer"
to "here's the STL on the print bed." If it saves you that same hassle, brilliant.

👉 **[Try it Live!](https://www.linkedin.com/in/ishaanbhutda/)**

---

## What it makes

PartForge has three tabs, each for a different kind of part.

**Single Gear** — spur, helical, and herringbone gears with proper involute teeth.
Set the number of teeth, the module, pressure angle, face width, and bore, and (for
helical/herringbone) the helix angle. The teeth are real involute profiles, not
approximations, so they actually mesh.

**Planetary** — tell it the reduction ratio you want and how many planets, and it
works out the tooth counts for you. It sizes the sun, the planets, and the internal
ring gear so everything meshes and the planets are evenly spaced, then shows you the
exact ratio it landed on. You can export the whole assembly or any single gear.

**Cycloidal** — a cycloidal disc, the heart of a cycloidal drive. This is the one I
care about most, because the disc profile comes straight from the parametric equations
below. Set the reduction ratio, the pin-circle and pin sizes, the eccentricity, and the
output-pin holes, and it draws the lobed disc for you. It also checks the maths: if your
numbers would produce a self-overlapping or undercut shape that won't actually work, it
tells you, and it shows the valid range for each value so you can dial it in.

Every part can be exported two ways:

- **Download STL** — the exact, nominal geometry.
- **3D-print STL** — the same part with printing clearances baked in: the bore is
  opened up a touch so it slides onto a shaft, and the outer teeth/lobes are trimmed
  slightly so meshing parts don't bind. You set those clearances in the box on the left.

---

## Cycloidal disc — the MATLAB generator

The cycloidal disc is built from this parametric script. It's the same maths the website
runs internally, so you can sketch a profile in MATLAB and reproduce it exactly in PartForge.

```matlab
R = 40;                 % pin-circle radius  (D/2)
r = 4;                  % pin radius         (d/2)
Gear_ratio = 19;        % reduction ratio
N = Gear_ratio + 1;     % number of pins  (the disc has N-1 lobes)
e = 1.5;                % eccentricity

syms t
x(t) =  R*cos(t) - r*cos(t + atan( sin((N-1)*t) / (cos((N-1)*t) - (R/(N*e))) )) - e*cos(N*t);
y(t) = -R*sin(t) + r*sin(t + atan( sin((N-1)*t) / (cos((N-1)*t) - (R/(N*e))) )) + e*sin(N*t);

x(t), y(t)

t = linspace(0, 2*pi, 5000);
plot(x(t), y(t))
axis equal
```

Reduction ratio is `N - 1`, and eccentricity `e` sets how deep the lobes are — turn it
up too high and the lobes overlap and the shape stops being printable (PartForge catches
this for you). One quiet gotcha: it's single-argument `atan`, not `atan2` — they differ
by π when the denominator goes negative, which changes the whole curve.

---

## How to use it

1. Open `index.html` (or the live link).
2. Pick a tab — **Single Gear**, **Planetary**, or **Cycloidal**.
3. Type your numbers. The 3D view updates as you go. On the Cycloidal tab, stay inside
   the little grey ranges under each box — if it turns red, ease the value back.
4. Drag to spin it around, scroll to zoom.
5. Hit **Download STL** for the exact part, or **3D-print STL** for the print-ready one.
6. Open it in your slicer or CAD and go.

New here? The Cycloidal tab opens on my actual printed 19:1 disc — just hit **3D-print
STL** and you've got something on the bed in one click.

---

## Where this is going

This is very much a living project, and honestly I'm having a lot of fun with it. I'd
love to keep growing PartForge — more part types (bevel gears, racks, splines), proper
STEP solid exports, full cycloidal-drive assemblies, maybe gear-train design end to end.

If you use it, break it, or have an idea for it, I'm all ears — open an issue, send a PR,
or reach out on [LinkedIn](https://www.linkedin.com/in/ishaanbhutda/). And if you print
something with it, I'd genuinely love to see it. More to come. 🛠️
