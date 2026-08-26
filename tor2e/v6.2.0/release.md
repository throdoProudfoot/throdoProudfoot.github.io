# TOR2E — Release Notes · vNext

> **Release date:** TBD  
> **Platform:** Foundry VTT 14

## A release focused on trust at the table

This release is less about adding another layer of interface and more about making the system behave the way players and Loremasters expect it to behave.

Across rolls, sheets, Active Effects, migrations, Communities, NPCs and combat interactions, the focus has been the same: **the value you see should be the value the system uses, the data you enter should remain saved, and the result of a roll should remain faithful to The One Ring rules.**

A large part of the work also strengthens the automated regression suite behind TOR2E. Most of that work is invisible during play, but it gives the system a much stronger safety net for future releases.

---

## 🎲 Rolls are more reliable

The roll engine and Roll Dialog received a broad reliability pass covering many situations that matter during actual play.

### Better rule handling

- **Weary rolls** correctly handle Success Dice results of `1–3`.
- **Miserable + Eye of Sauron** correctly produces an automatic failure.
- **Gandalf Rune** and **Eye of Sauron** outcomes are covered by deterministic regression tests.
- **Favoured**, **Ill-favoured**, and cancellation between the two states are now explicitly protected by automated tests.
- Roll result classification is verified from **Failure** through **Extraordinary Success**.
- Task rolls now respect Foundry's configured **chat message mode**.

### Roll Dialog bonuses

The Roll Dialog is now protected against several regressions around manual modifiers:

- manual **bonus Success Dice**;
- manual **penalty Success Dice**;
- Success Dice pools correctly stop at a **minimum of zero**;
- spending **Hope**;
- the **Inspired** bonus;
- manual **companion support** bonus dice.

These mechanics remain player-driven where the system currently expects a manual choice, but their impact on the final dice pool is now covered end-to-end.

---

## ⚔️ Combat and action messages are safer

Combat-related rolls now have stronger regression coverage around the complete table workflow.

- Weapon rolls are exercised with their combat context.
- Attack chat messages preserve the information required by follow-up actions.
- Protection-roll actions are tested against the correct adversary.
- Skill rolls triggered from NPCs and Community journey roles are checked to ensure the resulting chat message is attributed to the correct Actor and action.

This reduces the risk of a roll being mechanically correct while being attached to the wrong character, adversary or action in chat.

---

## ◆ Active Effects now behave more predictably

A major internal cleanup changes how editable sheet fields interact with Active Effects.

Previously, some sheet submissions could cause an Active Effect to be effectively applied again when unrelated data was edited. This could make displayed and stored values drift apart.

The new model is simpler from a user point of view:

- **editable fields display their effective value**;
- changes are safely converted back to the underlying source value when needed;
- Active Effects no longer get unintentionally re-applied during normal form submissions;
- Actor data preparation remains synchronous and predictable.

The result is a much more coherent rule:

> **What you see on the sheet is the value you are editing, without corrupting the stored base value behind an Active Effect.**

This work covers Character, Adversary, NPC and Community sheets and is backed by dedicated regression tests.

---

## 💾 Stronger data persistence

A large group of regressions now checks what matters after the sheet is closed and reopened: **your data is still there**.

Coverage now includes:

- Player-hero data;
- Adversary **Endurance** and **Hate**;
- NPC **Occupation** and **Description**;
- Lore Actor **Role** and **Description**;
- Community **Connections** and **Patrons**;
- Armour;
- all simple Item types;
- Item types using Active Effects;
- skill **rank** and **favoured** state across data-model migration.

The NPC, Lore and Item sheet editors were also adjusted where necessary so these workflows can be used and tested reliably.

---

## 👥 Communities are more dependable

Community handling received several targeted fixes.

- Patron handling when dropping Characters onto a Community has been simplified and made more consistent.
- Community updates are now built from source data more safely.
- Community editable fields follow the same effective-value model as other Actor sheets.
- Connections and Patron persistence are now covered end-to-end.

The goal is to make the Community sheet behave like a dependable campaign record rather than a fragile collection of linked fields.

---

## 🧭 Migration failures are safer

World upgrades now fail more defensively.

If a migration cannot complete successfully, TOR2E no longer advances the stored world version as if the upgrade had succeeded.

This prevents a failed migration from leaving the world marked as upgraded when its data may not actually be in the expected state.

Migration handling for skill rank and favoured state has also been reinforced.

---

## 🖥️ Sheet and interface polish

Several smaller interface issues have been corrected along the way:

- NPC card editor and sidebar layout improvements;
- Item sheets regain reliable scrolling;
- Item-sheet dimensions and layout have been normalized;
- Undertaking description layout has been aligned with the rest of the system;
- combat task sheet readability has been improved;
- resize handles now stay usable above window content;
- the Character Sheet label now correctly references **TOR2E** rather than the legacy **SWERPG** name;
- Character sheet tabs correctly expose the relevant Endurance and Hope values.

These changes are individually small, but together they make the ApplicationV2 interface feel more consistent.

---

## 🧪 A much stronger regression safety net

This release significantly expands TOR2E's end-to-end coverage.

The automated suite now exercises complete Foundry workflows for:

- Character creation and persistence;
- simple and Active-Effect-enabled Items;
- Communities, Connections and Patrons;
- Character rolls and Short Rest;
- Weary rolls;
- Gandalf Rune and Eye of Sauron outcomes;
- Favoured and Ill-favoured rolls;
- Hope and Inspired bonuses;
- manual bonus and penalty dice;
- NPC skill-roll attribution;
- Community traveller-roll attribution;
- weapon and protection rolls;
- manual companion support;
- Fellowship Focus and support interactions.

The E2E harness itself was also improved so a regression campaign can keep its Foundry world open for the duration of the test workflow instead of repeatedly opening and closing it.

For players and Loremasters, the important part is not the test count itself: it is that **more of the rules and workflows used at the table are now automatically checked before a release ships.**

---

## 🔧 Technical maintenance

Under the hood, this release also includes:

- migration to **ESLint 10 flat config**;
- updated E2E documentation and JSDoc conventions;
- deterministic dice testing through a dedicated `DiceRig`;
- explicit project guidance around source data, effective values and Active Effects;
- removal of legacy source-value infrastructure;
- removal of the custom Actor/Item sheet submission queue;
- targeted collection updates for Journey Logs;
- cleanup of obsolete debug logging and legacy styling aliases;
- documentation and ADRs clarifying safe Foundry document-update patterns.

---

## Upgrade

1. Make sure your world is running on a supported **Foundry VTT 14** build.
2. Back up your world before updating, as you should for any system update.
3. Update TOR2E through Foundry's package manager.
4. Open the world normally.
5. If a migration reports a failure, stop and investigate it rather than continuing with the assumption that the world was upgraded.

---

## In short

This release is about **confidence**.

Confidence that a sheet does not quietly rewrite a value.  
Confidence that an Active Effect does not apply twice.  
Confidence that closing and reopening a document does not lose your changes.  
Confidence that a Hope bonus, a Weary die, a Protection roll or an Eye of Sauron result behaves the same way every time.

That foundation matters because it makes the next features safer to build — and safer to use at the table.
