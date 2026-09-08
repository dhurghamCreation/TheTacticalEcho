# THE TACTICAL ECHO — The Chrono-Archive    https://tactical-3ag51vgq1-dhurgham-s-projects.vercel.app/


A single-file, self-contained browser game (no build step, no dependencies). Open
`tactical_echo.html` in any modern desktop or mobile browser and play.

> *"The Archive is erasing itself. Every gate forgotten, every corridor unmade.
> Yet you found a flaw in its logic — what is remembered can be replayed."*

## How to play

You are an Archivist exploring the semi-sentient Chrono-Archive. Each hall you
enter must be solved by **recording echoes of yourself**, then letting your past
selves perform tasks in parallel with your present body.

| Input | Action |
| --- | --- |
| `WASD` / Arrow keys | Move |
| `R` | Record a loop (leave an echo of yourself) |
| `E` | Interact: take/place/throw a torch, **grip a City-Stone and drag it any direction**, or crank an opened gear |
| `X` | Open the **Whisper Composer** (leave instructions for the next echo) |
| `P` / `Esc` | Pause / settings menu |
| `M` | Toggle sound |
| `C` | Chrono-Archæology Codex |
| Touch | Virtual joystick + LOOP / ACT / WHISPER buttons |

### The loop economy — Anchors

Each hall gives you a fixed number of **Anchors** (see the HUD chip). Recording
an echo is *not* free forever: the Archive taxes the loop with every echo you
cast, so the **cost of your Nth echo is N anchors**. Replicating ten ghosts to
solve one door now bankrupts you — you have to reuse echoes, whisper them to
do several jobs, and spend each Anchor deliberately. Perfect runs now mean
deciding exactly how few versions of yourself can do the job.

### Handling City-Stones — grip & drag

Sometimes a stone sits where you simply cannot get *under* it to push it.
That's a dead end for pushing — but not for you. Walk up to any City-Stone and
press `E` to **grip** it (a chain appears and the block pulses gold). Now just
**walk** to drag it in any direction — up, down, sideways, out of corners, up
onto shelves. Press `E` again to set it down. This makes every stone puzzle
solvable and never leaves a block permanently wedged or "stuck in the ground".

### Burn the brambles — fire clears the path

Some halls have overgrown knots of briar that block entire roads. Bring any
**lit flame** within reach and the knot catches, burns, and the way opens
(permanently). Carry a taper up, or fling one in from across a gap.

### Sealed wheels need a deliberate key — no more auto-thaw

Carrying fire beside a **still-sealed gear** no longer opens it on its own — the
Archive ignores a flame until you commit it. Walk up to a sealed wheel holding a
lit taper and the game shows **`E — INSERT TAPER`** over it. Press `E` and the
taper is **driven into the hub as a key**: the wheel thaws open in a burst, the
flame survives in your hand, and the hub can then be **cranked (E) for +1
Anchor**. The yellow "heating" glow never appears by proximity — only your drive
lights the wheel.

### The Unfed Hearth & Vessel wheels

The great vertical wheel in **The Unfed Hearth** opens **either way**: feed
the hammer an echo so it forges a Vessel, **or** carry a lit taper up to it and
drives it into the hub (`E`) to thaw the wheel. Both paths satisfy the same lock,
so the taper there always has a real purpose and you're never left stuck just
holding fire.

### Tapers become keys — seal the crank

A carried flame no longer lasts forever. When you stand beside an **opened,
uncranked gear** while holding a lit taper, the game shows **`E — INSERT TAPER ·
SEAL +1`** over the wheel. Press `E` and the taper is **driven into the hub as a
key**: it is spent (removed from your hands and the world), the wheel shows the
inserted taper sticking out of it, the label reads **SEALED**, and you earn +1
Anchor. No more finishing a hall while permanently towing a torch — fire is now
a resource you deliberately commit.

### Clean state transitions & aligned stones

- **Gears turn red → green smoothly** (and the door slab fades with them) —
  nothing pops between states in a single frame, and an opened gear stays green.
- **Gear labels (`CRANK +1` / `SPENT` / `SEALED`) now sit *inside* the wheel**
  on a small plaque, and door `SEALED` text sits on the slab itself — no text
  floats outside the shapes.
- **Low-road seal plates are no longer half-buried under the floor** (several
  were, which is why the grey pressing box could never sit on the yellow plate).
  Every plate now ends above the floor line.
