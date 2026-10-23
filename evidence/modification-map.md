# Modification Map: external/Microsoft-GSL

## Source: BlissOS android-x86 reference (external/Microsoft-GSL)
- BlissOS reference: android-generic/microsoft-GSL (simple cc_library_headers)
- UPSTREAM commits (port + evidence + post-audit fixes):
  - b4cc25f (initial KhillOS port - Android.bp + metadata)
  - db333c7 (AOSP 17 conventions - extended Android.bp + full metadata)
  - 8695410 (evidence files)
  - fb26ebb (fix fabricated METADATA identifier.version; correct apex_available provenance row)
  - 493899f (correct apex_available row to "(no apex_available)"; add reference HEAD to method section)
- Upstream base: microsoft/GSL v5.0.1 (tag fbd20b8)

## Modifications Applied to UPSTREAM/external_Microsoft-GSL (khillos-17 branch)

### 1. Android.bp Build System (EXTENDED from BlissOS)
**File:** `Android.bp` (extended from BlissOS version in commit db333c7)
- BlissOS: Basic `cc_library_headers` with `host_supported: true`, `vendor_available: true`, `cflags: ["-Wall", "-Werror"]`
- **UPSTREAM:** Extended with AOSP 17 conventions (reference: external/fmtlib/Android.bp):
  - Package-level license configuration with `default_applicable_licenses`
  - License module with `visibility: [":__subpackages__"]`, `license_text: ["LICENSE", "NOTICE"]`
  - Added `product_available`, `ramdisk_available`, `vendor_ramdisk_available`, `recovery_available`
  - Added `native_bridge_supported`
  - Added `target` config (linux_bionic + windows)
  - Added `min_sdk_version: "29"`, `sdk_version: "current"`
  - Added `apex_available` with `//apex_available:anyapex` + `//apex_available:platform`
  - Added `visibility: ["//system/libbase"]`
  - Added `cpp_std: "c++14"` (upstream requires C++14)
  - Kept `cflags: ["-Wall", "-Werror"]` (BlissOS Android.bp already set them)
  - Kept `host_supported: true`, `vendor_available: true`

### 2. AOSP 17 Compliance Metadata Files (NEW/EXTENDED)
**Files:** `METADATA` (extended), `NOTICE` (new - replaced symlink), `MODULE_LICENSE_MIT`, `OWNERS`
- METADATA: Updated to external_updater format with proper identifier
- NOTICE: Created as actual file (was symlink to LICENSE in BlissOS)
- MODULE_LICENSE_MIT: SPDX identifier for Soong license module
- OWNERS: Standard AOSP OWNERS file

### 3. SPDX / Licensing Approach (UPSTREAM BASIS: NO per-file SPDX headers)
The 11 headers under `include/gsl/` carry Microsoft copyright notices and contain **no SPDX-License-Identifier lines** (verified: `grep -rn "SPDX-License-Identifier" include/` in khillos-17 returns nothing; headers are byte-identical to microsoft/GSL v5.0.1). Licensing is expressed the AOSP 17 way: the `license` module in Android.bp references `LICENSE`/`NOTICE` with `SPDX-license-identifier-MIT`, plus MODULE_LICENSE_MIT. No per-file SPDX banners were added.

## Summary
- **Total files modified:** 5 (4 metadata files + 1 Android.bp extended)
- **Source files unchanged:** Yes (header-only library, no source changes)
- **Logic/behavior changes:** None
- **Build system changes:** Extended Android.bp with AOSP 17 conventions (functional equivalent + more)