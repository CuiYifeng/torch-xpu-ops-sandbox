# Issue #24: FFT Half Dtype Workaround Status

## Status: NEEDS_HUMAN - Blocked on External Dependency

This issue tracks removal of the Half dtype upcasting workaround for FFT
operations once oneMKL introduces native Half support.

## Current Workaround Location

**File:** `src/ATen/native/xpu/mkl/SpectralOps.cpp`

```cpp
// TODO: Remove this work-around in future.
Tensor promote_fft_input(const Tensor& input) {
  if (input.scalar_type() == ScalarType::Half)
    return input.to(ScalarType::Float);
  if (input.scalar_type() == ScalarType::ComplexHalf)
    return input.to(ScalarType::ComplexFloat);
  return input;
}
```

This function upcasts Half/ComplexHalf inputs to Float/ComplexFloat before
performing FFT operations. Results are cast back to the original type after.

## What Needs to Be Done

1. Monitor oneMKL releases for native Half dtype support in FFT kernels.
2. Once available, remove `promote_fft_input()` calls and the function itself.
3. Remove the downcast operations at the end of `_fft_c2c_mkl`, `_fft_c2r_mkl`,
   and `_fft_r2c_mkl` that convert results back to Half.
4. Verify correctness and performance with the native Half path.

## References

- Original issue: intel/torch-xpu-ops#2617
- Workaround PR: intel/torch-xpu-ops#2637
- Tracking: CuiYifeng/torch-xpu-ops-sandbox#24
