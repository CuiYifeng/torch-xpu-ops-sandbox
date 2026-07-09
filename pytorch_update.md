# PyTorch Update Notes

## Issue 5: hardcoded torch.cuda calls in upstream tests

- Source issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/5

### Current status

No pytorch source change was needed on this iteration.

- The reported convolution slice passes locally:

```bash
cd third_party/torch-xpu-ops/test/xpu
python -m pytest -sxv nn/test_convolution_xpu.py -k 'test_slow_conv_dilated3d_unbatched'
```

- The reported indexing slice is stale on the current checkout. Collecting the
  current XPU wrapper does not expose a `smem_stage_alignment_multi_iter` test.

### Remaining upstream touchpoint

The CUDA-only device property query currently lives in
`pytorch/test/test_scatter_gather_ops.py`, so any future real fix would likely
start there if the failure reappears on the relevant release branch.

### Suggested follow-up

If the issue still matters, re-run it against the original release/2.13 commit
or the original wrapper revision from the report, then decide between an
upstream device-agnostic test fix and a local XPU wrapper override.