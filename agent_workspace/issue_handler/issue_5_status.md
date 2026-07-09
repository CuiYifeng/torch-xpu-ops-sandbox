# Issue 5 Status

- Issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/5
- Branch: dev_issue_5
- Classification: stale upstream porting report on the current checkout

## Summary

Issue 5 reports hardcoded CUDA API usage in upstream tests, but the current
checkout does not reproduce the reported failures as written.

## Current Findings

- Reproducer used for the convolution slice:
  `python -m pytest -sxv nn/test_convolution_xpu.py -k 'test_slow_conv_dilated3d_unbatched'`
- That convolution test passes locally on the current workspace.
- The reported indexing case is no longer present under the named test path.
  Collecting the current XPU scatter/gather suite shows no
  `smem_stage_alignment_multi_iter` XPU test in this checkout.
- The current upstream CUDA-only code path lives in
  `pytorch/test/test_scatter_gather_ops.py`, but it is not surfaced by the
  current XPU wrapper as the reported failing test.

## Handling Result

- No code fix was committed in this iteration.
- `pytorch_update.md` was updated to record the current `NOT_REPRODUCED`
  result and the verified commands.
- This branch remains a status-only handoff for a later check against the
  original release/2.13 revision if the issue still reproduces there.