# mpvfx-media-binaries

Compiled libraries of the MpVFX engines, published as releases of this repository: the media engine (releases
`media-v<version>`) and the keyframe engine (releases `keyframes-v<version>`). Each release holds one package per
platform and a `SHA256SUMS` file.

## Media engine

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

## Keyframe engine

| Platform | Package |
| --- | --- |
| macOS arm64 | `video-keyframing-<version>-macos-arm64.tar.gz` |
| Linux x86_64 | `video-keyframing-<version>-linux-x86_64.tar.gz` |
| Windows x86_64 (MSVC) | `video-keyframing-<version>-windows-x86_64.zip` |

Each package contains one folder `video-keyframing-<version>-<platform>/` with:

- `lib/`: the dynamic library: `libcvkf.1.dylib` (install name `@rpath/libcvkf.1.dylib`) with a `libcvkf.dylib` link,
  `libcvkf.so.1` (soname `libcvkf.so.1`) with a `libcvkf.so` link, or `cvkf.dll` with its import library `cvkf.lib`.
  It exports only the `cvkf_*` functions of the C API, has no debug information and needs only system libraries
  (libc, libm and libgcc_s on Linux; libc++ on macOS; the MSVC runtime on Windows).
- `include/cvkf.h`: the C API.
- `LICENSE`, `NOTICE` and `third_party/core-math/LICENSE`.
- `SHA256SUMS-keyframes-<version>`: the SHA-256 of the other files in the folder.

## Using a release

Pin a release by its SHA-256 from `SHA256SUMS`. A published version is never replaced.

Ship the library beside your program, or on its library search path (`@rpath` on macOS).

## Licence

The engine is proprietary; see `LICENSE` in each package. Third-party notices are in `NOTICE`.

## How releases are made

`.github/workflows/build.yml` builds and tests the libraries on all three platforms. It runs only when started by
hand or by a release tag, never for pull requests. When publishing, it creates the release here. Run by hand, it
takes the component, the full source commit SHA, whether to publish, and for the keyframe engine the version.