- **Stones magnetically seat onto a seal** while you drag them, and a seal only
  activates when a stone genuinely covers ≥45% of it — a glancing touch no
  longer counts.

### Death is a scene, not a crash

When you die the game doesn't freeze, shake, or blink out. It runs a short
cinematic: slow-motion, a white impact flash, the body dissolving into rising
motes of light, red pressure vignette and letterbox bars — *without* the camera
shaking — and *then* a proper death report appears with your Loops, Sacrifices,
Time and Deaths, and two choices: **Re-Knit the Loop** (rewind and try again)
or **Return to Title**. The frame loop itself is guarded, so no hazard combination
can ever hard-freeze the tab again.

### Real light, real stone

Every flame in the Archive now casts **genuine light**: the world is dappled
with darkness and each torch, brazier, thawed wheel, active seal, vent jet,
exit beacon — even a sentry's red eye — carves a warm pool of visibility out of
the gloom. Stone blocks get carved chamfers and contact shadows, floors get
mortar seams and hand-set grit, and the whole scene lands with proper
grounding instead of flat "AI" shapes.

### Responsive polish

- **Hover is instant** — the welcome panel deliberately avoids a per-frame
  `backdrop-filter` blur and animates the logo with cheap `text-shadow` instead
  of `filter:drop-shadow`, so moving across the menu buttons never lags.
  Hover chimes are also throttled so fast mouse movement stays silky.
- **No sudden pops** — spike beds retract/extend with a smooth glide when you
  carry fire near them, and torches fade lit ⇄ unlit gently instead of
  vanishing. World note-plaques get a dark backing so text never mixes with
  the floor, and the mid-screen toast is solid so it can't blur into the world
  behind it.
- **The Hollow Thicket's spike-bed is ruthless** — it does *not* cower from
  fire (it pulses red to say so), so you can't just waltz through with a torch;
  time your crossing or use the stone instead. Normal spike-beds everywhere
  else still cower for fire.
- **The HUD only lives in the halls.** The logo, anchor/echo chips, title bar
  and Codex/Mute/Menu buttons are fully hidden on the welcome screen and only
  appear once you enter a room — nothing overlaps the title anymore.

### Music — why it might have been silent

Browsers block audible audio until the page has had some interaction, so a fully
automatic start is not always possible. The game now does its best: it boots the
AudioContext **the moment the loader starts**, keeps politely asking for the
track every ~0.6s while the logo plays (and again right when it finishes), then
**remembers** that it wanted music — so the very first click or keypress resumes
the audio and the track begins instantly. In browsers that allow autoplay the
song starts with no interaction at all; in browsers that don't, it starts on
your first click, which is the earliest the browser will legally let it.

### The Whisper system

While walking a pass you intend to record, press `X`. The composer lets you etch
contingency notes the echo will obey when its loop unwinds:

