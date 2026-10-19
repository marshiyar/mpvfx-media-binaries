# mpvfx-media-binaries

Compiled libraries of the MpVFX media engine, published as releases of this repository. Each release holds one
package per platform and a `SHA256SUMS` file:

| Platform | Package |
| --- | --- |
| macOS arm64 | `mpvfx-media-<version>-macos-arm64.tar.gz` |
| Linux x86_64 | `mpvfx-media-<version>-linux-x86_64.tar.gz` |
| Windows x86_64 (MSVC) | `mpvfx-media-<version>-windows-x86_64.zip` |

Each package contains:

- `lib/`: the dynamic library: `libmpvfx_ffi.dylib` (install name `@rpath/libmpvfx_ffi.dylib`), `libmpvfx_ffi.so` (soname `libmpvfx_ffi.so`), or `mpvfx_ffi.dll` with its import library `mpvfx_ffi.dll.lib`. It exports only the C API.
- `include/mpvfx_media.h`: the C API.
- `include/module.modulemap`: a Clang and Swift module named `CMpvfxMedia`.
- `LICENSE` and `NOTICE`.

Pin a release by its SHA-256 from `SHA256SUMS`. A published version is never replaced.

Ship the library beside your program, or on its library search path (`@rpath` on macOS).

## Licence

The engine is proprietary; see `LICENSE` in each package. Third-party notices are in `NOTICE`.

## How releases are made

`.github/workflows/build.yml` builds and tests the libraries on all three platforms. It runs only when started by
hand or by a release tag, never for pull requests. When publishing, it creates the release here.
