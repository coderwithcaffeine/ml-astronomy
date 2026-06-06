# 03 — GPU Acceleration in PyTorch

> **A GPU is the single most important reason you can train a deep learning model in a coffee break instead of a coffee plantation's harvest season.** This page covers how PyTorch finds your GPU, how you put tensors on it, and how to measure the speedup yourself.

---

## CPU vs GPU: A Quick Mental Model

| | CPU | GPU |
|---|---|---|
| Cores | Few (4–16), very fast, very flexible | Thousands of small, simpler cores |
| Best at | Sequential logic, branching, I/O | The same operation applied to *many* numbers at once |
| Analogy | A handful of brilliant chefs | A small army of line cooks chopping vegetables in parallel |

Deep learning is essentially a sequence of huge matrix multiplications. That's *exactly* the workload GPUs were built for. A modest GPU can outpace a top-end CPU by **10×–100×** on these workloads. Big networks are *not feasible* to train on CPU at all.

You don't need to know any CUDA programming to benefit from this. PyTorch handles the low-level details; you just have to put your tensors in the right place.

---

## Is the GPU Available?

After enabling the GPU runtime in Colab (see [`01-getting-started-with-colab.md`](01-getting-started-with-colab.md)), confirm from Python:

```python
import torch

print("CUDA available:", torch.cuda.is_available())
print("Device count :", torch.cuda.device_count())
print("Device name  :", torch.cuda.get_device_name(0) if torch.cuda.is_available() else "n/a")
```

Expected output on a healthy Colab GPU runtime:

```
CUDA available: True
Device count : 1
Device name  : Tesla T4
```

If `is_available()` returns `False`, your runtime is on CPU. Fix it via **Runtime → Change runtime type → GPU**.

> "CUDA" is NVIDIA's parallel computing platform. PyTorch's GPU backend is built on it. You'll see `cuda:0` everywhere — that's just "GPU number 0".

---

## The `device` Pattern

A common idiom you should adopt for every project:

```python
device = "cuda" if torch.cuda.is_available() else "cpu"
print("Using:", device)
```

Now anything you want on the GPU gets `.to(device)` tacked on:

```python
x = torch.randn(3, 64, 64).to(device)
```

This pattern is portable: the same code will silently fall back to CPU on a machine without a GPU. Use it religiously.

---

## Moving Tensors Around

```python
cpu_tensor = torch.randn(1000, 1000)        # default: on CPU
gpu_tensor = cpu_tensor.to("cuda")          # copy to GPU
back_to_cpu = gpu_tensor.to("cpu")          # copy back
back_to_cpu = gpu_tensor.cpu()              # shorthand
```

Three crucial rules:

1. **All operands of an op must share a device.** `cpu_tensor + gpu_tensor` throws. PyTorch never silently moves data for you.
2. **`.to(device)` returns a *new* tensor for non-CPU moves.** It does not modify the original in-place.
3. **NumPy lives on the CPU.** You must `.cpu()` before `.numpy()`.

```python
# wrong — will raise an error
a = torch.randn(3, 3)               # cpu
b = torch.randn(3, 3).cuda()        # gpu
c = a + b   # RuntimeError: Expected all tensors to be on the same device

# right
a = torch.randn(3, 3, device=device)
b = torch.randn(3, 3, device=device)
c = a + b
```

> **Pro tip:** create tensors directly on the right device with `device=device` instead of creating them on CPU and then moving. This is faster and uses less memory.

---

## Move Whole Models, Not Just Tensors

When we start defining models in Week 2, you'll do the equivalent thing for the model:

```python
model = MyModel().to(device)
```

This moves all the model's parameters (weights and biases) to the GPU. You'll then have to move every batch of input data to the same device before each forward pass:

```python
for inputs, labels in loader:
    inputs, labels = inputs.to(device), labels.to(device)
    outputs = model(inputs)
    # ...
```

---

## Benchmarking: Feel the Difference

Try this in a Colab cell to see the speedup yourself. Pay attention to the **second** GPU run — the first run includes one-time GPU initialisation overhead, which is misleading.

