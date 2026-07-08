# PyTorch Update Notes

## Issue 2: sdpa dynamic shapes mismatch on XPU

- Source issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/2
- Upstream test anchor: `pytorch/test/dynamo/test_repros.py::test_sdpa_dynamic_shapes`
- Candidate XPU implementation touchpoint: `src/ATen/native/transformers/Attention.cpp`

### Current status

This iteration did not make a pytorch source change. The immediate blocker is
environmental: the local pytorch source tree is not built, importing `torch`
from the source tree fails, and the active Python environment does not provide
an installed torch package with XPU support for direct reproduction.

### Next verification step

When a runnable torch/XPU environment is available, rerun the minimal repro
derived from `test_sdpa_dynamic_shapes` and compare eager vs `torch.compile(...,
backend="eager", dynamic=True)` output on XPU.

### Expected follow-up area

If the mismatch reproduces, start by checking SDPA backend selection and math
fallback behavior in `src/ATen/native/transformers/Attention.cpp`.