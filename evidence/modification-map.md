# Modification Map: external/Microsoft-GSL

## Source: BlissOS android-x86 reference (external/Microsoft-GSL)
- BlissOS reference: android-generic/microsoft-GSL (simple cc_library_headers)
- UPSTREAM commits:
  - b4cc25f (initial KhillOS port - Android.bp + metadata)
  - db333c7 (AOSP 17 conventions - extended Android.bp + full metadata)
- Upstream base: microsoft/GSL v5.0.1 (tag fbd20b8)

## Modifications Applied to UPSTREAM/external_Microsoft-GSL (khillos-17 branch)

### 1. Android.bp Build System (EXTENDED from BlissOS)
**File:** `Android.bp` (extended from BlissOS version in commit db333c7)
- BlissOS: Basic `cc_library_headers` with `vendor_available: true`
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
  - Added `cflags: ["-Wall", "-Werror"]`
  - Kept `host_supported: true`, `vendor_available: true`

### 2. AOSP 17 Compliance Metadata Files (NEW/EXTENDED)
**Files:** `METADATA` (extended), `NOTICE` (new - replaced symlink), `MODULE_LICENSE_MIT`, `OWNERS`
- METADATA: Updated to external_updater format with proper identifier
- NOTICE: Created as actual file (was symlink to LICENSE in BlissOS)
- MODULE_LICENSE_MIT: SPDX identifier for Soong license module
- OWNERS: Standard AOSP OWNERS file

### 3. SPDX Headers - ALREADY PRESENT
Upstream Microsoft-GSL uses MIT license. Source files may have license headers but SPDX identifiers are typically in license module only for header-only libraries.

## Summary
- **Total files modified:** 5 (4 metadata files + 1 Android.bp extended)
- **Source files unchanged:** Yes (header-only library, no source changes)
- **Logic/behavior changes:** None
- **Build system changes:** Extended Android.bp with AOSP 17 conventions (functional equivalent + more)