# Issue 2 Status

- Issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/2
- Branch: dev_issue_2
- Classification: concrete bug report, not yet locally verified

## Summary

Issue 2 points to an upstream XPU failure in
`test/dynamo/test_repros.py::test_sdpa_dynamic_shapes`, with the symptom that
compiled and eager outputs are not close.

## Current Findings

- The upstream test anchor exists in `pytorch/test/dynamo/test_repros.py`.
- A likely XPU-side implementation touchpoint exists in
  `src/ATen/native/transformers/Attention.cpp`.
- The current workspace does not provide a usable verification environment:
  - importing `torch` from the pytorch source tree fails because the tree is
    not built;
  - the active Python environment outside the source tree does not have an
    installed `torch` package;
  - no local `.venv` was present for a fallback environment.

## Handling Result

- No code fix was committed in this iteration.
- A pytorch-side follow-up record was added to `pytorch_update.md`.
- A PR is opened to preserve the triage result and unblock later iteration once
  a runnable torch/XPU environment is available.