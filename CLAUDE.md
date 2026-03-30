# 🥁 Drum Rhythm Game — Claude Handoff Document

This file tells Claude exactly what this project is, what has been built, what needs to be built next, and how everything works. Read this entire file before making any changes.

---

## What This Is

A browser-based drum rhythm game built as a single HTML file. It works like Rock Band — notes scroll down the screen and the player hits the matching drum pad in time. It runs entirely in the browser with no server, no dependencies, no npm. Just open `index.html`.

The game was originally built to work with a **Wii Rock Band drum kit connected via USB** on Windows, Mac, and Linux. It also works with keyboard keys.

---

## Current File Structure

Right now everything is in one file: `index.html`. As this project grows, split it as follows:

```
drum-rhythm-game/
├── index.html          ← main shell, links all JS/CSS
├── css/
│   └── style.css       ← extract all <style> here
├── js/
│   ├── audio.js        ← AudioContext, drum sounds, synthesizer
│   ├── rhythms.js      ← all genre drum patterns
│   ├── classical.js    ← classical pieces, note sequences, synth orchestra
│   ├── game.js         ← game loop, scoring, hit detection, players
│   ├── canvas.js       ← all canvas drawing
│   ├── input.js        ← keyboard + gamepad input
│   └── menu.js         ← UI screens, genre tabs, pad toggles
└── CLAUDE.md           ← this file
```

---

## Hardware Setup

- **Drum kit**: Wii Rock Band drums connected via USB dongle
- **Pads**: Red, Yellow, Blue, Green (4 pads) + Kick pedal
- **OS**: Must work on Windows 11, Linux, and Mac
- **Browser**: Chrome or Edge recommended for gamepad API support

### Gamepad Button Mapping (Wii Rock Band via USB)
```
Button 0 → Blue  (lane 2)
Button 1 → Green (lane 3)
Button 2 → Red   (lane 0)
Button 3 → Yellow(lane 1)
Button 4 → Kick  (lane 4)
Button 8 → Kick  (lane 4) — alternate
```

### Lane Definitions
```
Lane 0 = Red    — Tom high  — keyboard: F
Lane 1 = Yellow — Snare     — keyboard: G
Lane 2 = Blue   — Hi-hat    — keyboard: H
Lane 3 = Green  — Tom low   — keyboard: J
Lane 4 = Kick   — Bass drum — keyboard: Space
```

---

## What Has Been Built

### Screens
1. **Menu screen** — mode select, rhythm picker, pad toggles, players, leaderboard
2. **Game screen** — canvas highway, HUD (score/streak/acc/player), countdown
3. **Leaderboard screen** — all saved scores sorted by score

### Modes
1. **Rhythm Mode** — select a genre + rhythm, notes scroll, drum pattern plays as audio background, score your hits
2. **MP3 Jam Mode** — load your own MP3, it plays in background, drum freely (no chart, no scoring)

### Genres & Rhythms (8 genres × 15 patterns = 120 rhythms)
- Rock, Metal, Jazz, Hip Hop, Funk, Latin, Electronic, Country
- Each rhythm has: name, BPM, bars, pattern array
- Pattern format: `{t: beat_offset, l: lane}` where t is within a 4-beat bar

### Rhythm Pattern System
```javascript
// Example pattern entry
{n:"Basic Rock", bpm:90, bars:8, p:[
  {t:0, l:4},   // kick on beat 1
  {t:0, l:2},   // hihat on beat 1
  {t:1, l:1},   // snare on beat 2
  // etc.
]}
```
- `bars` controls how many times the 4-beat pattern repeats
- Notes are built by looping the pattern for the full bar count
- Only notes on **active pads** appear on screen (user can toggle pads)

### Pad Toggle System
- Menu has colored buttons for each pad/kick
- Toggle off = pad makes sound when hit but shows no notes and doesn't score
- Designed for beginners — start with kick+snare, add more pads as you improve

### Scoring
- Hit within 0.17 seconds of note time = counts as hit
- Within 0.05s = "PERFECT" (green), otherwise "GOOD" (yellow)
- Miss = streak resets
- Score = 100 × min(streak, 10) per hit
- Scores saved to localStorage key `"drgame5"`

