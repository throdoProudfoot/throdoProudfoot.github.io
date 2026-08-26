# TOR2E — Changelog · vNext

> **Release date:** TBD  
> **Platform:** Foundry VTT 14

## Rolls & Dice

### Fixed

- Corrected roll-result classification across the full range from **Failure** to **Extraordinary Success**.
- Task rolls now honor Foundry's configured chat-message mode.
- Skill migration preserves both **rank** and **favoured** state.
- Active regression coverage now protects:
  - Weary Success Dice results `1–3`;
  - Miserable + Eye of Sauron automatic failure;
  - Gandalf Rune and Eye of Sauron results;
  - Favoured rolls;
  - Ill-favoured rolls;
  - Favoured / Ill-favoured cancellation;
  - Hope bonus;
  - Inspired bonus;
  - manual bonus Success Dice;
  - manual penalty Success Dice;
  - zero-floor handling for Success Dice pools;
  - manual companion support bonus dice;
  - Fellowship Focus / support interactions.

### Added

- Added configurable `min` / `max` result options to `TORSuccessDie.roll()`.
- Added deterministic dice programming for automated tests through `DiceRig`.

---

## Character, Adversary, NPC & Community Sheets

### Fixed

- Prevented Active Effects from being re-applied during full form submissions.
- Editable Active-Effect-targeted inputs now safely reconcile effective displayed values with stored source values.
- Community editable fields migrated to the effective-value display model.
- NPC editable fields migrated to the effective-value display model.
- Actor data preparation remains synchronous.
- Corrected Character Sheet tab activation for Endurance and Hope maximum values.
- Restored reliable persistence checks for Adversary **Endurance** and **Hate**.
- Improved NPC card editor/sidebar layout.
- NPC editors now reliably preserve **Occupation** and **Description**.
- Lore editors now reliably preserve **Role** and **Description**.
- Simplified and normalized Community Patron handling when Characters are dropped on a Community.
- Community updates are built from source data more safely.
- Embedded Active Effect creation now returns the created documents as expected.

### Refactored

- Removed legacy `use-source-value` infrastructure.
- Removed the custom Actor and Item sheet submission queue.
- Encapsulated source data in sheet context.
- Simplified Character-type handling in extended Actor data preparation.

---

## Persistence & Data Models

### Fixed

- Player-hero data persistence is covered after closing and reopening the sheet.
- Armour creation and persistence are covered through the Foundry UI.
- Every simple Item type is covered for UI creation.
- Effect-enabled Item types are covered for persistence.
- Community Connections and Patrons are covered for persistence.
- Skill `rank` and `favoured` values are preserved through migration-model handling.
- Removed partial-update side effects from `migrateData()`.

---

## Migration Safety

### Fixed

- A failed world upgrade no longer advances the stored world version.
- Migration/model handling no longer relies on partial-update side effects.

---

## Combat & Chat Messages

### Fixed / Covered

- Character weapon rolls are regression-tested with combat metadata.
- Protection actions are tested against the correct adversary Actor.
- Protection-roll chat-message handling has been hardened.
- NPC skill rolls are checked for correct Actor attribution in chat.
- Community traveller skill rolls are checked for correct member Actor, action name and dice pool.
- Character-roll chat selectors and assertions have been updated for current Foundry output.

---

## Items, Journey Logs & Interface

### Fixed

- Restored scrollable Item-sheet content.
- Removed obsolete Item-sheet color alias and debug logging.
- Journey Log updates now target the relevant collection entries instead of replacing broader data unnecessarily.
- Added z-index handling to Foundry window resize handles.
- Corrected the legacy **SWERPG** Character Sheet label to **TOR2E**.

### Changed

- Item-sheet dimensions and layout structure were normalized.
- Item icons were adjusted for more consistent display.
- Undertaking description layout was aligned with the rest of the system.
- Combat Task sheet layout was reorganized for readability.

---

## Foundry VTT 14 Compatibility

### Fixed

- Updated E2E user-selection handling for Foundry VTT 14 Build 366+.
- Added handling for asynchronous Foundry tour overlays in browser tests.
- Sheet and document interactions were updated around current Foundry V14 behavior.

---

## Automated Regression Suite

### Added

New or expanded E2E coverage includes:

- Character creation and persistence;
- simple Item creation;
- Armour persistence;
- Effect-enabled Item persistence;
- Community Connections and Patrons;
- Character rolls and Short Rest;
- Weary skill rolls;
- Gandalf Rune / Eye of Sauron outcomes;
- Favoured / Ill-favoured states;
- Miserable + Eye of Sauron;
- Bonus / Penalty Success Dice;
- Hope and Inspired bonuses;
- NPC skill-roll attribution;
- Community traveller skill-roll attribution;
- Character weapon / protection workflows;
- manual companion support;
- Fellowship Focus / support interactions.

### Refactored

- A regression test campaign can now keep its Foundry world open and close it once at the end of the campaign workflow.
- Test helpers now use stronger readiness and document-property synchronization patterns.
- E2E TypeScript/JSDoc conventions were tightened.
- Dice-test guidelines were documented.

---

## Tooling & Engineering

### Changed

- Migrated the JavaScript lint stack to **ESLint 10 flat config**.
- Updated project documentation references from `docs/` to `documentation/`.
- Updated legacy project references from SWERPG to TOR2E.
- Added and expanded ADRs covering:
  - direct `_source` write prohibition;
  - update behavior from `_preUpdate`;
  - source vs. effective/system value handling.
- Added audit documentation and methodology around Actor source/system discrepancies.
- Cleaned up obsolete debug output.

---

## Notes

- Many commits in this release are regression-test additions rather than new table-facing features.
- Their purpose is to protect existing TOR2E behavior and make future changes safer.
- No release version number or release date has been assumed in this document; replace `vNext` / `TBD` when the release is cut.
