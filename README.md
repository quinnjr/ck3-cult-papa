# The Moon Must Fall: Ser Cult Papa the Hedge Knight

A Crusader Kings III mod that adds **Ser Cult Papa**, a wandering hedge knight who
arrives at the court of any player-controlled king or emperor on a random date and
raves about his sworn quest to destroy the Moon.

## What it does

A Don Quixote arc. Once per campaign, on a random year (~10% chance per year once you
hold a kingdom or empire title), a provincial gentleman who read too many chivalric
romances and astronomical treatises arrives at your court as a self-invented
knight-errant, riding a swaybacked nag he calls *Moonbane*, squire PapaLaCroix in tow.
He serves the Lady Conspiracy Dearest (the Dawn herself) and has sworn to bring down
her pale usurping rival, the Moon.

- **`cult_papa.0001` — The Ingenious Knight of the Waning Moon.** Recruit him and PapaLaCroix,
  fund the emprise (25 gold for prestige and *Patron of the Lunar War*), or throw him out
  (*The Moon's Gaze*, which arms the moon-madness chain below).
- **`cult_papa.0002` — The Giant of the Mill.** He tilts at your capital's windmill,
  certain it is one of the Moon's earthly engines, and blames a jealous enchanter for
  the transformation. You can pay the miller or declare the mill defeated.
- **`cult_papa.0003` — The Vigil of the Pale Foe.** His original knighting was performed
  by an innkeeper, so he stands a proper vigil over his arms until moonrise and asks
  you to do it right.
- **`cult_papa.0005` — A Formal Declaration of War.** He points out the realm has been
  prosecuting hostilities without declaring them. A document addressed to *The Moon,
  Usurper of the Night, Dragger of Seas, Occupant of the Sky* awaits your seal
  (*At War with the Moon*). A herald, who happens to be PapaLaCroix's cousin, is
  retained to read it from the tower at every moonrise.
- **`cult_papa.0006` — The Night the Moon Died.** Three nights after he shoots an arrow
  at the Moon, a lunar eclipse. He accepts the garrison's apologies, earns the nickname
  *the Moonsbane*, and, when the enemy recovers, explains that the Moon is a dynasty
  and this has been a war of succession all along.
- **`cult_papa.0007` — The Lunar War Council.** Years in, the whole court has bought in:
  the physician prescribes against moonlight, the marshal has siege plans blocked on a
  ladder, the spymaster tracks the Moon's agents (the tides, several owls, one specific
  cat), and Quartermaster-General PapaLaCroix keeps the ledger.
- **`cult_papa.0004` — The Knight Wakes.** Years later a fever breaks his madness, he
  renounces the quest, and the war against the Moon ends. You keep the *Memory of the
  Moon Knight*, and one option finally grants PapaLaCroix his island.
- **`cult_papa.0008` — A Letter from the Island.** If you granted the island, word
  arrives a year on from Governor PapaLaCroix: a hill named the keep, a goat named
  Ser Cult Papa, and a cup raised each month when the Moon dies its little death.

Turning the knight away has a price. Under *The Moon's Gaze*, **`cult_papa.0020` —
What the Knight Knew** fires a year or three later: the clear nights get to you, and
you may go lunatic (35% if you resist, 65% if you compose "one formal insult, purely
to know how it feels"). If the madness takes hold, **`cult_papa.0021` — The Moon
Collects** follows and can kill you (35% if you answer the enemy in person from the
tower, 15% if you bar the shutters), with a bespoke death reason: *died of
moon-madness, at moonrise, mid-insult*.

While the knight lives at your court, a yearly pulse (~25%) also fires one of three
repeatable gags: **`cult_papa.0010` — The Enemy in the Pond** (he charges the Moon's
reflection in your fishpond), **`cult_papa.0011` — The Interrogation of the Owl** (he
questions a captured enemy agent for eleven hours), and **`cult_papa.0012` — The
Tourney of the Silver Shield** (he unhorses your champion over a polished shield and
takes the shield prisoner).

## Layout

```
ck3-cult-papa/
├── descriptor.mod                                  # in-mod descriptor
├── cult_papa.mod                                   # copy to .../Crusader Kings III/mod/
├── common/
│   ├── on_action/cult_papa_on_actions.txt          # yearly_playable_pulse hook + random-date gate
│   ├── scripted_character_templates/cult_papa_templates.txt   # the knight and PapaLaCroix
│   ├── nicknames/cult_papa_nicknames.txt           # "the Moonsbane"
│   ├── traits/cult_papa_traits.txt                 # the Shitposter trait
│   ├── deathreasons/cult_papa_death_reasons.txt    # death by moon-madness
│   └── modifiers/cult_papa_modifiers.txt
├── events/cult_papa_events.txt                     # namespace cult_papa, events 0001–0021
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
- The repeatable flavor events (0010–0012) require the `cult_papa_knight` character
  variable, set on the player when the knight is recruited in `cult_papa.0001` and
  cleared on his death in `cult_papa.0004`. They won't fire from console on a save
  where he was never recruited.

## Notes for extending

- **All** script files (`.txt` and `.yml`) must be UTF-8 with BOM — the game logs a
  lexer error for every file without one. Localization uses the `_l_english.yml` suffix.
- `create_character` cannot assign DNA; forced appearance is done via a portrait
  modifier (`dna_modifiers` keyed on the `is_cult_papa` character flag).
- New events go in `events/` under the `cult_papa` namespace (`cult_papa.0008`, ...).
- `supported_version` in the two `.mod` files is set to `1.19.*` — bump as CK3 updates.
