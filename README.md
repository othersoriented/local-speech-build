# Local recognizer reproducible build

Manual, secret-free build of public Apache-2.0 ccoreilly/vosk-browser source at `4b8eb257503108d96819854d3984372903c2259e`, using its official 0.0.6 builder resolved to `sha256:a71beab353712ad6c052d07f9665bee748fd0109bf331c77d988f308ebb6de9a`.

The source and recursive submodule pins are retained with the artifact (`vosk` API at `7012103b3bc7a3da67faf9eb452991e60fcd8af7`). Build-time Emscripten settings are `DYNAMIC_EXECUTION=0`, `SINGLE_FILE=0`, `EXPORT_ES6=1`, `USE_ES6_IMPORT_META=0`. Generated JS and WASM are unmodified. AST verification rejects direct eval/Function execution. Compiler settings: https://emscripten.org/docs/tools_reference/settings_reference.html#dynamic-execution . Builder recipe: https://github.com/ccoreilly/vosk-browser/blob/4b8eb257503108d96819854d3984372903c2259e/Makefile .

Successful build: https://github.com/othersoriented/local-speech-build/actions/runs/44462567576 . Core JS: 145,680 bytes; WASM: 3,122,379 bytes. License, notice, hashes and source pins accompany the one-day artifact. No release is published and no recognition model is bundled.

Local verification of this exact core in Edge and automation WebKit used the official small English model and constrained Next/Back/Ingredients/Stop grammar. All commands passed with synthetic clean speech and deterministic Gaussian noise at 10 dB SNR; noise alone returned no command. Dedicated worker CSP permits wasm-unsafe-eval and same-origin fetch, without JS unsafe-eval; main page CSP remained script-src self. No off-origin requests occurred. This does not establish real microphone, physical phone, ordinary kitchen noise or general speech accuracy.

Workflow uses the standard public Linux runner, manual invocation only, read-only workflow token, digest-pinned container, disabled container networking during compilation, pinned artifact action and parser, and one-day artifact retention. It contains no private application source/data or deployment credentials.

Earlier attempts combined a fork with this builder and failed compatibility checks; those have been superseded by matching source and builder. The current output is a core ES module, not the fork's browser API. Browser adapters require separate contract and runtime verification before use.
