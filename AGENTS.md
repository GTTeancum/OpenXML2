# Scope

- Work directly in `D:\Programming\GitHub\OpenXML2`; use explicit working
  directories if the task's initial directory is elsewhere.
- Recover the PC executable into buildable, maintainable source. Keep the
  original Alchemy and other installed DLLs unchanged. Start with x86 ABI.
- Keep game testing in `C:\Games\X-Men Legends II`. Preserve the original
  `XMen2.exe`, assets, configuration and saves. Prefer separately named test
  executables and bounded, opt-in instrumentation with reversible deployment.
- Do not commit proprietary binaries, assets, RAM dumps, or raw disassembly.
- Keep OpenXML1 work paused. Do not modify that repository or its runtime.

# Computer and process control

- Never use Computer Use, desktop capture, screen takeover, UI automation, or
  host keyboard/mouse/controller input. Leave interactive operation to the user.
- Process-local synthetic input is permitted only inside the targeted game or
  harness; it must not generate host input or affect other applications.
- Use source, files, logs, native framebuffer captures and non-interactive
  commands. Normal targeted process launch/monitor/termination is permitted.
- Do not stop or modify unrelated processes. Never automatically restart a
  game the user closed. Announce when an automated run disables user controls.
- Builds: one worker, BelowNormal priority, affinity 0xF, maximum 2048 MiB per
  owned compiler. Preserve these limits in build helpers.

# Delivery and communication

- Prioritize playable reconstructed game code, then broader coverage and FPS.
- Validate against original behavior; distinguish static evidence, isolated
  comparisons, and actual gameplay verification. Do not invent timing estimates.
- The user explicitly requested an active goal in the new task. Create it at
  the start without a token budget. Keep it incomplete until the executable is
  buildable from source with no original EXE-code fallback and representative
  movement/combat, progression, and save/load validation succeeds against the
  unchanged DLLs. A single reconstructed function is only an early milestone.
- Keep acknowledgements direct. Do not use praise formulas when corrected.
- Before a playable interactive handoff, announce **Controls enabled: ready for
  you to test**, then pause automated replacement/testing for user feedback.
