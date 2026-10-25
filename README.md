# skia-wasm-webgpu

Prebuilt [skia-bindings](https://crates.io/crates/skia-bindings) for `wasm32-unknown-emscripten`, with Skia's Graphite
running on WebGPU through Dawn's emdawnwebgpu Emscripten port (and Ganesh on WebGL 2). skia-safe publishes no such
build itself.

- `skia-emdawnwebgpu.patch`: the Skia changes (see its header).
- `.github/workflows/build.yml`: builds skia-bindings from crates.io against the patched Skia and publishes a release
  `<crate version>-<commit>` with `skia-binaries.tar.gz`. The pinned versions and features are at the top.

## Using it

1. Keep `skia-safe` from crates.io at the workflow's `CRATE_VERSION`, with the features in its `FEATURES`.
2. Download and unpack `skia-binaries.tar.gz` from a release.
3. Build with `SKIA_BINARIES_URL=file://<path to skia-binaries.tar.gz>`. Linking needs emsdk at `EMSDK_VERSION` and
   `--use-port=<emdawnwebgpu_pkg>/emdawnwebgpu.port.py` from Dawn's `DAWN_TAG` release.
