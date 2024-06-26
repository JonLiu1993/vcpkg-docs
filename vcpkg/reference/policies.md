---
title: Port Policies
description: Reference documentation of all policies that can be set in a port.
ms.date: 5/10/2024
ms.topic: reference
---
# Port Policies Reference

Port policies can be set to 'disabled' (the default) or 'enabled' in a `portfile.cmake`. For example:

```cmake
set(VCPKG_POLICY_EMPTY_INCLUDE_FOLDER enabled)
```

## VCPKG_POLICY_ALLOW_DEBUG_INCLUDE

Disables vcpkg's post-build check for the debug/include directory, which ports should not create.

## VCPKG_POLICY_ALLOW_DEBUG_SHARE

Disables vcpkg's post-build check for the debug/share directory, which ports should not create.

## VCPKG_POLICY_ALLOW_DLLS_IN_LIB

Disables vcpkg's post-build check for DLLs installed to the 'lib' directory rather than the 'bin' directory.

## VCPKG_POLICY_ALLOW_EMPTY_FOLDERS

Disables vcpkg's post-build check for empty directories created by a port. Empty directories are not considered semantically part of what a port installs, and aren't representable to several binary caching backends.

## VCPKG_POLICY_ALLOW_EXES_IN_BIN

Disables vcpkg's post-build check for exe files in the 'bin' directory, which should not exist. Build tools should be moved to the tools directory, possibly using [`vcpkg_copy_tools`](../maintainers/functions/vcpkg_copy_tools.md).

## VCPKG_POLICY_ALLOW_KERNEL32_FROM_XBOX

Disables vcpkg's post-build check for linking with kernel32 when a port requests targeting XBox. Binaries linked with kernel32 can't run on the XBox, which does not have kernel32.dll.

## VCPKG_POLICY_ALLOW_OBSOLETE_MSVCRT

Disables vcpkg's post-build check for old C runtime libraries.

## VCPKG_POLICY_ALLOW_RESTRICTED_HEADERS

Disables vcpkg's post-build check for taking headers normally reserved by the operating system and standard library.

## VCPKG_POLICY_CMAKE_HELPER_PORT

Marks that a port is intended to provide CMake functions to other ports, and that depending ports should load `vcpkg_port_config.cmake` set by this port.

## VCPKG_POLICY_DLLS_IN_STATIC_LIBRARY

Disables vcpkg's post-build check for DLLs generated by ports when a triplet requests a static build.

## VCPKG_POLICY_DLLS_WITHOUT_EXPORTS

Disables vcpkg's post-build check for DLLs without exports. DLLs without exports are usually not useful to callers. Providing a good dynamic linking experience on Windows requires that a library define a DLL interface. See also [`Do not add CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS`](../contributing/maintainer-guide.md#do-not-add-cmake_windows_export_all_symbols) in the maintainer guide.

## VCPKG_POLICY_DLLS_WITHOUT_LIBS

Disables vcpkg's post-build check for DLLs generated without import libraries. These DLLs can be more difficult to use as the functions exported by that DLL won't be visible to the linker.

## VCPKG_POLICY_EMPTY_INCLUDE_FOLDER

Disables vcpkg's post-build check for empty include directories. Empty include directories usually mean that headers are incorrectly installed.

## VCPKG_POLICY_EMPTY_PACKAGE

Disables all post-build checks and prevents a port from being included in a `vcpkg export`'d package for some package types.

## VCPKG_POLICY_MISMATCHED_NUMBER_OF_BINARIES

Disables vcpkg's post-build check for a matching number of release and debug binaries.

## VCPKG_POLICY_ONLY_RELEASE_CRT

Indicates that a port intends to install only components that use the release C Runtime libraries, and that linking with the debug C Runtime libraries is a bug. See also [`VCPKG_POLICY_SKIP_CRT_LINKAGE_CHECK`](#vcpkg_policy_skip_crt_linkage_check).

## VCPKG_POLICY_SKIP_ABSOLUTE_PATHS_CHECK

Disables vcpkg's post-build check for absolute paths embedded in an installed file. Absolute paths generally break binary caching, as the installed tree may have a different root in different vcpkg instances.

## VCPKG_POLICY_SKIP_ALL_POST_BUILD_CHECKS

Disables all vcpkg's post-build checks.

## VCPKG_POLICY_SKIP_APPCONTAINER_CHECK

Disables vcpkg's post-build check for the appcontainer bit, even when a triplet requests targeting UWP.

## VCPKG_POLICY_SKIP_ARCHITECTURE_CHECK

Disables vcpkg's post-build check that binaries created by a port target the architecture requested by the triplet.

## VCPKG_POLICY_SKIP_COPYRIGHT_CHECK

Disables vcpkg's post-build check that a port installs a copyright file intended to contain the licensing information to use that port.

## VCPKG_POLICY_SKIP_CRT_LINKAGE_CHECK

Disables vcpkg's post-build checks for linking with correct C Runtime libraries entirely.

## VCPKG_POLICY_SKIP_DUMPBIN_CHECKS

This policy has no effect. In old copies of vcpkg it was intended to workaround environments which did not provide the `dumpbin` utility such as MinGW by disabling post-build checks that required it. In current copies of vcpkg, the features provided by `dumpbin` are now implemented directly without needing to invoke `dumpbin`.

## VCPKG_POLICY_SKIP_LIB_CMAKE_MERGE_CHECK

Disables vcpkg's post-build check for CMake configs for the release and debug configurations being merged into a single config. This is usually caused by forgetting to call [`vcpkg_cmake_config_fixup`](../maintainers/functions/vcpkg_cmake_config_fixup.md).

## VCPKG_POLICY_SKIP_MISPLACED_REGULAR_FILES_CHECK

Disables vcpkg's post-build check for regular files installed in places regular files are not intended to be. The searched locations should only contain directories.

## VCPKG_POLICY_SKIP_PKGCONFIG_CHECK

Disables vcpkg's post-build check for pkgconfig (`.pc`) files being installed in correct locations. Incorrectly installed `.pc` won't be found by `pkgconf` or `pkg-config`, or advertise architecture independence when that is not actually provided.

## VCPKG_POLICY_SKIP_USAGE_INSTALL_CHECK

Disables vcpkg's post-build check for forgotten usage text. This is triggered when a port contains a file named `usage` but no `${CURRENT_PACKAGES_DIR}/share/${PORT}/usage` exists, indicating it was likely a usage was intended to be installed but was not.