```python
import time
import torch

size = 4096
n_runs = 5

def bench(device):
    a = torch.randn(size, size, device=device)
    b = torch.randn(size, size, device=device)
    # warm-up (especially important for GPU)
    for _ in range(2):
        (a @ b).sum().item()
    if device == "cuda":
        torch.cuda.synchronize()

    t0 = time.perf_counter()
    for _ in range(n_runs):
        c = a @ b
    if device == "cuda":
        torch.cuda.synchronize()
    t1 = time.perf_counter()
    return (t1 - t0) / n_runs

print(f"CPU avg : {bench('cpu')*1000:.1f} ms")
if torch.cuda.is_available():
    print(f"GPU avg : {bench('cuda')*1000:.1f} ms")
```

On a Colab T4 you'll typically see something like:

```
CPU avg : ~3500 ms
GPU avg : ~30   ms
```

That's roughly a **100× speedup** for a single matrix multiply. Models do many of these per batch and hundreds of batches per epoch — which is why running on GPU is non-negotiable.

> **Why `torch.cuda.synchronize()`?** GPU calls are *asynchronous* — they queue work and return immediately. To time them honestly, you have to wait for the GPU to finish.

---

## GPU Memory Management

The Colab T4 has roughly **15 GB** of GPU memory. That's a lot, but it's easy to exhaust if you're not careful. Useful tools:

```python
torch.cuda.memory_allocated() / 1e9   # currently allocated, in GB
torch.cuda.memory_reserved()  / 1e9   # reserved by PyTorch's allocator, in GB
torch.cuda.empty_cache()              # free unused cached memory
```

If you hit `CUDA out of memory`:

1. **`del` the big tensors** you no longer need, then call `torch.cuda.empty_cache()`.
2. **Reduce the batch size** (we'll see this in Week 3).
3. **Restart the runtime** as a last resort — it always works.
4. **Use smaller image sizes** during early experimentation (e.g., 32×32 instead of 224×224).

You can also peek at the GPU's own view from a shell cell:

```python
!nvidia-smi
```

---

## Common Mistakes (You Will Make All of Them)

| Symptom | Cause | Fix |
|---|---|---|
| `RuntimeError: Expected all tensors to be on the same device` | Mixing CPU and GPU tensors. | `.to(device)` the offender. |
| `TypeError: can't convert cuda:0 device type tensor to numpy` | Calling `.numpy()` on a GPU tensor. | `.cpu().numpy()`. |
| Model runs but is just as slow as CPU | Model is on GPU but data isn't (or vice versa). | Move both. |
| `CUDA out of memory` | Batch / model too big, leftover tensors. | Shrink batch, `del` + `empty_cache()`, restart runtime. |
| `is_available()` returns `False` mysteriously mid-session | Colab swapped you to a CPU-only host. | Reconnect to runtime, or pick a new one. |

---

## External Resources

- 📘 [PyTorch — CUDA semantics](https://docs.pytorch.org/docs/stable/notes/cuda.html) — the canonical reference.
- 📘 [PyTorch — `torch.cuda` reference](https://docs.pytorch.org/docs/stable/cuda.html).
- 📘 [Colab — Using accelerated hardware](https://research.google.com/colaboratory/faq.html#gpu-availability) (Colab FAQ).
- 📘 [NVIDIA — CUDA in 60 seconds](https://developer.nvidia.com/blog/even-easier-introduction-cuda/) for if you ever get curious about how the GPU is *actually* programmed.
- 📺 [How GPUs work — Sebastian Lague (~15 min)](https://www.youtube.com/watch?v=h9Z4oGN89MU) — beautiful animated intuition.
- 📘 [PyTorch performance tuning guide](https://docs.pytorch.org/docs/stable/notes/cuda.html#cuda-performance-considerations).

---

⬅️ Previous: [`02-pytorch-tensors.md`](02-pytorch-tensors.md) | ➡️ Next: [`04-hubble-tuning-fork.md`](04-hubble-tuning-fork.md)
