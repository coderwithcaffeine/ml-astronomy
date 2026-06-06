# Week 3 — CNNs, the Training Loop & Evaluation

> 🚧 **Content coming soon.** This week's concept markdowns and notebooks are being written. The outline below is final and shows exactly what you'll learn.

The headline week. We build a **Convolutional Neural Network (CNN)**, write the **training loop** that actually teaches it, then learn to **evaluate and interpret** the result — including a confusion matrix that tells us, astrophysically, where the model gets confused.

---

## Planned Scope

### Part 1 — The Training Loop & CNNs

**Machine learning**
- `nn.Conv2d` and `nn.MaxPool2d`: extracting spatial features (spiral arms, edges) *without* flattening the image first.
- The PyTorch training loop, its five core steps every iteration:
  1. `optimizer.zero_grad()` — clear past gradients
  2. `outputs = model(inputs)` — forward pass
  3. `loss = criterion(outputs, labels)` — calculate error
  4. `loss.backward()` — backpropagation
  5. `optimizer.step()` — update weights
- Running for several epochs and watching the training loss fall.

**Astronomy**
- **Localized astrodynamics:** spiral arms are not rigid structures turning like fan blades — they're **density waves**, like moving traffic jams of gas and dust that trigger star formation as material passes through.
- **Dust lanes & H II regions:** dust lanes absorb light; H II regions are bright patches where new stars are forming.

### Part 2 — Validation & Interpretation

**Machine learning**
- `with torch.no_grad()`: turning off gradient tracking to evaluate quickly.
- Tracking and plotting **training vs. validation loss** over time (spotting overfitting).
- Generating a **confusion matrix** to see which galaxy types are hardest to distinguish.

**Astronomy**
- **Lenticular galaxies (S0):** the bridge between ellipticals and spirals — a disk but no arms — and a major source of classification ambiguity.
- **Galaxy evolution & mergers:** galaxies interact; irregular shapes often signal active galaxy-galaxy collisions, meaning morphology changes over billions of years.

---

## Planned Project Task

1. Replace the fully-connected model from Week 2 with a **CNN**, write the **training loop**, and run it for 5–10 epochs while watching the loss decrease.
2. Write the **evaluation loop**, plot training vs. validation curves, display a **confusion matrix**, and save the trained weights with `torch.save(model.state_dict(), 'galaxy_model.pth')`.

---

## Prerequisites

Finish [Week 1](../Week-1/) and [Week 2](../Week-2/) first. This week assumes you can load batched galaxy data, define an `nn.Module`, and understand losses and optimisers.

---

⬅️ Back to [track overview](../README.md)
