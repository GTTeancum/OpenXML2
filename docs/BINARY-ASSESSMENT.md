# XML2 PC binary assessment — September 9, 2026

## Scope and conclusion

Read-only inspection of `C:\Games\X-Men Legends II\XMen2.exe` and its installed
DLLs. No game execution, binary modification, DLL replacement, or host input.
The intended deliverable is reconstructed, maintainable game source that builds
against the unchanged proprietary Alchemy DLLs. Engine source recovery is outside
this proposed scope.

The installed executable is a promising starting point: named engine interfaces,
C++ runtime type information, inheritance descriptors, and virtual-function
tables survive. This is direct evidence for reconstructability, not a completed
decompilation or a supported calendar estimate.

## Executable identity

- File: 3,129,344 bytes; SHA-256
  `146cd9c316edb57a267cd73753a7ce9af647e52aab750d449c6b278fb4a1669b`.
- PE machine `0x14c`: 32-bit x86; preferred image base `0x400000`.
- Entry point `0x6725f4`; ordinary x86 startup instructions disassemble there.
- `.text`: 2,611,125 virtual bytes (approximately 2.49 MiB).
- No COFF symbols, executable exports, PE debug directory, or embedded PDB path
  found. No `.pdb`, `.map`, `.h`, or `.lib` files found in the installation scan.
- This hash identifies this installed copy; no claim that it is an unmodified
  retail executable or matches another project's supported build.

## DLL interfaces

The EXE has 989 static imports across 16 modules. Of these, 794 entries target
seven Alchemy DLLs: IGSg (290), IGAttrs (134), IGDisplay (9), IGGfx (61),
IGUtils (15), IGMath (125), and IGCore (160). Their decorated C++ import names
provide class/namespace names and encoded signatures. Examples demangle to:

- `Gap::Display::igControllerManager::getController(unsigned int) const`,
  returning `Gap::Display::igController*`, using `__thiscall`.
- `Gap::Math::igVec3f::addScaled(float, const igVec3f&)`, returning `void`,
  using `__thiscall`.
- `Gap::Sg::igAnimationCombiner::updateAnimStates(__int64)`, returning `int`.

All 900 EXE imports whose modules are present in this installation resolve by
name or ordinal in those DLL export tables. This is a static export-resolution
check, not a runtime or transitive-dependency validation. Indirect virtual calls,
callbacks, dynamically loaded APIs, and inline object access add contracts beyond
the static import list. Export names alone do not recover full object layouts.

Keeping these DLLs entails retaining their 32-bit ABI, packing, calling
conventions, allocation ownership, and callback expectations. A 64-bit rebuild
cannot directly link and call these 32-bit DLLs.

## Game-side structure actually recovered

The initial scan finds 1,059 C++ RTTI-like name strings. Six selected classes
were followed through type descriptors, complete-object locators, inheritance
descriptors, and candidate vtables pointing into executable code.

`CActor -> CPhysicalEntity -> CGameEntity -> CActionEntity -> CEntity`

- CActor type descriptor: `0x6d5c80`; vtable: `0x682ccc`.
- CPhysicalEntity type descriptor: `0x6d57d4`; vtable: `0x68285c`.
- CEntity type descriptor: `0x6d5368`; vtable: `0x686644`.
- CHud type descriptor: `0x6e46d4`; vtable: `0x69dca4`, deriving from IHud.

Vtable candidates have consecutive pointers into `.text`; exact table extents
and method meanings still require further analysis. Actor and physical-entity
entries at `0x422b20` and `0x41c630` have the standard shape of deleting
destructors. This provides concrete object-lifetime entry points for investigation.

The `friction` string at `0x68a2b0` has a code-operand reference at `0x49bd2f`;
`gravitymod` at `0x689d84` has one at `0x4989fc`. These are investigation leads,
not recovered movement equations. `setVelocity` and `setNoGravity` strings also
exist; the simple direct-reference scan did not resolve their callers.

## Next proof

Recover one bounded game function and the object fields/interfaces it needs,
compile it for x86 against the unchanged engine, and compare its behavior with
the original. Use actual reconstruction and validation results to assess pace.
No function has yet been rebuilt or behaviorally validated in this inspection.

Local generated metadata: `out/xml2-inspection/binary-inventory.json` and
`out/xml2-inspection/class-evidence.json` (gitignored). Analysis used Python
pefile, Capstone, and the Windows symbol undecorator. Export enumeration raised
pefile's default 8,192-symbol cap to avoid truncating large Alchemy export tables.
