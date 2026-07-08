# PyTorch Update Notes

## Issue 5: hardcoded torch.cuda calls in upstream tests

- Source issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/5

### Likely upstream touchpoints

- `pytorch/test/test_scatter_gather_ops.py`: CUDA-only device property queries
  are used in scatter-add override coverage.
- `pytorch/test/nn/test_convolution.py`: the reported slow convolution failure
  should be re-checked against the current upstream test body because the local
  file has already drifted from the issue description.

### Current status

This iteration did not make a pytorch source change. The local workspace does
not currently provide a runnable torch/XPU environment for direct reproduction
and validation.

### Suggested follow-up

When an environment is available, verify which failing tests are still current,
then either:

- make the upstream test logic device-agnostic, or
- override the affected test methods in the XPU wrapper layer with equivalent
  XPU-safe logic.