- **Hold still** for `N` seconds
- **Take** the nearest torch
- **Throw** (the torch you hold)
- **Throw if seen** (fling the flame the moment a sentry's gaze touches you)
- **Wait until seen**

Use the timeline to pick *when* in the loop the echo acts.

## The 28 halls

1. **The Threshold Vault** — a single plate, a single idea: record, step off, walk.
2. **The Twin Locks** — one lock wants a body, the other wants a stone.
3. **The Withering Span** — a crumbling bridge. *You weaponize its collapse.*
4. **The Whisper Gallery** — a sentry haunts the past. Carry the taper to the gear
   by the sealed door, or Whisper "throw if seen" so the flung flame survives.
5. **The Ember Forge** — the sacrifice hall. Summon an echo beneath the falling
   smelter and *let it die* so the Vessel can forge itself.
6. **The Convergence** — everything at once: hold, light, throw, walk.
7. **The Obsidian Script** — a razor-thin time trial. Beat the Archivist's ghost.
8. **The Ashen Toll** — the first use of the **spike-bed**: a City-Stone crossed
   where no body can follow, and a seal that still wants a living weight.
9. **The Hollow Bell** — a two-gear relay behind the anvil-yard sentry. **Carry
   both tapers** and walk them to each gear, or throw them.
10. **The Veined Caldera** — a body on the high seal, a stone on the low, and a red
    sentry patrolling the only road. A *thrown* torch sends it running to cover.
11. **The Hundred Cairns** — two seals, two City-Stones, and a spike-bed between.
    Roll one stone up to the high shelf and walk the other down the low lane.
12. **The Keyhole Chamber** — the **timed bonus**: hold the seal, feed the hammer
    so the Vessel forges, then slip past the iron eye to the far door.
13. **The Twin Flames** — the lesson room for **carrying two torches at once**:
    grab both, dodge the spike-tooth, and thaw the two gears that share one door.
14. **The Mirrored Halls** — leave an echo on each of the two seals; two remembered
    bodies hold the door open while you walk through.
15. **The Tide of Ash** — the **timed gauntlet**: echo on the high seal, wheel the
    City-Stone across the crumbling span and the spike-bed onto the low seal, and
    outrun the closing corridor.
16. **The Red Chain** — three gears, three doors, one carried flame. Thaw all
    three gears and the far door unseals; a sentry patrols the low road.
17. **The Sundered Vault** — the door needs **three seals held at once**. Leave an
    echo on each of the three plates and walk through an open vault.
18. **The Reverie Well** — two gears behind a spike field; **carry both tapers**
    along the low road or throw them across. The well drinks held flames.
19. **The Reliquary** — two seals that answer to stone. Roll one crate up to the
    high shelf and the other down the low road, minding the falling hammer.
20. **The Last Syllable** — the **timed finale**: forge the Vessel, slip past the
    iron sentry, and reach the exit *before the Archive closes its window*.
21. **The Loom of Threads** — an S-shaped hall of baffles. An echo on the high
    seal, the City-Stone on the low, and a carried taper melting the loom's hub
    open one door.
22. **The Cold Cistern** — the hall is split by a stone throat; only the mid
    passage crosses. Leave a memory on the high shelf, answer the low seal with
    a stone, and outrun the sentry.
23. **The Split Prism** — four cells braided by three doors, each answered by a
    different kind of you: body, flame, stone.
24. **The Filigree Gate** — an ice-spine with a narrow gate. Carry the taper
    through it, melt the hub, and satisfy both seals to unseal the far door.
25. **The Unfed Hearth** — sacrifice an echo to the hammer so the Vessel forges
    itself, hold the high seal, and slip past the iron eye.
26. **The Scalding Antrum** — the floor breathes. Two **flame vents** jet fire on
    a staggered rhythm; time your crossing or feed the vent your taper instead
    of your life.
27. **The Corridor That Hunts** — the **closing seam**. A wall of burning vault
    folds shut behind you and chases your heels the whole run. Melt both hubs
    and reach the door before the seam reaches you.
28. **The Hollow Thicket** — the Archive overgrew its own courtyard. **Burn the
    brambles** with a flame to clear the roads, hold the old seal with an echo,
    and warmth or a cast flame on the far hub opens the way out.

Every hall now wears its own **visual theme** (amber, frost, crimson, ember,
cobalt, verdigris, violet, ash, argent, rust, midnight) — different stone,
different light, different falling dust — so no two chambers look alike.

Persistent consequences follow you across revisits: **collapsed bridges stay
collapsed**, **thawed gears stay open**, **cranks stay spent**, and **sacrifices
are never undone**. The Archive remembers what you destroy.

*Engine note:* the City-Stone **H-blocks now push only from the side you're
actually standing on** — pushing right then pushing left never makes a stone
leap to the other side of you again, and crumbling bridge spans are walkable
floors (their danger is the collapse + pit below, not invisible walls).
Torches are fully **dual-wielded**: carry two, throw one at a time, and a held
flame melts a gear it touches.

### Flame is a real tool now

A carried, thrown, or planted taper does far more than look pretty:

- **Opens sealed wheels** — a lit flame does nothing until you press `E` beside a
  sealed hub to **drive the taper into it**; the wheel thaws open and stays open.
- **Retracts spike-beds** — carry fire across a trap and the teeth lower and
  stay down while your flame is near.
- **Blinds sentries** — firelight cuts an iron eye's sight range by almost half;
  stand in the light and it struggles to see you.
- **Opened gears are anchors in disguise** — press `E` beside a thawed gear to
  **crank +1 Anchor** (once each, permanently) — and opened gears also **relight
  any taper** you drop beside them and **repel sentries** for a few paces.
- **Banishes wraiths** — a shadow that was once you is burnt clean by any flame.

### New hazards

- **Flame vents** — the floor breathes. Jetting fire on a timed rhythm: step
  through a jet and it drinks a **held** flame instead of your life (if you're
  not carrying one, it unmakes you).
- **Wraith stalkers** — drifting Archive-shadows that wake and chase you within
  their radius. A flame evicts them permanently; otherwise they close in.
- **The closing seam** — behind you in **The Corridor That Hunts**, a vault wall
  slowly folds the hall shut. Keep moving.

### Stars & the PAR clock

Finish any hall *under its PAR* to earn stars (★★★ for finishing under 80% of
par, ★★ for a clean par, ★ for clearing it at all). A **time chip** appears in
the HUD for the timed halls; letting it hit zero ends the run on the *lose*
screen. The **level select** on the welcome screen shows your stars and best
times, and lets you jump to any hall.

### Boot & welcome screen

The game opens with a full **animated boot loader** — spinning chrono-orb logo,
"THE TACTICAL ECHO · THE CHRONO-ARCHIVE" title, a gradient progress bar with a
live percentage and stage captions ("binding the echoes…", "lighting the old
furnaces…"). It unloads **straight onto the welcome dashboard** — never into the
game world — and the title floats over a living animated backdrop (drifting fog,
silhouette arches, a floor reflection and a rain of golden dust):

- A glowing **gradient logo** with a little **floating ghost** riding on the "E"
  of ECHO — the Chrono-Archivist is watching over its own title.
- Stat cards for **Halls Sealed**, **Stars Earned**, **Best Clear** and **PAR budget**
  that **pop in one-by-one, count their numbers up, lift and shine when hovered**.
- An animated **completion progress bar** ("X% of the Archive mapped").
- A **vertical title menu** of brushed-metal buttons (riveted, bevel-lit plates
  that shine-sweep and lift when you hover) with every option stacked down the
  screen: **Enter the Archive**, **Select a Hall**, **Codex**, **Settings** and
  **Ghost Share**.
- The **level-select grid** (25 halls) with stars and best times, revealed by
  the "Select a Hall" button.
- The welcome screen is **clean**: the in-game HUD, the room-hint toast and the
  old decorative chrono-ring behind the stats are all hidden — nothing bleeds
  through the title.

### Pause / settings menu

`Esc` / `P` (or the **☰ Menu** button in the HUD on desktop, **II** on mobile)
opens the full menu:

- **Resume** — keep playing.
- **Restart Room** — reset the current hall's puzzle state.
- **Sound On/Off** — toggles all WebAudio cues (`M` toggles this too).
- **Music On/Off** — toggles the built-in procedural soundtrack (an ambient
  drone + wandering arpeggio synthesized live in WebAudio, so it works with
  **zero asset files**) — or an external track if you set `MUSIC_SRC`.
- **Shake On/Off** — disables screen shake for motion-sensitive players.
- **Advanced Settings** — the full tuning panel, reachable from pause or title:
  - **Sound / Music / Master volume sliders** — independent levels, saved.
  - **Particles** (Low / Medium / High) — ember, dust and burst intensity.
  - **Reduce Motion** — also kills the death slow-mo, letterbox bars and flash.
  - **Echo Trails** — glimmering recorded ghost paths in the air.
  - **Practice Mode** — echoes are free and death gently re-knits the loop, so
    you can learn every hall without losing runs.
  - **Reset Save** — wipes best times, stars and hall state.
- **Codex**, **Ghost Share**, **Return to Title**.

### Fullscreen

`fitCanvas` now **covers every pixel of the browser window** — no black bars, no
grey slivers. The 907×507 world is zoomed edge-to-edge, and on very tall phones
or ultrawide monitors a **follow-camera** pan-locks the player inside the visible
slice so you're never pushed off-screen. The HUD and settings buttons sit on top;
resize/re-orient freely and it re-fits instantly.

### Carrying two flames

The player can now carry **two torches at once** (a `Flames` chip in the HUD
shows how many). Press `E` to pick up a second torch while holding one; press
`E` away from any torch to **throw the first flame** while keeping the other.
Carried flames thaw gears only when you press `E` beside a sealed hub — so grab
both tapers, walk them to the gears, and drive one into each, or fling them one
at a time first and pick them back up.

### Sound & music — where to drop your files

The always-on ambient "drone" is **gone** (no more hum in the background) — every
sound the game makes is now an intentional event, all synthesized live in
WebAudio and toggleable with `M`:

| Event | Cue |
| --- | --- |
| Reaching the exit | gate groan + chime cascade (also the win fanfare) |
| The red SEALED doors sliding **open / shut** | low stone groan + thunk |
| Gears melting open | deep clunk + chime |
| A seal (plate) pressing / releasing | two-note chime |
| Your footsteps | soft textured thump + dust |
| **Ghost footprints** | spectral shimmer as echoes walk |
| Recording a loop | three-note rise |
| Throwing / taking / **setting down** a torch | whoosh / pickup tinkle / stone thud |
| **Open gear relighting a cold taper** | warm relight pop |
| **Brambles catching fire** | long crackle + whoosh |
| **Sentry spotting you** | alert alarm + red burst |
| Sentry snuffing a flame | hiss |
| **Wraith touching you** | cold descending gasp |
| **Vent jet igniting** | pressurised hiss |
| **Dragging / releasing a City-Stone** | heavy clank / settling thud |
| Smelter falling, bridge collapsing | bass crunch + shake |
| The closing Seam | deep rumble |
| Win / Lose | fanfare / low drone |
| Every menu / HUD button **+ hover** | soft click + quiet hover chime |

To use your own **music** or **sounds**, open `tactical_echo.html` and edit the
block near the top of the script marked **`SFX + MUSIC PLACEHOLDER`**:

```js
const MUSIC_SRC = 'assets/leberch-dark-585984.mp3';  // <<< in-game track
const TITLE_MUSIC_SRC = '';                          // <<< OPTIONAL separate title-menu track
const SFX_FILES = { exit:'', door:'', gear:'', button:'', win:'', lose:'' };
```

Drop a file next to the HTML (an `assets/` folder works), set the path, and the
game auto-plays it. **Title music and gameplay music are independent**: if you
set `TITLE_MUSIC_SRC`, the welcome screen plays that track while the halls play
`MUSIC_SRC`. If you leave `TITLE_MUSIC_SRC` empty, the menu uses your in-game
track too. No file at all? A light wandering chime (no drone) plays as a
fallback when you toggle **Music On**.

## Ghost Share

Every hall's win screen and the pause menu can export your *exact* loop chain:
an encoded string (`TE1:…`) containing every recorded path and whisper. Paste it
into the **Import** box to spawn those ghosts in your session and race/compare
against them. This is the "Ghost Share mode" from the roadmap — creators share
not just a map, but the *solution's motion*.

## Mobile

The same file is a touch-first game on phones/tablets:

- Left thumb **virtual joystick**.
- Right thumb buttons: **LOOP** (record), **ACT** (interact/throw), **WHISPER**.
- Responsive canvas + safe-area aware HUD; works in landscape.

## Implementation notes

- 20 interconnected rooms, each a genuine puzzle rather than a demo
  (spikes, sentries, crumbling spans, sacrificial smelters, dual-flame carries,
  three-seal vaults and a timed finale).
- Web Audio procedural audio: ambience, footsteps, thuds, chimes, snuffs,
  door/gear/plate cues, a win/lose fanfare **and a full procedural music engine**
  — all synthesized live, no assets required, plus a clearly-marked placeholder
  for dropping in real music files.
- Canvas-rendered humanoid figures with a real walk-cycle, idling, blinking and
  lean; a particle engine (dust, sparks, rings, motes, runes); an animated exit
  beacon; doors that slide open; and a screen-filling ambient backdrop.
- Animated boot loader (spinning chrono-orb + live progress %) leading to a
  welcome **dashboard** with stat cards, completion bar and level select.
- LocalStorage persistence for best times, completed halls, and per-room
  state (destroyed bridges, forged vessels, opened gears).
- All code is vanilla JS — no build step, no dependencies, works offline.

## Controls recap

Desktop: `WASD` / arrows move; `R` record; `E` act/throw; `X` whisper; `P`/`Esc`
pause + settings menu; `M` mute; `C` codex.
Mobile: joystick + LOOP / ACT / WHISPER buttons; pause + settings via top-right `II`.

---

*Four roadmap phases roll into one file: prototype loop recording, a vertical
slice of three connected rooms, an input-serialization export format, and
polish (sand-gold echo shaders, screen shake, responsive echoes, atmospheric
lighting).*
