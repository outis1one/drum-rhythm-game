# Drum Rhythm Game

A browser-based drum rhythm game. Notes scroll down the screen and you hit the matching drum pad in time — like Rock Band, but it runs entirely in your browser with no server, no dependencies, no install. Just open `index.html`.

Works with **keyboard**, **Wii Rock Band drum kit via USB**, or any gamepad.

## How to Play

1. Open `index.html` in Chrome or Edge
2. Pick a genre and rhythm (or a classical piece)
3. Click **Start**
4. Hit the pads when notes reach the line:
   - **F** = Red (Tom)
   - **G** = Yellow (Snare)
   - **H** = Blue (Hi-hat)
   - **J** = Green (Tom)
   - **Space** = Kick (Bass drum)

## Features

- **9 Genres**: Rock, Metal, Jazz, Hip Hop, Funk, Latin, Electronic, Country, Classical
- **146 Rhythms**: 120 drum patterns + 26 classical orchestral pieces
- **Classical Mode**: Synthesized orchestra plays automatically while you hit the melody notes on the pads. Choose between drum sounds or orchestral hit sounds.
- **26 Classical Pieces**: Beethoven's 5th, Hall of the Mountain King, O Fortuna, Ride of the Valkyries, Toccata & Fugue, Bolero, Also Sprach Zarathustra (2001), The Blue Danube, Flight of the Bumblebee, Fur Elise, Canon in D, Ode to Joy, 1812 Overture, and more
- **MP3 Jam Mode**: Load your own music and drum along freely
- **Multiplayer**: Take turns on the same rhythm, scores compared at the end
- **Pad Toggles**: Turn pads on/off to adjust difficulty — start with kick+snare, add more as you improve
- **Leaderboard**: Scores saved locally with player name, accuracy, and streak
- **Preview**: Hear any rhythm before playing
- **Gamepad Support**: Wii Rock Band drums via USB, auto-detected

## Synthesizer

All sounds are generated in real-time using the Web Audio API — no audio files needed:

| Sound | Method |
|-------|--------|
| Kick | Sine oscillator, 180Hz to 40Hz sweep |
| Snare | Highpass noise burst + 180Hz tone |
| Hi-hat | Highpass noise burst, very short |
| Toms | Sine oscillator pitch sweep |
| Strings | Sawtooth oscillator + lowpass filter |
| Brass | Square oscillator + lowpass filter |
| Woodwind | Triangle oscillator |
| Bass | Sine oscillator, low frequency |
| Timpani | Sine frequency sweep |
| Choir | Multiple detuned sine oscillators |

## Tech

- Pure vanilla JavaScript — no libraries, no build step, no server
- Single `index.html` file
- Web Audio API for all sound synthesis
- Canvas 2D for the note highway
- Gamepad API for drum kit input
- localStorage for score persistence
- Works on Windows, Linux, and Mac

## License

[MIT](LICENSE)
