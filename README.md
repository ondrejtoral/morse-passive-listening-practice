# CW Morse Trainer - Passive Listening Practice

A browser-based Morse code (CW) training application designed to help amateur radio operators improve their listening comprehension through passive practice.

## Features

- **Multiple Practice Categories**
  - Q-Codes (QTH, QSL, QRM, etc.)
  - CW Abbreviations (73, CQ, TNX, etc.)
  - Contest Phrases (5NN, CQ TEST, etc.)
  - Realistic Callsigns (generated for CZ, DE, US, PL, UK, FR, IT, AT, SK, HU, ES, CA)
  - Equipment & Antennas
  - RST Signal Reports
  - Prosigns (AR, SK, BK, etc.)

- **Progressive Speed Training**
  - 25 WPM
  - 25 WPM with Farnsworth timing (20 WPM effective)
  - 20 WPM
  - 20 WPM with Farnsworth timing (17 WPM effective)
  - Text-to-speech pronunciation

- **Practice Modes**
  - **Shuffle Mode**: Randomized deck approach for varied practice
  - **Sequential Mode**: Go through phrases in order
  - **Auto-play Mode**: Continuous playback with 3-second intervals

## Usage

1. Open `app.html` in a modern web browser
2. Select a practice category from the dropdown
3. Click "Play" to start
4. Listen to the Morse code sequence at progressively slower speeds
5. The phrase is revealed visually and spoken after the Morse playback
6. Toggle shuffle and auto-play modes as desired

## Technical Details

- Pure HTML/CSS/JavaScript - no external dependencies
- Web Audio API for high-quality tone generation (600 Hz sine wave)
- Speech Synthesis API for pronunciation
- Settings saved to localStorage
- Responsive design for mobile and desktop

## Customization

You can easily add custom categories by editing the `content` object in the JavaScript section of `app.html`. Example:

```javascript
myCustomPhrases: [
    'TEST',
    'HELLO',
    'WORLD',
],
```

Then add a corresponding option to the category selector:

```html
<option value="myCustomPhrases">My Custom Phrases</option>
```

## Browser Compatibility

Requires a modern browser with support for:
- Web Audio API
- Speech Synthesis API
- ES6 JavaScript

Tested on Chrome, Firefox, Edge, and Safari.

## Credits

Vibecoded with Claude, 2025-12 OK1TRL

## License

Open source - feel free to use and modify for your own CW training needs.
