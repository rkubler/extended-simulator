# Extended Shot Peening Coverage Simulator

**Dr Régis Kubler**, Arts et Métiers Institute of Technology
*Developed with the assistance of Claude Opus 5.5 (Anthropic), November 2026*

**User guide (PDF):** [extended_simulator_guide.pdf](docs/extended_simulator_guide.pdf), online at https://rkubler.github.io/extended-simulator/docs/extended_simulator_guide.pdf. LaTeX sources in [`docs/`](docs/).

![Shot peening process: media flow rate ṁ, jet size ΔX, feed V (sizes not to scale)](shot_peening_process.gif)

Interactive educational tool extending the shot peening coverage model to
**raster paths**: the nozzle sweeps the part along parallel lines, back and
forth, with a **step δ** between lines. With a jet of width ΔX, each point is
crossed by ΔX/δ lines on average, and the number of impacts can vary from
line to line in **stripes**.

**▶ Live simulator:** https://rkubler.github.io/extended-simulator/

## What the simulator shows
- Animated map of the part: raster path, jet footprint, local coverage or impacts per point
- Cross-section across the lines: coverage τ(y) and impacts per point λ(y), showing stripes
- Mean, minimum and maximum coverage in the central zone, stripe amplitude
- Coverage versus number of rasters: simulation, stripe-corrected model and average model
- One-raster coverage versus step δ
- Crossed rasters at 0° and 90°: λ(x,y) = λ₀(y) + λ₉₀(x), mean coverage 1 − mean(e^(−λ₀))·mean(e^(−λ₉₀))
- Rasters and time needed to reach 98 % coverage

An information page on the jet profile (uniform, Gaussian and flattened Gaussian, equations,
overlap of neighbouring lines) opens from the ⓘ button next to the jet
profile setting: [jet_profile.html](https://rkubler.github.io/extended-simulator/jet_profile.html).

Parameters (sliders or typed values): media flow rate, density, shot size
(log-normal spread), dent radius, jet size ΔX, jet profile (uniform,
Gaussian or flattened Gaussian with exponent p), traverse speed V, step δ, number of rasters at 0° (horizontal lines)
and at 90° (vertical lines), order of the rasters (alternate or 0° first), half-step
offset between rasters, part length and width.

## Model
- Shots per second: Ṅ = ṁ / m̄ₚ, with m̄ₚ = ρ·π/6·E[D³]
- Area of one dent: a = π·E[r²]
- Single line (δ = ΔX): K = a·Ṅ / (V·ΔX), the original model
- Raster with step δ, average: K_δ = a·Ṅ / (V·δ) = K·ΔX/δ
- Local impacts per point: λ(y) = a·(Ṅ/V)·Σ g(y − y_j), g = jet profile across the line
- Local coverage: τ = 1 − e^(−λ); stripes always lower the mean coverage
- Uniform jet: τ = 1 − (1−f)·e^(−K·m₀·n) − f·e^(−K·(m₀+1)·n), m₀ = ⌊ΔX/δ⌋, f = ΔX/δ − m₀
- Gaussian jet (σⱼ = ΔX/4): stripe amplitude ≈ 4·e^(−2π²(σⱼ/δ)²), negligible for δ ≤ ΔX/2
- Flattened Gaussian g ∝ e^(−|u/w|^p), w = (ΔX/2)/2^(1/p): p = 2 is the Gaussian, large p tends to the uniform jet; stripes computed numerically


## Coverage above 100 % (NF L 06-832)

The base time is the peening time needed to dent 98 % of the surface. Full coverage (100 %) is 1.25 × the base time (an option sets it to the base time instead), and 200 % or 300 % means 2 or 3 times the time of full coverage. On an even random treatment, full coverage corresponds to λ = 1.25·ln 50 = 4.89 impacts per point on average (99.25 % dented). Coverage itself is always the dented area divided by the total area. The readout "Coverage (NF L 06-832)" combines both: it is the dented area up to the base time t_b (98 %), goes from 98 % to 100 % between t_b and 1.25·t_b, and is 100·t / (1.25·t_b) above (200 % = twice the time of full coverage).

## Use
Open the live link above, or download `index.html` and open it in any web
browser (works offline; no installation needed).

## Limitations
Educational mean-field model: the map shows the expected number of impacts
per point, and random impacts give the local coverage 1 − e^(−λ). Constant
traverse speed, jet firing during turnarounds outside the part, flat
surface, normal incidence. It does not replace coverage verification
according to the applicable standards (e.g. SAE J2277).

## Related tools
- Shot Peening Coverage Simulator: https://rkubler.github.io/peening-coverage/
- Piezopeening Coverage Simulator: https://rkubler.github.io/piezopeening-coverage/

## Author and acknowledgement
Dr Régis Kubler, Arts et Métiers Institute of Technology.
The simulator was developed with the assistance of Claude Opus 5.5 (Anthropic),
November 2026. All content was reviewed by the author.

## Licence
Code: MIT, see [LICENSE](LICENSE). Documentation: CC BY 4.0.

## Cite as
Kubler, R. (2026). *Extended Shot Peening Coverage Simulator*. Arts et Métiers Institute of Technology. Zenodo. DOI: [to add]

## Versions

- 2.3 (22 November 2026): export of every figure as a PNG image (as shown at that instant) and of the data of every chart, map and table as a CSV file.
- 2.2 (22 November 2026): the stripe-corrected model is averaged over the central zone of the part (the same surface as the map), so the base time and all the times are consistent with the simulated coverage; checked against an independent computation.
- 2.1 (22 November 2026): angle ψ tilting the nozzle plane across the path (cos γ = cos θ·cos ψ, jet ΔX/cos ψ wide across the lines, smoother stripes); front view of the nozzles across the line.
- 2.0 (22 November 2026): side view of the nozzles along the current line, with their angles to the normal, the jets, the footprints and the direction of travel.
- 1.9 (22 November 2026): option for 2 nozzles in the same plane, aimed at the same point, at angles θ₁ ≥ 0 and θ₂ ≤ 0 (flow rate per nozzle); K = K₀·[f(θ₁) + f(θ₂)].
- 1.8 (22 November 2026): nozzle angle θ from the normal (0 to 60°, tilted in the plane of the path and the normal) and dent-area law a = a₀·cos θ or a₀·cos²θ; the footprint is ΔX/cos θ long along the path.
- 1.7 (18 November 2026): readout "Min / max coverage (NF L 06-832)", which can exceed 100 %.
- 1.6 (18 November 2026): local coverage (NF L 06-832) of each point, above 100 %, in the hover readout and as a map mode.
- 1.5 (18 November 2026): new readout "Coverage (NF L 06-832)", which can exceed 100 %.
- 1.4 (18 November 2026): coverage-level readouts and map removed; coverage is the dented area divided by the total area.
- 1.3 (18 November 2026): coverage above 100 % (NF L 06-832): specified coverage, base time, 1.25 factor option.
- 1.2 (18 November 2026): flattened Gaussian jet profile with exponent p, on the simulator and the jet profile page.
- 1.1 (17 November 2026): rasters at 0° and 90°, choice of raster order, horizontal or vertical cross-section.
- 1.0 (17 November 2026): first release.
