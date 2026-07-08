# Issue 5 Status

- Issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/5
- Branch: dev_issue_5
- Classification: concrete porting bug with likely upstream-test fixes

## Summary

Issue 5 describes hardcoded CUDA-specific API usage in upstream tests that are
being exercised through XPU wrappers.

## Current Findings

- The convolution-related failure points at the upstream test path in
  `pytorch/test/nn/test_convolution.py`.
- The indexing-related failure points at upstream scatter/gather tests using
  `torch.cuda.get_device_properties(...).multi_processor_count`.
- The local XPU wrapper files are likely touchpoints for any targeted override,
  but the current workspace still lacks a runnable torch/XPU environment for
  validating a behavior change.

## Handling Result

- No code change was committed in this iteration.
- A pytorch-side follow-up note was added to `pytorch_update.md`.
- A status PR is opened so the porting bug remains tracked for a later fix.