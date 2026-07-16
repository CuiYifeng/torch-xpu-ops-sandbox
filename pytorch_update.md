# Upstream PyTorch Changes

## Issue #21: Add expectedFailure decorator for native_group_norm on XPU

**File:** `torch/testing/_internal/common_methods_invocations.py`

**Change:** Add `DecorateInfo(unittest.expectedFailure, "TestMeta", "test_dispatch_symbolic_meta_outplace_all_strides", device_type="xpu")` to the `native_group_norm` OpInfo `skips` tuple, mirroring the existing CUDA entry.

**Diff:**
```diff
--- a/torch/testing/_internal/common_methods_invocations.py
+++ b/torch/testing/_internal/common_methods_invocations.py
@@ -16336,6 +16336,7 @@
             # native_group_norm expects contiguous inputs on CUDA
             DecorateInfo(unittest.expectedFailure, "TestMeta", "test_dispatch_symbolic_meta_outplace_all_strides", device_type="cuda"),
+            DecorateInfo(unittest.expectedFailure, "TestMeta", "test_dispatch_symbolic_meta_outplace_all_strides", device_type="xpu"),
         ),
```

**Reason:** `native_group_norm` expects contiguous inputs. The same `expectedFailure` decorator already exists for CUDA; XPU has the same constraint.
