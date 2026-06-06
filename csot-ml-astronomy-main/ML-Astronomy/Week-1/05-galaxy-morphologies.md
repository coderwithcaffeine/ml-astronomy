# 05 — Galaxy Morphologies: What You Actually See

> The tuning fork gives us labels. This page gives us the *intuition* — what each class looks like in real survey imagery, what physical process produces that appearance, and where the boundaries between classes blur.

> All images linked below come from public NASA / ESA / NOIRLab / SDSS image archives. We **link** to them rather than embedding to keep this repo lightweight; click through to see them in full resolution.

---

## Ellipticals (E)

A **smooth, featureless ball or oval of light**, brightest in the centre and fading gradually outwards.

**Visual signatures**
- No spiral arms, no disk, no dust lanes.
- Light profile is smooth — if you sketch contours of constant brightness (*isophotes*, which we'll formalise in Week 2), they're nested ellipses.
- Colour is typically **yellow-to-red** in true-colour imagery.

**Physical story**
- *Pressure-supported* — stars orbit on random, near-isotropic paths, like bees around a hive. No coherent rotation.
- Dominated by **old, low-mass stars**, with very little cold gas.
- Star formation is largely *quenched* — they are "red and dead".
- Many ellipticals appear to be the end products of **major mergers** of two spirals.
- Common in dense environments like the cores of galaxy clusters.

**Where to look**
- **M87** (Virgo cluster) — the supermassive black hole imaged by Event Horizon Telescope sits in its centre. [Hubble image](https://esahubble.org/images/opo0010c/).
- **M49**, **M60**, **NGC 1399** — other classic giant ellipticals.

---

## Spirals (S, SB)

A **flat rotating disk** with arms wound around a central **bulge**. If a straight bar of stars crosses the centre, the galaxy is *barred* (SB).

**Visual signatures**
- Distinct spiral arms (sometimes only 2, sometimes many, sometimes flocculent).
- A bright central bulge (size varies between Sa → Sc).
- **Dust lanes**: dark threads silhouetted against the disk, where dense gas blocks starlight.
- Bright blue spots and pink patches along the arms — sites of recent and ongoing star formation.

**Physical story**
- *Rotation-supported* — stars and gas orbit coherently in a thin disk.
- The arms are **density waves**, not rigid structures (more on this in Week 3).
- Lots of cold gas and dust → ongoing star formation → blue, hot, short-lived stars trace the arms.
- The bulge is older and redder; the disk is younger and bluer.
- **Bars** are common (~⅔ of nearby disk galaxies, including ours) and act as engines that funnel gas inward.

**Where to look**
- **M31 (Andromeda)** — nearest large spiral, naked-eye-visible. [NASA/Galex composite](https://www.nasa.gov/centers-and-facilities/jpl/galex-finds-link-between-black-holes-and-galaxy-formation/).
- **M51 (Whirlpool)** — textbook grand-design spiral. [Hubble image](https://esahubble.org/images/heic0506a/).
- **NGC 1300** — beautiful barred spiral. [Hubble image](https://esahubble.org/images/heic0501a/).
- **The Milky Way** — barred spiral, ~SBbc, ~100 000 light-years across. We live ~26 000 ly from its centre.

---

## Lenticulars (S0) — The Bridge

Lenticulars are the **identity crisis of the Hubble sequence**. They have:

- a disk (like a spiral)
- a bulge (sometimes large, like an elliptical)
- **but no spiral arms**

**Visual signatures**
- Smooth disk that looks elliptical from face-on, but clearly lens-shaped (hence "lenticular") when seen from the side.
- Often little to no visible dust or star-forming patches.
- Edge-on lenticulars are easy to spot (a featureless thin lens). Face-on ones often get mis-classified as ellipticals.

**Physical story**
- Generally thought to be **former spirals that have lost or used up their cold gas**, possibly through:
  - **Ram-pressure stripping** while moving through hot intracluster gas, or
  - **Starvation** as gas accretion is cut off, or
  - **Mergers** that disrupted the disk.
- Common in galaxy groups and the outskirts of clusters.

> **Why this matters for our project:** S0s sit *exactly* on the visual decision boundary between ellipticals and spirals. They are notoriously hard to classify — even for humans — and will likely be the dominant source of confusion in our CNN's confusion matrix in Week 3.

**Where to look**
- **NGC 5866** (sometimes called the Spindle Galaxy) — striking edge-on S0 with a dust lane. [Hubble image](https://esahubble.org/images/heic0604a/).

---

## Irregulars (Irr)

Galaxies that simply do not fit the orderly classes above.

**Visual signatures**
- Chaotic, asymmetric shapes.
- Sometimes recognisable "leftover" disk or arm structure being torn apart.
- Often *very* blue, with intense pockets of star formation.

**Physical story**
- Many are **tidal interactions** or **mid-merger snapshots**: two galaxies passing through each other, throwing off streams of stars and gas.
- Mergers funnel cold gas inward, triggering bursts of star formation (*starbursts*).
- Some irregulars are intrinsically clumpy — common at high redshift, when the universe was younger and gas-richer.
- Many dwarf galaxies are irregulars.

**Where to look**
- **Large Magellanic Cloud (LMC)** and **Small Magellanic Cloud (SMC)** — Milky Way satellite irregulars, naked-eye visible from the southern hemisphere.
- **The Antennae (NGC 4038/4039)** — a textbook mid-merger between two spirals. [Hubble image](https://esahubble.org/images/heic0615a/).
- **M82 (Cigar Galaxy)** — heavily disturbed by interaction with M81, hosts a powerful starburst. [Hubble image](https://esahubble.org/images/heic0604a/).

---

## What Makes a Galaxy Look the Way It Does?

A handful of physical knobs explain most of the visual differences:

| Knob | Effect on appearance |
|---|---|
| **Cold gas content** | More gas → more star formation → bluer colour, lumpier appearance. |
| **Angular momentum** | High angular momentum → disk forms. Low → spheroid. |
| **Recent merger history** | Recent merger → disturbed, asymmetric, often starbursting. |
| **Stellar age distribution** | Old populations → red. Young populations → blue. |
| **Dust content** | More dust → more reddening + visible dust lanes. |
| **Viewing angle** | Edge-on vs face-on can hide or reveal arms, bars, and dust. |

Morphology is therefore the **2D projection of a 3D system shaped by these physical processes**. Our CNN will learn the projection statistics; understanding the physics is what makes us better than the network at interpreting its mistakes.

---

## Beware: Things That Look Weird

- **Edge-on spirals** can be mistaken for cigar-shaped ellipticals if you ignore the dust lane.
- **Face-on lenticulars** look almost identical to face-on ellipticals.
- **Foreground stars** in our own galaxy often sit on top of background galaxy images and confuse both humans and CNNs.
- **Image artefacts** (cosmic ray hits, satellite trails, diffraction spikes) can mimic real morphological features.
- **Distance / resolution.** A galaxy too far away may look like a featureless blob even if it's a beautiful spiral up close.

A robust ML pipeline has to deal with all of these. We'll see how transforms (Week 1, Part 2) and validation (Week 3) help.

---

## Self-Check: Classify These

Open each link and decide for yourself: **E, S, SB, S0, or Irr?** Answers are hidden below.

1. [Image A — M104 (Sombrero Galaxy)](https://esahubble.org/images/opo0328a/)
2. [Image B — M87](https://esahubble.org/images/opo0010c/)
3. [Image C — NGC 1300](https://esahubble.org/images/heic0501a/)
4. [Image D — The Antennae](https://esahubble.org/images/heic0615a/)
5. [Image E — NGC 5866](https://esahubble.org/images/heic0604a/)

<details>
<summary>Answers</summary>

1. **Sa** — spiral, very prominent bulge, almost edge-on, gorgeous dust lane.
2. **E** — giant elliptical, smooth featureless light profile (note the jet — that's the central supermassive black hole, not morphology).
3. **SBb** — textbook barred spiral, prominent bar feeding into two open arms.
4. **Irr / Merger** — two spirals mid-collision.
5. **S0** — lenticular: a clear disk and dust lane, but no spiral arms.

</details>

---

## External Resources

- 🌌 [SDSS SkyServer Image Gallery](https://skyserver.sdss.org/dr18/en/tools/explore/summary.aspx) — browse real survey imagery the same data Galaxy Zoo used.
- 🌌 [Galaxy Zoo classification tutorial](https://www.zooniverse.org/projects/zookeeper/galaxy-zoo/classify) — try classifying galaxies the way humans label our dataset.
- 🖼️ [ESA/Hubble image archive — Galaxies](https://esahubble.org/images/archive/category/galaxies/).
- 🖼️ [NASA Astronomy Picture of the Day archive](https://apod.nasa.gov/apod/archivepix.html) — endless galaxy eye-candy with expert captions.
- 📘 [Las Cumbres Observatory — Spacebook on Galaxies](https://lco.global/spacebook/galaxies/).
- 📺 [Dr. Becky — playlists on galaxies](https://www.youtube.com/@DrBecky/playlists) — accessible, professionally accurate.
- 📺 [PBS Space Time — Why Do Galaxies Have Spiral Arms?](https://www.youtube.com/watch?v=ldRsHPnL0RM).
- 📄 [Conselice 2014 — The Evolution of Galaxy Structure (Annual Review, arXiv)](https://arxiv.org/abs/1403.2783) — for if you want to go deep.

---

⬅️ Previous: [`04-hubble-tuning-fork.md`](04-hubble-tuning-fork.md) | ➡️ Next: [`06-how-telescopes-see.md`](06-how-telescopes-see.md)
