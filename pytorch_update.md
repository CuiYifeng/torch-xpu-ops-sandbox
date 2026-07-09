# PyTorch Update Notes

## Issue 4: dynamo zip strict unsupported on XPU

- Source issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/4
- Reported test case:
  `third_party.torch-xpu-ops.test.xpu.dynamo.test_functions_xpu.DefaultsTests.test_zip_strict`

### Current status

No pytorch source change was needed on this iteration. The current checkout does
not reproduce the report:

```bash
python test/dynamo/test_functions.py DefaultsTests.test_zip_strict
```

That command passes locally.

### Suggested follow-up

If the issue still matters, re-run it against the original release/2.13 commit
from the issue body or the original XPU wrapper revision, because the current
workspace layout no longer contains the reported wrapper path.