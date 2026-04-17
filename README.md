# MTG Commander Judge App

A mobile-friendly, offline tournament tool for running **Commander pod events** without relying on spreadsheets, internet access, or complicated pairings software.

This app is built for judges, organizers, and tournament staff who want a clean way to manage pods, track scores, correct mistakes, and keep the event moving with as little friction as possible.

---

## Purpose

This app is designed to run **Commander pod-based tournaments** with:

- manual point entry
- pod generation
- round history
- player add/drop tools
- repair options when mistakes happen
- optional Round 1 seeding by **Random** or **Infamy**

It is intentionally built around **manual score control** instead of hidden scoring logic so the judge always stays in charge of final results.

---

## Core Design Philosophy

This app is built around a few simple principles:

- **Manual points are the source of truth**
- **The judge controls the event**
- **Standings should not update until a round is finalized**
- **Mistakes should be fixable without wrecking the tournament**
- **The interface should stay usable on a phone-sized screen**
- **Pods should stay balanced and avoid awkward 5-player groups**

---

## Pod Structure Rules

This app supports:

- **4-player pods**
- **3-player pods when needed**

This app does **not** support:

- **5-player pods**

The pod builder prefers 4-player pods first, then uses 3-player pods to absorb uneven player counts.

### Examples

- 8 players → 4 / 4
- 10 players → 4 / 3 / 3
- 11 players → 4 / 4 / 3
- 14 players → 4 / 4 / 3 / 3
- 17 players → 4 / 4 / 3 / 3 / 3

If the active player count cannot be split cleanly into 3-player and 4-player pods, the app will stop round generation until the player count is corrected.

---

## Scoring System

Each pod must total exactly **10 points**.

The app uses **manual point entry only**. It does not auto-calculate placements or split points behind the scenes.

### Standard 4-player pod balance
- 1st = 4
- 2nd = 3
- 3rd = 2
- 4th = 1

Total = 10

### Standard 3-player pod balance
- 1st = 4
- 2nd = 3
- 3rd = 3

Total = 10

### Why 3-player pods use 4 / 3 / 3

This keeps every pod worth the same total number of points.

- 4-player pod = 10 total points
- 3-player pod = 10 total points

That prevents smaller pods from being worth less than larger pods and helps keep standings fair across uneven rounds.

### Why scoring is manual

Manual scoring was chosen because it is the simplest and most reliable way to preserve accuracy.

This avoids:
- hidden math
- automatic assumptions
- edge-case tie handling behind the curtain
- judge confusion over how the app arrived at a result

The app validates only one thing:

**Every pod must total exactly 10 points before the round can be finalized.**

---

## Round 1 Seeding Options

Before starting the event, you can choose how Round 1 is seeded:

### Random
Players are shuffled randomly into pods.

### Infamy
Players are sorted by Infamy score and distributed across pods using seeded placement logic for Round 1.

This seed mode is locked visually once the tournament begins so the event setup is clear at a glance.

---

## Main Controls

### Start Tournament
Builds Round 1 using the selected seed mode.

### Add Player
Adds a player before the event starts.

### Add Late Player
Adds a player after the event has already started.

Late-added players:
- do not get inserted into a round that already exists
- become available for future rounds only

### Drop / Undrop
Marks a player as dropped or restores them to active status.

Dropped players:
- remain in standings/history
- are excluded from future pod generation

### Finalize Round
Locks the current round and updates standings.

A round cannot be finalized unless:
- every pod has scores entered
- every pod totals exactly 10 points

### Reopen Current Round
Unlocks the most recent finalized round without deleting it.

Use this when:
- the pods were correct
- the scores need to be corrected

### Undo Last Round
Deletes the most recently created Swiss round and rewinds the event state one round at a time.

Use this when:
- pod construction needs to be rebuilt
- player pool changes require a repair
- you need to undo a round entirely

### Build Next Round
Generates the next Swiss round using the current active player list and standings.

### Save / Load
Stores or restores the event state locally in the browser.

### Reset Tournament
Clears the event and starts over.

---

## Pod Repair Controls

### Swap With
During an **open** Swiss round, each player row includes a **Swap with** dropdown and a **Swap** button.

This allows manual repair of pods without rebuilding the entire round.

Use this when:
- a specific pod needs correction
- two players need to be exchanged between pods
- the generated pods are close, but not quite right

This was chosen instead of drag-and-drop so the app stays more stable and mobile-friendly on smaller screens.

---

## Round History

The app includes a **Round History** panel that shows:

- each prior round
- whether the round is open or finalized
- the pods in that round
- the scores entered for each pod

This gives judges a quick audit trail without needing a separate spreadsheet.

---

## Final Pod

If enabled before the event starts, the app can create a **Final Pod** for the top 4 players after Swiss is complete.

The Final Pod:
- is optional
- uses the same manual 10-point scoring model
- must also total exactly 10 points before finalization

If the Final Pod ends with a tie for highest points, the champion remains unresolved until the tie is broken manually.

---

## Typical Judge Workflow

### Normal round flow
1. Build or begin the current round
2. Enter pod scores manually
3. Verify each pod totals 10
4. Finalize the round
5. Build the next round

### If the scores are wrong
1. Reopen Current Round
2. Correct the scores
3. Finalize again

### If the pods are wrong
1. Undo Last Round
2. Adjust player status if needed
3. Rebuild the round

### If a player drops after a round
1. Finalize the current round
2. Drop the player
3. Build the next round

### If a late player must be added
1. Add Late Player
2. Build the next round when ready

If they need to be included immediately and the current next round is already built:
1. Undo Last Round
2. Add the player
3. Rebuild the round

---

## What This App Is Not Trying To Be

This app is intentionally **not** trying to be:

- a fully automated scoring engine
- a placement interpreter
- a drag-and-drop pod editor
- a 5-player pod manager
- an online sync platform
- a hidden logic system that makes judgment calls for you

It is a **judge control tool**, not a replacement for the judge.

---

## Recommended Use

This app is best for:

- local Commander events
- casual-competitive leagues
- store-run pod tournaments
- mobile-first event administration
- organizers who want something simpler than a spreadsheet but more controlled than paper notes

---

## Notes

- This app is intended to run **offline**
- Save often during live events
- Manual scoring is intentional and should remain the final source of truth
- If the app appears stale after an update on GitHub Pages, refresh the browser cache

---

## Future Maintenance Notes

If future changes are made, they should preserve the core design priorities:

- manual scoring only
- mobile-friendly controls
- no 5-player pods
- clear judge override options
- no hidden scoring assumptions
