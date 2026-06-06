# 02 — PyTorch Tensors

> A **tensor** is the fundamental data structure of PyTorch. If NumPy arrays are matrices on steroids, PyTorch tensors are matrices on steroids that can also live on a GPU and remember how they were calculated. That last bit is what makes deep learning possible.

---

## What is a Tensor?

In physics and math, "tensor" has a fancy meaning. In ML libraries like PyTorch and TensorFlow, the definition is mercifully simpler:

> **A tensor is a multi-dimensional array of numbers, of any dimension you like.**

You already know the lower-dimensional cases:

| Name      | Math notation | Shape (PyTorch) | Example                              |
|-----------|---------------|-----------------|--------------------------------------|
| Scalar    | a number      | `()`            | `3.14`                                |
| Vector    | 1D array      | `(n,)`          | `[1.0, 2.0, 3.0]`                     |
| Matrix    | 2D array      | `(m, n)`        | grayscale image                       |
| 3-Tensor  | 3D array      | `(c, h, w)`     | RGB image (channels × height × width) |
| 4-Tensor  | 4D array      | `(b, c, h, w)`  | **batch** of RGB images               |

Every tensor we touch this summer will be one of these shapes. A galaxy image is a 3-tensor; a batch of galaxy images going into a CNN is a 4-tensor.

---

## Creating Tensors

```python
import torch

# from a Python list
t1 = torch.tensor([[1, 2, 3], [4, 5, 6]])

# common factory functions
zeros = torch.zeros(3, 4)          # 3x4 of 0.0
ones  = torch.ones(2, 2)           # 2x2 of 1.0
rand  = torch.rand(3, 64, 64)      # uniform in [0, 1)
randn = torch.randn(3, 64, 64)     # standard normal (mean=0, std=1)
ar    = torch.arange(0, 10, 2)     # [0, 2, 4, 6, 8]
eye   = torch.eye(4)               # identity matrix
```

> **Why `randn` and not `rand`?** Most weight initialisation in deep learning uses samples from a Gaussian. `randn` is the workhorse you'll see most often.

You can also convert from NumPy:

```python
import numpy as np
arr = np.array([1.0, 2.0, 3.0])
t   = torch.from_numpy(arr)   # shares memory with the NumPy array!
```

---

## The Three Attributes You'll Check Every Day

Every tensor has three attributes you'll inspect constantly:

```python
x = torch.randn(3, 64, 64)
print(x.shape)   # torch.Size([3, 64, 64])
print(x.dtype)   # torch.float32
print(x.device)  # cpu
```

| Attribute | What it tells you | Why it matters |
|---|---|---|
| `.shape` | Sizes along each dimension. | A shape mismatch is the most common source of bugs in deep learning. |
| `.dtype` | Element type (e.g. `float32`, `int64`, `bool`). | Models expect specific dtypes; mixing them throws errors. |
| `.device` | Where the tensor lives (`cpu` or `cuda:0`). | All operands of an op must share a device. |

Get used to printing all three at any sign of trouble. It's the deep-learning equivalent of `console.log`.

---

## Indexing, Slicing, and Reshaping

PyTorch borrows NumPy's indexing syntax almost wholesale:

```python
x = torch.randn(3, 64, 64)

x[0]            # first channel (shape: 64x64)
x[:, 0, :]      # first row of every channel (shape: 3x64)
x[..., -1]      # last column of every channel (shape: 3x64)
x[0, 10:20, 5]  # a sub-slice
```

**Reshaping** without changing data:

```python
flat = x.view(-1)         # 1D, shape: (12288,) — uses 3*64*64
flat2 = x.reshape(3, -1)  # 2D, shape: (3, 4096)
```

> `view` requires contiguous memory; `reshape` figures it out for you. When in doubt, use `reshape`.

**Adding / removing dimensions:**

```python
batch = x.unsqueeze(0)    # add batch dim: (1, 3, 64, 64)
back  = batch.squeeze(0)  # remove a length-1 dim
```

The `unsqueeze(0)` pattern is something you'll do *a lot*, because models almost always expect a batch dimension.

---

## Element-wise Operations and Broadcasting