### Multiplayer (Take Turns)
- Add players in menu (up to N players)
- Each player takes a turn on the same rhythm
- After all turns, results shown sorted by score
- All scores saved to leaderboard

### Audio System
- Uses Web Audio API — no external files needed
- **Critical**: AudioContext must be unlocked on user gesture — especially important on Linux/Chrome
- Unlock happens on any click, keydown, touchstart, mousedown
- Two separate AudioContexts: `previewAc` (menu preview) and `gameAc` (in-game)
- Both must call `.resume()` aggressively

### Drum Sounds (Synthesized)
```
Kick  → sine oscillator, 180Hz → 40Hz sweep, ~0.3s
Snare → highpass noise burst + 180Hz tone body
Hi-hat→ highpass noise burst, very short ~0.05s
Tom   → sine oscillator, 160Hz → 64Hz sweep
Tom2  → sine oscillator, 120Hz → 48Hz sweep
```

### Canvas Layout
- Top 78% = 4 pad lanes side by side
- Bottom 22% = kick zone (full width, centered)
- Hit line at 76% down the pad zone
- Notes fall from top, future notes above hit line
- Note Y position: `noteY = HIT_Y - (noteTime - currentSongTime) * SPEED`
- SPEED = 260px/second
- Notes outside screen bounds are skipped (culled)
- Missed notes (past hit line by HIT_WIN) fade to 20% opacity

### Preview System
- In menu, click Preview to hear any rhythm before playing
- Auto-loops the pattern using scheduled Web Audio nodes
- Plays all drum hits as audio so user can hear the beat
- Stops cleanly when switching rhythms or starting game

---

## What Needs To Be Built Next

### 1. Classical Music Genre Tab (PRIORITY)

Add a new genre called **"Classical"** with the following pieces. Each piece needs:
- A synthesized melody/orchestral background that plays automatically
- A separate set of "hittable" notes (melody notes only) that scroll on screen
- The player hits the melody rhythm, background fills in the rest

#### Pieces to implement (all public domain compositions):

| Piece | Composer | Notes |
|-------|----------|-------|
| Beethoven's 5th (Opening) | Beethoven | DA DA DA DUM — 3 same pad + 1 different |
| Hall of the Mountain King | Grieg | Starts slow, accelerates — great difficulty curve |
| O Fortuna | Orff | Heavy rhythmic hits, powerful |
| Ride of the Valkyries | Wagner | Galloping rhythm pattern |
| Mars, Bringer of War | Holst | Heavy 5/4 march |
| Toccata & Fugue in D Minor | Bach | Famous DUN DUN DUN opener |
| William Tell Overture (Gallop) | Rossini | Fast galloping rhythm |
| Bolero | Ravel | Literally a drum pattern that builds — perfect |
| Also Sprach Zarathustra | Strauss | DA DAAAA DA DUM (2001 theme) |
| Barber of Seville Overture | Rossini | Bugs Bunny classic |
| The Blue Danube | Strauss Jr. | Waltz rhythm |
| Sabre Dance | Khachaturian | Very fast and fun |
| Night on Bald Mountain | Mussorgsky | Fantasia — dark and dramatic |
| Sorcerer's Apprentice | Dukas | Fantasia — Mickey Mouse |
| Swan Lake (Theme) | Tchaikovsky | Elegant waltz |
| Morning Mood | Grieg | Peer Gynt — gentle build |
| In the Hall of the Mountain King | Grieg | (same as above, confirm not duplicate) |

#### How Classical Mode Should Work
1. Player selects a classical piece
2. Game starts with countdown
3. **Background**: Full synthesized orchestral arrangement plays automatically (Web Audio oscillators, multiple voices, proper frequencies)
4. **Foreground**: Only the main melody notes scroll down as hittable notes
5. Player hits the melody rhythm — satisfying because they're "playing" the famous part
6. Scoring same as rhythm mode

#### Synthesizer Architecture for Classical
Use multiple oscillator types for different instruments:
```javascript
// Strings — sawtooth oscillator + lowpass filter
// Brass   — square oscillator + envelope
// Woodwind— triangle oscillator
// Bass    — sine oscillator, low frequency
// Timpani — sine sweep, like kick but lower
// Choir   — multiple detuned sine oscillators
```

