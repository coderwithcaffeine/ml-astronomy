# Week 1 — Curated Resources

> The links in each numbered concept markdown are the *minimum* set you need. This page gathers extras for the curious, organised by theme. Nothing here is required; everything here is good.

---

## PyTorch

### Official
- 📘 [PyTorch — Tensors tutorial](https://docs.pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html) — the one-page intro everyone should read.
- 📘 [PyTorch — Deep Learning with PyTorch: A 60-Minute Blitz](https://docs.pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html) — tensors, autograd, nn basics.
- 📘 [PyTorch documentation — tensors](https://docs.pytorch.org/docs/stable/tensors.html) — comprehensive API reference.
- 📘 [PyTorch documentation — CUDA semantics](https://docs.pytorch.org/docs/stable/notes/cuda.html) — required reading before debugging device issues.
- 📘 [PyTorch examples on GitHub](https://github.com/pytorch/examples) — official, tested example scripts.

### Friendlier intros
- 📺 [PyTorch tutorial — Patrick Loeber (free 4-hour course)](https://www.youtube.com/watch?v=c36lUUr864M).
- 📺 [PyTorch in 100 seconds — Fireship](https://www.youtube.com/watch?v=ORMx45xqWkA) for the absolute high-level pitch.
- 📘 [Daniel Bourke's "Learn PyTorch for Deep Learning"](https://www.learnpytorch.io/) — book + videos, beginner-friendly, free.
- 📘 [`pytorch-for-numpy-users` cheat sheet](https://github.com/wkentaro/pytorch-for-numpy-users) — invaluable if you already know NumPy.

### Reference books
- 📘 [Deep Learning with PyTorch — Eli Stevens, Luca Antiga, Thomas Viehmann (free PDF from Manning)](https://www.manning.com/books/deep-learning-with-pytorch).
- 📘 [d2l.ai — Dive into Deep Learning (PyTorch edition)](https://d2l.ai/) — interactive textbook with executable notebooks.

### Data pipelines (Part 2)
- 📘 [PyTorch — Datasets & DataLoaders tutorial](https://docs.pytorch.org/tutorials/beginner/basics/data_tutorial.html).
- 📘 [`torchvision.datasets.ImageFolder` docs](https://docs.pytorch.org/vision/stable/generated/torchvision.datasets.ImageFolder.html).
- 📘 [`torchvision.transforms` docs](https://docs.pytorch.org/vision/stable/transforms.html).
- 📘 [PyTorch — `DataLoader` API reference](https://docs.pytorch.org/docs/stable/data.html).
- 📘 [PyTorch — Writing custom datasets, dataloaders and transforms](https://docs.pytorch.org/tutorials/beginner/data_loading_tutorial.html).
- 📺 [PyTorch DataLoaders explained — Patrick Loeber](https://www.youtube.com/watch?v=PXOzkkB5eH0).
- 🌌 [Galaxy Zoo 2 Kaggle dataset (our dataset)](https://www.kaggle.com/datasets/jaimetrickz/galaxy-zoo-2-images) and the [Kaggle API docs](https://github.com/Kaggle/kaggle-api).

---

## Telescopes, CCDs & Detectors (Part 2)

- 📘 [SDSS — instruments and the photometric camera](https://www.sdss.org/instruments/).
- 📘 [Wikipedia — Charge-coupled device](https://en.wikipedia.org/wiki/Charge-coupled_device).
- 📘 [Las Cumbres Observatory — Telescopes & detectors](https://lco.global/spacebook/telescopes/) and [light & filters](https://lco.global/spacebook/light/).
- 📘 [SDSS — magnitudes and photometry](https://www.sdss.org/dr18/algorithms/magnitudes/).
- 📘 [Wikipedia — Photometric system](https://en.wikipedia.org/wiki/Photometric_system) and [Apparent magnitude](https://en.wikipedia.org/wiki/Apparent_magnitude).
- 📄 [Gunn et al. 1998 — The SDSS Photometric Camera (arXiv)](https://arxiv.org/abs/astro-ph/9809085).
- 📄 [Lupton et al. 2004 — Preparing RGB images from CCD data (arXiv)](https://arxiv.org/abs/astro-ph/0312483) — how SDSS colour images are made.
- 📺 [Crash Course Astronomy — Telescopes](https://www.youtube.com/watch?v=3HmF1JFFi-c).
- 📘 [Astropy — working with FITS files](https://docs.astropy.org/en/stable/io/fits/) — the format real astronomers use instead of JPGs.

---

## Google Colab

- 📘 [Welcome to Colab](https://colab.research.google.com/notebooks/welcome.ipynb).
- 📘 [Colab feature overview notebook](https://colab.research.google.com/notebooks/basic_features_overview.ipynb).
- 📘 [Colab FAQ](https://research.google.com/colaboratory/faq.html) — covers GPU availability, runtime limits, billing.
- 📘 [`colab-cheatsheet`](https://github.com/tugot17/Colab-Cheat-Sheet) — handy keyboard shortcut summary.

---

## Linear Algebra & Math Foundations

You will not need to derive backprop by hand, but you'll be far happier if you have visual intuition for vectors, matrices, and linear transformations.

- 📺 [3Blue1Brown — Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) — the gold standard.
- 📺 [3Blue1Brown — Neural Networks series](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — beautiful intuition for what a network *is*.
- 📺 [StatQuest — Neural Networks Clearly Explained](https://www.youtube.com/playlist?list=PLblh5JKOoLUIxGDQs4LFFD--41Vzf-ME1) — Josh Starmer's calm pace makes ideas stick.
- 📘 [The Matrix Calculus You Need For Deep Learning — Parr & Howard](https://arxiv.org/abs/1802.01528) — when you want to actually understand the chain rule for tensors.
- 📘 [Deep Learning book — Goodfellow, Bengio, Courville (free online)](https://www.deeplearningbook.org/) — chapters 2–4 cover the math; chapter 9 covers CNNs.

---

## Galaxies & Astronomy

### Big picture
- 📘 [Las Cumbres Observatory — Spacebook on Galaxies](https://lco.global/spacebook/galaxies/) — concise, accurate primer.
- 📘 [Wikipedia — Hubble sequence](https://en.wikipedia.org/wiki/Hubble_sequence) — surprisingly well-written; mine the references.
- 📘 [Wikipedia — Galaxy morphological classification](https://en.wikipedia.org/wiki/Galaxy_morphological_classification).
- 📘 [NASA — "What Is a Galaxy?"](https://spaceplace.nasa.gov/galaxy/en/).
- 📘 [NASA Universe of Learning — Galaxies](https://universe-of-learning.org/contents/topics/galaxies).
- 📘 [Caltech Cosmos — Galaxies](https://www.astro.caltech.edu/~george/ay127/) lecture notes (graduate but very clear).

### Citizen science & data
- 🌌 [Galaxy Zoo — project home](https://www.zooniverse.org/projects/zookeeper/galaxy-zoo).
- 🌌 [Galaxy Zoo 2 results paper — Willett et al. 2013](https://academic.oup.com/mnras/article/435/4/2835/1023755).
- 🌌 [SDSS — Sloan Digital Sky Survey](https://www.sdss.org/).
- 🌌 [SDSS SkyServer Explore Tool](https://skyserver.sdss.org/) — look at the exact images Galaxy Zoo labelled.
- 🌌 [Galaxy Zoo 2 Kaggle dataset (our dataset)](https://www.kaggle.com/datasets/jaimetrickz/galaxy-zoo-2-images).

### Channels worth following
- 📺 [Dr. Becky (Dr. Becky Smethurst, Oxford astrophysicist)](https://www.youtube.com/@DrBecky) — galaxies, black holes, with rigour and humour.
- 📺 [Crash Course Astronomy — Phil Plait](https://www.youtube.com/playlist?list=PL8dPuuaLjXtPAJr1ysd5yGIyiSFuh0mIL) — 46 short episodes covering the whole field.
- 📺 [PBS Space Time](https://www.youtube.com/@pbsspacetime) — denser, but excellent on density waves, mergers, dark matter.
- 📺 [Sixty Symbols — galaxies playlist](https://www.youtube.com/@sixtysymbols) — short, fun, faculty-led.

### Textbooks (deep dives)
- 📘 *Galaxies in the Universe: An Introduction* — Sparke & Gallagher (undergraduate-level, very readable).
- 📘 *Extragalactic Astronomy and Cosmology* — Schneider (more advanced).
- 📘 *Galactic Dynamics* — Binney & Tremaine (the bible; graduate-level, mathematical).

### Image galleries (eye candy that builds intuition)
- 🖼️ [ESA/Hubble image archive — Galaxies](https://esahubble.org/images/archive/category/galaxies/).
- 🖼️ [NASA / James Webb Space Telescope — galaxy images](https://webbtelescope.org/contents/articles/galaxies).
- 🖼️ [NOIRLab image gallery](https://noirlab.edu/public/images/).
- 🖼️ [Astronomy Picture of the Day (APOD) archive](https://apod.nasa.gov/apod/archivepix.html).

---

## ML × Astronomy (Where We're Headed)

- 📄 [Dieleman, Willett, Dambre 2015 — Rotation-invariant CNNs for Galaxy Morphology (arXiv)](https://arxiv.org/abs/1503.07077) — the original *Kaggle Galaxy Zoo Challenge* winner. Highly readable.
- 📄 [Walmsley et al. — Galaxy Zoo DECaLS papers (arXiv search)](https://arxiv.org/a/walmsley_m_1) — modern deep learning at Galaxy Zoo scale.
- 📄 [Astronomy and Computing journal](https://www.sciencedirect.com/journal/astronomy-and-computing) — the field has its own dedicated journal.
- 📘 [`astroNN` — Python package for ML in astronomy](https://github.com/henrysky/astroNN).
- 📘 [HuggingFace — astronomy datasets](https://huggingface.co/datasets?search=galaxy).

---

## Communities

- 💬 [PyTorch discussion forums](https://discuss.pytorch.org/) — official, very active.
- 💬 [r/learnmachinelearning](https://www.reddit.com/r/learnmachinelearning/) and [r/MachineLearning](https://www.reddit.com/r/MachineLearning/).
- 💬 [r/AskAstronomy](https://www.reddit.com/r/AskAstronomy/) and [r/Astronomy](https://www.reddit.com/r/Astronomy/).
- 💬 [Astronomy Stack Exchange](https://astronomy.stackexchange.com/) — for proper "is this normal?" questions.
- 💬 The official **CAIC CSoT channels** — your first stop for track-specific questions and mentor help.

---

## How to Use This List

You will not read all of this. That's fine — most of it is reference, to be raided when a specific question comes up. Suggested workflow for week 1:

1. **Part 1:** do the [`Quick Self-Check`](02-pytorch-tensors.md#quick-self-check) in `02-pytorch-tensors.md` and the gallery quiz in [`05-galaxy-morphologies.md`](05-galaxy-morphologies.md).
2. **Watch** one episode of *Crash Course Astronomy* or *Dr. Becky* on galaxies.
3. **Skim** the official PyTorch [Tensors tutorial](https://docs.pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html) end-to-end.
4. **Part 2:** skim the PyTorch [Datasets & DataLoaders tutorial](https://docs.pytorch.org/tutorials/beginner/basics/data_tutorial.html) and the self-check in [`08-data-pipelines.md`](08-data-pipelines.md).
5. **Bookmark** this page; come back as questions arise.

⬅️ Back to [Week 1 README](README.md)
