# Local recognizer reproducible build

Manual build of public Apache-2.0 source https://github.com/lichess-org/vosk-browser at 50a6347c5167f95c458ffde0fd064569ae108ddf. The workflow adds the documented Emscripten DYNAMIC_EXECUTION=0 compiler setting, not a generated-binary patch. https://emscripten.org/docs/tools_reference/settings_reference.html#dynamic-execution

The official upstream ccoreilly builder tag 0.0.6 is resolved to sha256:a71beab353712ad6c052d07f9665bee748fd0109bf331c77d988f308ebb6de9a. Upstream build recipe: https://github.com/ccoreilly/vosk-browser/blob/master/Makefile . The fork documents a different builder; compatibility is tested by compilation rather than assumed. No artifact is claimed until build and execution checks pass.

Standard public Linux runner, manual invocation only, read-only workflow token, no secrets, container network disabled during compilation, exact public tool versions, one-day artifact retention. No application source, user data or deploy credentials. Artifacts are build outputs, not a release. WebAssembly CSP permission is still needed separately. No recognition model is bundled.

Build compatibility: the pinned compiler rejects LLVM bitcode named .a. Source Makefile intermediate targets use .bc instead; existing static archive inputs are unchanged. This is a source build-rule correction, not a binary patch.

The builder's library layout is taken verbatim from ccoreilly/vosk-browser source revision 4b8eb257503108d96819854d3984372903c2259e src/Makefile (LIBS block), because the fork otherwise references nonexistent .a Kaldi intermediates.

## Current result

No usable artifact has been produced. Run 44461958599 reaches linking with DYNAMIC_EXECUTION=0 after the source Makefile compatibility corrections. It fails on undefined exported `_f_init` and reports unresolved Kaldi RNNLM / Fortran runtime symbols. These have not been suppressed, stubbed or patched in generated binaries. The fork and ccoreilly builder are not established as compatible. Next work must obtain a matching, provenance-verified toolchain/library set or build that set from pinned official sources before attempting runtime validation. No release has been created.

## Bounded matching-source attempt

The current workflow now uses ccoreilly/vosk-browser at 4b8eb257503108d96819854d3984372903c2259e with its own digest-pinned 0.0.6 builder, without fork source or compatibility patches. Recursive submodule pins are recorded in the artifact. Build-time flags DYNAMIC_EXECUTION=0, SINGLE_FILE=0, EXPORT_ES6=1 and USE_ES6_IMPORT_META=0 produce a separately served WASM/ES-module core without modifying generated code. This core has a different browser contract from the previous prototype; output must undergo actual grammar/model/runtime and worker-only-CSP checks before any use. No claim of browser compatibility yet.
