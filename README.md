PartForge

Designed by Ishaan Bhutda · LinkedIn

PartForge is a little gear workshop that lives in your browser. You type in a few
numbers, watch the part take shape in 3D, and download an STL you can drop straight
into a slicer or CAD program. No installs, no accounts, no sign-ups — it's one HTML
file that does all the maths and 3D rendering on its own.

I built it because I kept rewriting the same gear equations in MATLAB every time I
wanted to print something, and I wanted a faster way to go from "I need a 19:1 reducer"
to "here's the STL on the print bed." If it saves you that same hassle, brilliant.

👉 Try it live — (once you turn on GitHub Pages, paste your link here)


What it makes

PartForge has three tabs, each for a different kind of part.

Single Gear — spur, helical, and herringbone gears with proper involute teeth.
Set the number of teeth, the module, pressure angle, face width, and bore, and (for
helical/herringbone) the helix angle. The teeth are real involute profiles, not
approximations, so they actually mesh.

Planetary — tell it the reduction ratio you want and how many planets, and it
works out the tooth counts for you. It sizes the sun, the planets, and the internal
ring gear so everything meshes and the planets are evenly spaced, then shows you the
exact ratio it landed on. You can export the whole assembly or any single gear.

Cycloidal — a cycloidal disc, the heart of a cycloidal drive. This is the one I
care about most, because the disc profile comes straight from the parametric equations
below. Set the reduction ratio, the pin-circle and pin sizes, the eccentricity, and the
output-pin holes, and it draws the lobed disc for you. It also checks the maths: if your
numbers would produce a self-overlapping or undercut shape that won't actually work, it
tells you, and it shows the valid range for each value so you can dial it in.

Every part can be exported two ways:


Download STL — the exact, nominal geometry.
3D-print STL — the same part with printing clearances baked in: the bore is
opened up a touch so it slides onto a shaft, and the outer teeth/lobes are trimmed
slightly so meshing parts don't bind. You set those clearances in the box on the left.
