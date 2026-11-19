# Local recognizer reproducible build

Manual build of public Apache-2.0 source https://github.com/lichess-org/vosk-browser at 50a6347c5167f95c458ffde0fd064569ae108ddf. The workflow adds the documented Emscripten DYNAMIC_EXECUTION=0 compiler setting, not a generated-binary patch. https://emscripten.org/docs/tools_reference/settings_reference.html#dynamic-execution

The official upstream ccoreilly builder tag 0.0.6 is resolved to sha256:a71beab353712ad6c052d07f9665bee748fd0109bf331c77d988f308ebb6de9a. Upstream build recipe: https://github.com/ccoreilly/vosk-browser/blob/master/Makefile . The fork documents a different builder; compatibility is tested by compilation rather than assumed. No artifact is claimed until build and execution checks pass.

Standard public Linux runner, manual invocation only, read-only workflow token, no secrets, container network disabled during compilation, exact public tool versions, one-day artifact retention. No application source, user data or deploy credentials. Artifacts are build outputs, not a release. WebAssembly CSP permission is still needed separately. No recognition model is bundled.

Build compatibility: the pinned compiler rejects LLVM bitcode named .a. Source Makefile intermediate targets use .bc instead; existing static archive inputs are unchanged. This is a source build-rule correction, not a binary patch.