Use a note-scheduling system:
```javascript
// Notes stored as: {time, freq, duration, instrument, volume}
// Schedule all notes at game start using AudioContext time
// This ensures perfect sync regardless of JS timing
```

#### Note Frequencies Reference
```javascript
const NOTES = {
  C3:130.81, D3:146.83, E3:164.81, F3:174.61, G3:196.00,
  A3:220.00, Bb3:233.08, B3:246.94,
  C4:261.63, D4:293.66, E4:329.63, F4:349.23, G4:392.00,
  A4:440.00, Bb4:466.16, B4:493.88,
  C5:523.25, D5:587.33, E5:659.25, F5:698.46, G5:783.99,
  A5:880.00, C6:1046.50
};
```

#### Beethoven's 5th — Starter Implementation
```
Opening motif (G minor):
- G4 (short) → G4 (short) → G4 (short) → Eb4 (long)
- F4 (short) → F4 (short) → F4 (short) → D4 (long)

Drum mapping:
- Short notes → Red pad (lane 0)
- Long notes  → Green pad (lane 3)
- Background: strings + brass arrangement
```

---

### 2. Audio Improvements
- Make drum sounds punchier with a slight distortion/clipping on kick
- Add reverb to classical orchestral sounds (ConvolverNode or simple delay feedback)
- Consider a master volume slider in the game HUD (not just menu)

### 3. Visual Improvements  
- Scrolling speed lines in lane backgrounds for motion feel
- Note "explosion" particle effect on perfect hit
- Combo multiplier display (currently capped at 10x but not shown prominently)
- BPM display during game

### 4. Gameplay Features
- **Practice mode**: slow down to 50/75% speed
- **Difficulty**: Easy (fewer notes), Medium (all notes), Hard (+ extra fills)
- **Endless mode**: rhythm loops until you quit, cumulative score
- **Song length selector**: 1 min / 2 min / full length

### 5. Quality of Life
- Remap button in-game HUD (not just standalone soundboard)
- Volume control per sound type (kick louder than hihat etc.)
- "How to play" screen
- GitHub Pages deployment so it runs at a URL without downloading

---

## Known Issues & Bugs

1. **Linux audio** — AudioContext needs aggressive `.resume()` on every user interaction. Already fixed in current code but watch for regressions.
2. **Pad toggle visual** — toggling a pad on/off used to flicker (toggle on click). Fixed to be one-directional but confirm behavior.
3. **High BPM rhythms** — at 200+ BPM notes can stack visually. May need note size scaling by BPM.
4. **MP3 Jam scoring** — currently no chart in MP3 mode, just free play. Future: beat detection to generate a chart from the MP3.

---

## Tech Constraints

- **No external libraries** — pure vanilla JS, Web Audio API, Canvas 2D
- **No build step** — must work by opening index.html directly
- **No server required** — localStorage for scores, no backend
- **Single HTML file** initially, refactor to multi-file as needed
- **Cross-platform** — Windows 11, Linux (Ubuntu/Fedora), Mac, any modern browser

---

## Style Guide

- Dark theme: background `#0a0a0f`, cards `#13131f`, borders `#222`
- Lane colors: Red `#e53e3e`, Yellow `#d69e2e`, Blue `#3182ce`, Green `#38a169`, Kick `#805ad5`
- Accent: Purple `#805ad5` for buttons/highlights
- Font: system sans-serif, no imports needed
- Minimal UI — game canvas should dominate the screen

---

## How To Test

1. Open `index.html` in Chrome or Edge
2. Click any genre tab → select a rhythm → click Preview to hear it
3. Click Start → watch countdown → notes should fall → hit F/G/H/J/Space
4. For drum kit: plug in USB, hit any pad to wake gamepad API, should show "🎮 Connected"
5. Test on Linux: click something first before hitting Preview — audio needs a gesture

---

## Questions / Decisions Needed

- [ ] Should classical pieces loop or play once through?
- [ ] Should the synthesized orchestra volume be adjustable separately from drum hit volume?
- [ ] For Bolero specifically — should difficulty increase as the piece builds (more notes appearing)?
- [ ] Should we add a GitHub Pages deploy so it runs at a public URL?
