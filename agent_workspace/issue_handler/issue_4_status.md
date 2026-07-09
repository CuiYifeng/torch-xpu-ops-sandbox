# Issue 4 Status

- Issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/4
- Branch: dev_issue_4
- Classification: stale upstream dynamo failure report on the current checkout

## Summary

Issue 4 reports `torch._dynamo.exc.Unsupported` from the XPU wrapper of
`test_zip_strict`, but that path is not reproducible on the current checkout.

## Current Findings

- Reproducer used:
  `python test/dynamo/test_functions.py DefaultsTests.test_zip_strict`
- The command passes locally on the current workspace.
- There is no current `third_party/torch-xpu-ops/test/xpu/dynamo/test_functions_xpu.py`
  wrapper in this checkout, which suggests the issue body points at an older
  layout or an older release branch.

## Handling Result

- No code fix was committed in this iteration.
- `pytorch_update.md` was updated to record the current `NOT_REPRODUCED`
  result and the verified command.
- This branch remains a status-only handoff for a later check against the
  original release/2.13 revision if needed.