```python
a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([10.0, 20.0, 30.0])

a + b      # tensor([11., 22., 33.])
a * b      # element-wise
a ** 2     # element-wise power
torch.exp(a)
```

**Broadcasting** lets you combine tensors of different (but compatible) shapes:

```python
m = torch.randn(3, 4)
v = torch.randn(4)
m + v   # v is broadcast across the rows of m
```

Broadcasting rules (read right-to-left): dimensions are compatible if they are equal *or* one of them is 1. This is identical to NumPy.

---

## Matrix Multiplication

This is the workhorse of every neural network:

```python
A = torch.randn(3, 4)
B = torch.randn(4, 5)

C = A @ B            # the @ operator — preferred
C = torch.matmul(A, B)  # equivalent
```

For batched matmul (`(b, m, k) @ (b, k, n) -> (b, m, n)`), `@` and `matmul` handle it automatically.

---

## Reductions

Operations that "collapse" a dimension:

```python
x = torch.randn(3, 64, 64)
x.sum()          # scalar — sum of everything
x.mean()         # scalar — mean of everything
x.sum(dim=0)     # shape (64, 64) — sum across the channel dim
x.max(dim=-1)    # returns (values, indices)
```

The `dim` argument is the dimension you're **collapsing away**. A common stumbling block.

---

## In-place vs Out-of-place

PyTorch has two flavours of many operations:

```python
y = x.add(1)   # out-of-place — returns a new tensor
x.add_(1)      # in-place — modifies x, indicated by trailing _
```

In-place is faster and uses less memory, but breaks autograd in some situations. Prefer out-of-place until you have a reason not to.

---

## NumPy Interop

```python
# tensor -> numpy
np_arr = x.cpu().numpy()   # must be on CPU first!

# numpy -> tensor
t = torch.from_numpy(np_arr)
```

A common mistake is forgetting `.cpu()` when your tensor is on GPU — you'll get a friendly error reminding you.

---

## Why This Matters for Galaxy Images

A single galaxy image from the dataset is a tensor of shape `(3, 64, 64)`:

- `3` — RGB channels
- `64, 64` — height × width in pixels (after our resize transform in Week 1, Part 2)

A **batch** of 32 such images is `(32, 3, 64, 64)`. Every layer of every model we build will be expressed as tensor operations on shapes like these. The "training" of the network is, at its core, a sequence of matrix multiplications and element-wise operations on these tensors — efficient because they all run on the GPU.

---

## Quick Self-Check

Try these mentally (or in a Colab cell) before moving on:

1. What's the shape of `torch.randn(5, 3, 32, 32).sum(dim=1)`?
2. What's the difference between `torch.zeros(3, 4)` and `torch.zeros((3, 4))`?
3. If `x.shape == (3, 64, 64)`, what's the shape of `x[None]`? (Hint: `None` is shorthand for `unsqueeze`.)
4. Why does `t.numpy()` fail if `t` lives on the GPU?

<details>
<summary>Answers</summary>

1. `(5, 32, 32)` — dimension 1 is removed.
2. None — they're equivalent.
3. `(1, 3, 64, 64)`.
4. NumPy doesn't know about GPU memory; you have to `.cpu()` first.

</details>

---

## External Resources

- 📘 [PyTorch — Tensors tutorial](https://docs.pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html) — the official one-page intro.
- 📘 [PyTorch — Tensor API reference](https://docs.pytorch.org/docs/stable/tensors.html) — when you need every method.
- 📘 [Deep Learning with PyTorch — 60-Minute Blitz](https://docs.pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html) — covers tensors, autograd, NN basics.
- 📺 [3Blue1Brown — Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) — visual intuition for matrices and transformations.
- 📺 [PyTorch Tutorial — by Patrick Loeber (~30 min)](https://www.youtube.com/watch?v=exaWOE8jvy8).
- 📘 [NumPy ↔ PyTorch cheat sheet](https://github.com/wkentaro/pytorch-for-numpy-users) — invaluable if you already know NumPy.

---

⬅️ Previous: [`01-getting-started-with-colab.md`](01-getting-started-with-colab.md) | ➡️ Next: [`03-gpu-acceleration.md`](03-gpu-acceleration.md)
