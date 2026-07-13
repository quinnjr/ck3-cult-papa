# The Moon Must Fall: Ser Cult Papa the Hedge Knight

A Crusader Kings III mod that adds **Ser Cult Papa**, a wandering hedge knight who
arrives at the court of any player-controlled king or emperor on a random date and
raves about his sworn quest to destroy the Moon.

## What it does

A Don Quixote arc in four events. Once per campaign, on a random year (~10% chance per
year once you hold a kingdom or empire title), a provincial gentleman who read too many
chivalric romances and astronomical treatises arrives at your court as a self-invented
knight-errant, riding a swaybacked nag he calls *Moonbane*, squire PapaLaCroix in tow. He
serves the Lady Conspiracy Dearest — the Dawn herself — and has sworn to bring down her pale usurping
rival, the Moon.

- **`cult_papa.0001` — The Ingenious Knight of the Waning Moon.** Recruit him and PapaLaCroix,
  fund the emprise (25 gold for prestige and *Patron of the Lunar War*), or throw him out
  (*The Moon's Gaze*).
- **`cult_papa.0002` — The Giant of the Mill.** He tilts at your capital's windmill,
  certain it is one of the Moon's earthly engines; a jealous enchanter is blamed for
  the transformation. Someone should pay the miller.
- **`cult_papa.0003` — The Vigil of the Pale Foe.** His original knighting was performed
  by an innkeeper, so he stands a proper vigil over his arms until moonrise and asks
  you to do it right.
- **`cult_papa.0004` — The Knight Wakes.** Years later a fever breaks, lucidity returns,
  the quest is gently renounced, and the war against the Moon ends. You keep the
  *Memory of the Moon Knight*.

## Layout

```
ck3-cult-papa/
├── descriptor.mod                                  # in-mod descriptor
├── cult_papa.mod                                   # copy to .../Crusader Kings III/mod/
├── common/
│   ├── on_action/cult_papa_on_actions.txt          # yearly_playable_pulse hook + random-date gate
│   ├── scripted_character_templates/cult_papa_templates.txt   # the knight and PapaLaCroix
│   └── modifiers/cult_papa_modifiers.txt
├── events/cult_papa_events.txt                     # namespace cult_papa, events 0001–0004
├── gfx/portraits/portrait_modifiers/zz_cult_papa_appearance.txt  # forced red hair + full beard
└── localization/english/cult_papa_l_english.yml    # localization
```

## Install (manual)

1. Copy this folder to `~/.local/share/Paradox Interactive/Crusader Kings III/mod/ck3-cult-papa`
   (on Windows: `Documents/Paradox Interactive/Crusader Kings III/mod/`).
2. Copy `cult_papa.mod` into the `mod/` directory itself (next to the folder), and make sure
   its `path=` line points at the folder from step 1.
3. Enable the mod in a playset in the CK3 launcher.

## Testing / tuning

- To fire the event immediately, open the console (`-debug_mode` launch option) and run:
  `event cult_papa.0001`
- To make the random visit more or less frequent, edit `chance_to_happen` in
  `common/on_action/cult_papa_on_actions.txt`.
- The visit is once-per-campaign, gated by the `cult_papa_has_visited` global variable.
  Clear it in console with `effect remove_global_variable = cult_papa_has_visited` to re-arm.

## Notes for extending

- **All** script files (`.txt` and `.yml`) must be UTF-8 with BOM — the game logs a
  lexer error for every file without one. Localization uses the `_l_english.yml` suffix.
- `create_character` cannot assign DNA; forced appearance is done via a portrait
  modifier (`dna_modifiers` keyed on the `is_cult_papa` character flag).
- New events go in `events/` under the `cult_papa` namespace (`cult_papa.0003`, ...).
- `supported_version` in the two `.mod` files is set to `1.19.*` — bump as CK3 updates.
