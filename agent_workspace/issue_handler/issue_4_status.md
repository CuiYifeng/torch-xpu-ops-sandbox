# Issue 4 Status

- Issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/4
- Branch: dev_issue_4
- Classification: concrete upstream test failure, not locally verified

## Summary

Issue 4 reports `torch._dynamo.exc.Unsupported` from the XPU wrapper of
`test_zip_strict` in the upstream dynamo test suite.

## Current Findings

- The issue is a single concrete failing case rather than a broad tracker.
- The failure likely needs investigation in the upstream PyTorch dynamo test or
  the XPU-specific wrapper path that exercises it.
- The current workspace still does not provide a runnable torch/XPU environment
  for local reproduction.

## Handling Result

- No code fix was committed in this iteration.
- A pytorch-side follow-up note was added to `pytorch_update.md`.
- A status PR is opened so the issue remains tracked for the next iteration.