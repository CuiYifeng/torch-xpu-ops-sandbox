# PyTorch Update Notes

## Issue 4: dynamo zip strict unsupported on XPU

- Source issue: https://github.com/CuiYifeng/torch-xpu-ops-sandbox/issues/4
- Reported test case:
  `third_party.torch-xpu-ops.test.xpu.dynamo.test_functions_xpu.DefaultsTests.test_zip_strict`

### Current status

This iteration did not make a pytorch source change. The local workspace does
not currently provide a runnable torch/XPU environment for direct reproduction.

### Suggested follow-up

Reproduce the failure in the upstream dynamo test path and inspect where the
`ValueError` from `zip(strict=True)` is wrapped into
`torch._dynamo.exc.Unsupported` on XPU.