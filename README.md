# Drum Rhythm Game

A browser-based drum rhythm game. Notes scroll down the screen and you hit the matching drum pad in time — like Rock Band, but it runs entirely in your browser with no server, no dependencies, no install. Just open `index.html`.

Works with **keyboard**, **Wii Rock Band drums**, **Xbox/PS Rock Band drums**, **Guitar Hero drums**, or any USB gamepad. Includes a **Remap Pads** button to configure any controller.

## How to Play

1. Open `index.html` in Chrome or Edge
2. Pick a genre and song
3. Adjust speed/volume sliders if desired
4. Click **Start**
5. Hit the pads when notes reach the line:
   - **F** = Red (Tom)
   - **G** = Yellow (Snare)
   - **H** = Blue (Hi-hat)
   - **J** = Green (Tom)
   - **Space** = Kick (Bass drum)
   - **Escape** = Pause

## Features

- **14 Genres** across two modes: synth orchestra songs + drum beat patterns
- **65 synth pieces** with full synthesized orchestra background (48 minutes)
- **120 drum patterns** across 8 genres
- **Drums or Orchestra mode** — choose whether pad hits play drum sounds or the actual melody note
- **Speed control** — slow down to 50% for practice or speed up to 150%
- **Volume control** — adjustable master volume
- **Pause/Resume** — press Escape or the pause button mid-song
- **Gamepad Remap** — configure any USB drum kit with the Remap Pads button
- **Multiplayer** — take turns, scores compared at the end
- **Pad Toggles** — turn pads on/off to adjust difficulty
- **Preview** — hear any song before playing
- **Leaderboard** — scores saved locally

## Song List

### Singalong (10 songs)
- Drunken Sailor (Sea Shanty)
- Molly Malone (Irish, 1880s)
- Whiskey in the Jar (Irish Traditional)
- The Parting Glass (Irish/Scots Traditional)
- Amazing Grace (1779)
- Auld Lang Syne (1788)
- When the Saints Go Marching In (Spiritual)
- Oh My Darling, Clementine (1884)
- Scarborough Fair (English Medieval)
- My Bonnie Lies Over the Ocean (Scottish, 1881)

### Christmas (10 songs)
- Jingle Bells (1857)
- Silent Night (1818)
- Deck the Halls (1862)
- We Wish You a Merry Christmas (1500s)
- O Christmas Tree (1824)
- The First Noel (1823)
- Joy to the World (1719)
- Away in a Manger (1885)
- 12 Days of Christmas (1780)
- Hark the Herald Angels Sing (1840)

### Folk (8 songs)
- Oh! Susanna (Stephen Foster, 1848)
- Greensleeves (English, 1580)
- Camptown Races (Stephen Foster, 1850)
- Red River Valley (American, 1870s)
- Home on the Range (American, 1870s)
- Yankee Doodle (American, 1770s)
- Turkey in the Straw (American, 1820s)
- Danny Boy (Irish, 1910s)

### Classical (26 pieces)
- Beethoven's 5th (Opening)
- Hall of the Mountain King (Grieg)
- O Fortuna (Orff)
- Ride of the Valkyries (Wagner)
- Mars, Bringer of War (Holst)
- Toccata & Fugue in D Minor (Bach)
- William Tell Overture — Gallop (Rossini)
- Bolero (Ravel)
- Also Sprach Zarathustra (R. Strauss) — 2001: A Space Odyssey
- Barber of Seville Overture (Rossini)
- The Blue Danube (J. Strauss II) — 2001: A Space Odyssey
- Sabre Dance (Khachaturian)
- Night on Bald Mountain (Mussorgsky) — Fantasia
- Sorcerer's Apprentice (Dukas) — Fantasia
- Swan Lake Theme (Tchaikovsky)
- Morning Mood (Grieg)
- Flight of the Bumblebee (Rimsky-Korsakov)
- Dance of the Sugar Plum Fairy (Tchaikovsky)
- 1812 Overture Finale (Tchaikovsky)
- Habanera from Carmen (Bizet)
- Spring from Four Seasons (Vivaldi)
- Fur Elise (Beethoven)
- Canon in D (Pachelbel)
- Hungarian Dance No. 5 (Brahms)
- Ode to Joy (Beethoven)
- William Tell Overture — Storm (Rossini)

### Video Games (5 pieces)
- Korobeiniki / Tetris Theme (Russian Folk, 1861)
- Turkish March (Mozart)
- Hungarian Rhapsody No. 2 (Liszt)
- Can-Can (Offenbach)
- Kalinka (Russian Folk, 1860)

### Chiptune Originals (6 pieces, composed by Claude.ai)
- Pixel Quest (Platformer)
- Starfield (Space Shooter)
- Dragon's Keep (RPG Overworld)
- Turbo Dash (Racing)
- Dungeon Crawl (Dark Adventure)
- Victory Fanfare (Boss Defeated)

### Drum Patterns (120 patterns)
- **Rock** (15): Basic Rock, Classic Rock, Punk Rock, Arena Rock, and more
- **Metal** (15): Double Bass, Thrash, Doom Metal, Blast Beat, and more
- **Jazz** (15): Jazz Ride, Bebop, Bossa Nova, Fusion, and more
- **Hip Hop** (15): Boom Bap, Trap, Lo-Fi, Drill, and more
- **Funk** (15): Classic Funk, Ghost Notes, P-Funk, Afrobeat, and more
- **Latin** (15): Samba, Salsa, Reggaeton, Cumbia, and more
- **Electronic** (15): Four on the Floor, Breakbeat, DnB, Dubstep, and more
- **Country** (15): Two-Step, Bluegrass, Rockabilly, Gospel, and more

## USB Drum Kit Compatibility

The Gamepad API works with any USB controller. Use the **Remap Pads** button to configure your kit.

| Kit | Connection |
|-----|-----------|
| Wii Rock Band drums | USB dongle (default mapping) |
| Xbox 360 Rock Band drums | USB wired |
| PS3/PS4 Rock Band drums | USB |
| Guitar Hero drums | USB |
| Roland/Alesis/Donner | USB-MIDI adapter |
| Any USB gamepad | Remap to configure |

## Synthesizer

All sounds are generated in real-time using the Web Audio API — no audio files needed:

| Sound | Method |
|-------|--------|
| Kick | Sine oscillator, 180Hz to 40Hz sweep |
| Snare | Highpass noise burst + 180Hz tone |
| Hi-hat | Highpass noise burst, very short |
| Toms | Sine oscillator pitch sweep |
| Strings | Sawtooth + lowpass filter |
| Brass | Square + lowpass filter |
| Woodwind | Triangle oscillator |
| Bass | Sine oscillator, low frequency |
| Timpani | Sine frequency sweep |
| Choir | Multiple detuned sine oscillators |
| Chiptune | Square wave with pulse bass |

## Tech

- Pure vanilla JavaScript — no libraries, no build step, no server
- Single `index.html` file
- Web Audio API for all sound synthesis
- Canvas 2D for the note highway
- Gamepad API for drum kit input
- localStorage for scores and gamepad mapping
- Works on Windows, Linux, and Mac

## License

[MIT](LICENSE)
