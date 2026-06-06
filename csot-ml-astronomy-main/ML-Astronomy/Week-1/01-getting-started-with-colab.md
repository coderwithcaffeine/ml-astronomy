# 01 — Getting Started with Google Colab

> Why we use Colab, how to enable a GPU, and the small handful of tricks that will save you hours later.

---

## What is Google Colab?

**Google Colaboratory** ("Colab") is a free, browser-based Jupyter notebook environment hosted on Google's infrastructure. You write Python in cells, hit Shift + Enter, and the code runs on a remote virtual machine that already has the entire data-science stack pre-installed.

Why we use it for CSoT:

- **Zero setup.** No Anaconda, no `pip install torch` battles, no CUDA driver mismatches.
- **Free GPUs.** You get access to an NVIDIA T4 (or sometimes better) for several hours at a stretch.
- **Shareable.** A Colab notebook is a Google Doc you can share with a mentor in one click.
- **Reproducible-ish.** The same notebook runs the same way for every participant.

Colab is built on top of **Jupyter notebooks**, so everything you learn here transfers to JupyterLab, Kaggle Kernels, VS Code's notebook UI, and so on.

---

## Step-by-Step: Your First Colab Notebook

### 1. Create the notebook

1. Go to [colab.research.google.com](https://colab.research.google.com).
2. Sign in with your Google account.
3. Click **File → New notebook**.

You'll see a single empty cell. The default name is `Untitled0.ipynb` — rename it (top-left) to something like `week1_tensors.ipynb`.

### 2. Switch to the GPU runtime

This is **the most important setup step of the entire summer**. Colab gives you a CPU by default, which is far too slow for deep learning.

1. Open the menu: **Runtime → Change runtime type**.
2. Under **Hardware accelerator**, choose **GPU**.
3. Under **GPU type**, leave it on the default (usually **T4**).
4. Click **Save**.

Colab will restart the runtime. Confirm the GPU is alive by running this in a cell:

```python
!nvidia-smi
```

You should see a table listing an NVIDIA Tesla T4 (or similar) with its memory usage. If you see `command not found`, your runtime is not on GPU — repeat the steps above.

### 3. Run a cell

Click into the first cell, type:

```python
print("Hello, cosmos!")
```

…and press **Shift + Enter**. The cell executes, prints the output below itself, and creates a new cell.

### 4. Add new cells

- **+ Code** (toolbar or `Ctrl/Cmd + M B`) — adds a code cell below.
- **+ Text** — adds a Markdown cell for notes / headings.

Markdown cells in Colab support standard Markdown syntax, LaTeX inside `$…$`, and embedded images — useful for narrating your project task.

### 5. (Optional) Mount Google Drive

When we start working with the Galaxy Zoo dataset (Week 1, Part 2), it's convenient to store data in your Drive so it persists across sessions:

```python
from google.colab import drive
drive.mount('/content/drive')
```

You will be prompted to authorise access. After mounting, your Drive is available under `/content/drive/MyDrive/`.

---

## Mental Model: Cells, Kernels, and State

A Colab notebook is a sequence of **cells** that share one underlying Python process called the **kernel** (technically an IPython kernel). Important consequences:

- **Order matters.** A variable defined in cell 5 is *not* available in cell 3 until you run cell 5 first.
- **Re-running cells is normal.** You're free to edit and re-run cells; the kernel keeps state across runs.
- **Restarting wipes state.** **Runtime → Restart runtime** clears every variable and reloads every module. Use it whenever things get weird.
- **Idle disconnects.** Colab kicks idle sessions after ~90 minutes and hard-disconnects after ~12 hours. Save your work to Drive or GitHub frequently.

A solid habit: at the end of every session, run **Runtime → Restart and run all** to confirm your notebook is reproducible from a cold start.

---

## Useful Keyboard Shortcuts

| Action | Shortcut |
|---|---|
| Run cell | `Shift + Enter` |
| Run cell and stay | `Ctrl/Cmd + Enter` |
| Insert code cell below | `Ctrl/Cmd + M B` |
| Insert code cell above | `Ctrl/Cmd + M A` |
| Convert to Markdown | `Ctrl/Cmd + M M` |
| Convert to code | `Ctrl/Cmd + M Y` |
| Delete cell | `Ctrl/Cmd + M D` |
| Show all shortcuts | `Ctrl/Cmd + M H` |

The full shortcut list is under **Tools → Keyboard shortcuts**.

---

## Shell Commands in Cells

Any line that starts with `!` is a **shell command** that runs on the underlying Linux VM:

```python
!pip install some-package
!ls /content
!nvidia-smi
!cat /etc/os-release
```

You'll mostly use `!pip install ...` when you need a package that's not pre-installed, and `!nvidia-smi` whenever you want to confirm your GPU is alive.

Note: the `!` runs in a fresh subshell, so things like `!cd somewhere` don't persist. For directory changes use the magic `%cd somewhere` instead.

---

## Saving Your Work

Colab autosaves to your Google Drive every few seconds (look for "All changes saved" near the title). You have a few additional options:

- **File → Save a copy in GitHub** — pushes the notebook to a repo (great for CSoT submissions).
- **File → Download → .ipynb** — get a local copy.
- **File → Save a copy in Drive** — duplicate for safety.

For this track, the recommended flow is: fork [the CSoT repo](../../README.md), keep your weekly notebooks under your fork, and push regularly from Colab.

---

## Common Pitfalls

| Symptom | Most likely cause | Fix |
|---|---|---|
| `torch.cuda.is_available()` returns `False` | Runtime is CPU, not GPU. | Runtime → Change runtime type → GPU. |
| Suddenly missing variables / weird errors | Cells were run out of order, or the runtime restarted. | Runtime → Restart and run all. |
| "You are not connected to a runtime" | Idle disconnect. | Click **Connect** in the top-right. |
| Out-of-memory (`CUDA out of memory`) | Tensor too big, or previous run still holding memory. | Restart runtime, or `del` large tensors and `torch.cuda.empty_cache()`. |
| Cannot find Drive files | Forgot to mount Drive. | Re-run the `drive.mount(...)` cell. |
| Slow cell despite GPU | The code is still running on CPU. | Ensure tensors and the model are `.to(device)`. |

---

## External Resources

- 📘 [Welcome to Colab](https://colab.research.google.com/notebooks/welcome.ipynb) — Google's official intro notebook.
- 📘 [Overview of Colab features](https://colab.research.google.com/notebooks/basic_features_overview.ipynb).
- 📘 [Markdown guide for Colab](https://colab.research.google.com/notebooks/markdown_guide.ipynb).
- 📺 [Getting Started with Google Colab — by Jeff Heaton](https://www.youtube.com/watch?v=inN8seMm7UI) (~10 min).
- 📺 [Google Colab Tutorial for Beginners — by Tech With Tim](https://www.youtube.com/watch?v=oCngVVBSsmA) (~15 min).
- 📘 [Jupyter Notebook documentation](https://jupyter-notebook.readthedocs.io/en/stable/) — Colab is a flavour of Jupyter.

---

➡️ Next: [`02-pytorch-tensors.md`](02-pytorch-tensors.md)
