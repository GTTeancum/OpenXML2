# OpenXML2 implementation

- [ ] Create the user-requested active goal in the new task.
- [ ] Reproduce the binary inventory with a reusable read-only analysis tool;
  identify this installed build by hash and retain private metadata under out/.
- [ ] Recover a meaningful game function, its needed object fields and DLL
  contracts; implement source and a reproducible 32-bit build.
- [ ] Compare the replacement with the original on valid matching inputs,
  including side effects and engine calls. Use process-local testing only.
- [ ] Expand to a playable movement/combat path; measure actual recovery pace
  and report remaining dependencies, rather than extrapolating from a tiny stub.
- [ ] Reconstruct executable initialization, gameplay, UI, progression, saves,
  and required platform glue while retaining unchanged engine DLLs.
- [ ] Remove every original executable-code fallback and verify a clean source
  build with representative gameplay, level transitions, and save/load tests.
- [ ] Document recovered architecture, build prerequisites, extension points,
  contribution workflow, and appropriate licensing of original project code.
- [ ] Add XML1-specific functionality after the XML2 foundation is working.
