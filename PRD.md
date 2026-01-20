# Morse Code Reading Training Tool - PRD

## Overview
A local, browser-only, fully offline tool for **passive listening practice** of Morse code while mobile (walking, commuting, etc.). Designed for general CW proficiency through graduated speed repetition and audio reinforcement.

## Target Users
- Amateur radio operators learning CW (Continuous Wave/Morse code)
- Ham radio enthusiasts building CW proficiency for on-air operation
- Anyone wanting to improve Morse code reading speed through passive listening

## Core Concept
**Passive audio training tool** - No interaction, no quiz, just listening.
- Present Morse code audio at progressively slower speeds using Farnsworth timing
- Reinforce with text-to-speech readback after all Morse playback
- Designed for "hands-free" practice while walking or commuting with earphones

---

## Proposed Features

### 1. Playback Sequence ✅ CONFIRMED

**Fast-to-slow progression with Farnsworth stepping stones:**

1. **25 WPM full speed** (×1) - Challenge at target speed
2. **25 WPM Farnsworth** (20 WPM effective) (×1) - Same character speed, more spacing
3. **20 WPM full speed** (×1) - Comfortable recognition speed
4. **20 WPM Farnsworth** (17 WPM effective) (×1) - Final reinforcement with max spacing
5. **Text-to-speech** - Read phrase aloud for confirmation

**Rationale:**
- Start fast to build familiarity with target speed
- Use Farnsworth as stepping stones between speeds (unique approach!)
- Progressively slower playback aids pattern recognition without learning "slow Morse" habits
- TTS at end confirms what was heard

**Implementation Notes:**
- Farnsworth timing: increase inter-character spacing while keeping character speed constant
- 25 WPM Farnsworth (20 eff): Characters at 25 WPM, spacing to achieve 20 WPM overall
- 20 WPM Farnsworth (17 eff): Characters at 20 WPM, spacing to achieve 17 WPM overall

### 2. Content Categories ✅ IMPLEMENTED

Based on common ham radio CW usage patterns, organized by category:

#### **A. Contest Phrases** ✅ NEW
High-speed contest exchanges and common contest terminology:
- **Contest CQ**: CQ TEST, CQ CONTEST, TEST
- **Signal Reports**: 5NN, TU 5NN, 5NN TU, 599
- **Repeat Requests**: AGN, AGN PSE, PSE AGN, NR, CALL, UR CALL
- **Serial Numbers**: 001, 023, 100, 250, 500, 999
- **Confirmations**: R, R TU, QSL TU, QRZ
- **Exchange Formats**: 5NN 001, 5NN 100, TU 5NN 023
- **Grid Squares**: FN20, DM79, EM12
- **State/Province**: CA, NY, ON, BC
- **Zone Numbers**: ZONE 4, ZONE 14, ZONE 25
- **Contest Phrases**: QRZ TEST, RUN, QTC

#### **B. Prosigns (Procedural Signals)**
Special Morse sequences with specific meanings:
- **AR** - End of message
- **SK** - End of contact / Silent Key
- **KN** - Specific station only (go ahead)
- **BK** - Break / Back to you
- **CL** - Closing station
- **SOS** - Distress (sent as single unit)
- **AS** - Wait / Stand by
- **CT** - Start of transmission

#### **C. Q-Codes**
Standard abbreviations for common questions/statements:
- **QTH** - Location
- **QSL** - Acknowledgement / Confirmation card
- **QRM** - Man-made interference
- **QRN** - Static / Natural noise
- **QSB** - Fading signal
- **QSY** - Change frequency
- **QSO** - Contact / Conversation
- **QRL** - Are you busy? / Frequency in use?
- **QRS** - Send more slowly
- **QRZ** - Who is calling me?
- **QRP** - Low power operation
- **QRQ** - Send faster

#### **D. Common CW Abbreviations**
Frequently used shorthands:
- **73** - Best regards
- **88** - Love and kisses
- **CQ** - Calling any station
- **DE** - From (this is)
- **K** - Go ahead / Over
- **TNX / TKS** - Thanks
- **FB** - Fine business / Excellent
- **OM** - Old man (any male operator)
- **YL** - Young lady (female operator)
- **XYL** - Wife
- **PSE** - Please
- **HR** - Here
- **ES** - And
- **CUL** - See you later
- **AGN** - Again
- **WX** - Weather
- **ANT** - Antenna
- **RIG** - Radio equipment
- **PWR** - Power
- **RST** - Readability-Signal-Tone report
- **UR** - Your / You're
- **VY** - Very
- **HW** - How
- **CFM** - Confirm
- **TU** - Thank you

#### **E. Callsigns** (Generated)
Realistic amateur radio callsign formats:
- **US Format**: K/W/N/A + [0-9] + [A-Z]{1-3}
  - Examples: K6ABC, W1XYZ, N2MH, AA7BQ
- **International prefixes**:
  - G (UK): G3XYZ, M0ABC
  - VE (Canada): VE3XYZ, VA7ABC
  - JA (Japan): JA1XYZ
  - VK (Australia): VK3XYZ
  - DL (Germany): DL1ABC

#### **F. Equipment & Antennas**
Common ham radio terminology:
- **Antennas**: DIPOLE, YAGI, VERTICAL, BEAM, LOOP, QUAD, DELTA, INVERTED VEE
- **Equipment**: RIG, XCVR (transceiver), AMP (amplifier), TUNER, KEY, PADDLE, LINEAR
- **Bands**: 80M, 40M, 20M, 15M, 10M, 6M, 2M

#### **G. RST Signal Reports**
Readability (1-5), Signal Strength (1-9), Tone (1-9 for CW):
- 599 (perfect signal)
- 579 (excellent but slight QSB)
- 559 (good readable signal)
- 339 (readable, weak, good tone)

**Content Storage:**
- Hardcoded arrays in JavaScript (fully offline) ✅
- Organized by category for easy selection ✅
- Callsigns generated algorithmically (70 in pool, European focus with Czech/German/Polish/US mix) ✅

### 3. Phrase Selection Mode ✅ CONFIRMED

**Toggle: Shuffle ON/OFF**

- **Shuffle ON** (default): Random selection from category
- **Shuffle OFF**: Sequential order through category list
- Setting persists across sessions (localStorage)
- Global setting (applies to all categories)

**Implementation:**
- Simple toggle switch in UI
- Randomized deck approach: shuffle once, go through all items before reshuffling
- Sequential mode: loop back to start when reaching end of category

---

## Confirmed Design Decisions

### Learning Model ✅
**Goal:** General CW proficiency through passive listening
- Build pattern recognition at multiple speeds
- Ear training for common ham radio phrases and callsigns
- No performance tracking or testing (passive only)

### User Experience ✅
**Passive listening tool** - optimized for hands-free use:
- Simple "Next" button to advance to next phrase
- Auto-play option for continuous listening
- No keyboard input, no answer checking
- Mobile-friendly UI for phone use while walking

### Speed Settings ✅
**Fixed progression** (for MVP):
- 25 WPM → 25 WPM Farns(20) → 20 WPM → 20 WPM Farns(17) → TTS
- Future: Make speeds configurable in settings

### Audio Settings
Suggested for MVP:
- [x] Default tone: 600 Hz (standard CW tone)
- [ ] Optional: Frequency adjustment (400-800 Hz range)
- [ ] Optional: Volume control (use device volume for MVP)
- [x] Envelope shaping to avoid clicks on tone start/stop (5ms attack/release)

---

## Technical Considerations

### Offline-First Architecture
✅ Single HTML file or local file structure
✅ No external dependencies
✅ Works without internet connection
✅ Data stored in localStorage (if needed)

### Browser Compatibility
- Web Audio API (all modern browsers)
- Web Speech API (check browser support)
- Fallback for browsers without TTS?

---

## Honest Assessment

### 🟢 What Works Extremely Well

1. **Farnsworth stepping-stone approach is brilliant**
   - Using Farnsworth as intermediate speeds between 25→20 WPM is innovative
   - Prevents learning "slow Morse" while still providing graduated difficulty
   - I haven't seen this approach documented elsewhere - it's genuinely clever

2. **Passive listening design** fits the use case perfectly
   - Walking/commuting is ideal time for ear training
   - No distraction from typing or checking answers
   - Builds unconscious pattern recognition through repetition
   - Similar to language learning immersion techniques

3. **Fast-to-slow progression** makes pedagogical sense here
   - Hear target speed first (aspirational)
   - Progressively slower playback aids decoding
   - TTS at end confirms without breaking flow

4. **Category system** enables focused practice
   - Q-codes one day, callsigns another
   - Realistic on-air vocabulary
   - Maintains motivation through variety

5. **Offline-first** is essential for mobile use
   - No data usage while walking
   - No latency issues with audio
   - Complete privacy

### 🟡 Considerations

1. **TTS quality varies by browser/OS**
   - Mobile browsers may have better voices than desktop
   - Consider adding visual text display as backup
   - Some users might prefer just seeing the text vs hearing TTS

2. **Auto-play could be disruptive**
   - Might need adjustable pause between phrases (2-5 seconds?)
   - Start/stop button for auto-play mode
   - Some users may want thinking time between phrases

3. **Mobile battery usage**
   - Web Audio API is efficient, but worth monitoring
   - Screen-off playback might not work (browser limitation)
   - Consider PWA (Progressive Web App) for better mobile integration

### ✅ No Major Issues

The design is well thought-out for the specific use case. The passive listening approach eliminates most complexity concerns (no state management for quizzes, no performance tracking, etc.).

---

## MVP Feature Set

### Phase 1: Core Passive Listening (Initial Release) ✅ COMPLETE

**Essential Features:**
- [x] Fixed playback sequence:
  - 25 WPM full speed
  - 25 WPM Farnsworth (20 WPM effective)
  - 20 WPM full speed
  - 20 WPM Farnsworth (17 WPM effective)
  - Text-to-speech readback
- [x] Category selector with all categories:
  - Contest Phrases (5NN, CQ TEST, etc.) ✅ BONUS
  - Prosigns (AR, SK, KN, etc.)
  - Q-Codes (QTH, QSL, QRM, etc.)
  - CW Abbreviations (73, CQ, TNX, etc.)
  - Callsigns (generated - 70 international)
  - Equipment & Antennas
  - RST Signal Reports
- [x] Shuffle toggle (ON/OFF) - persists to localStorage
- [x] "Play" button (renamed from "Next Phrase")
- [x] "Stop" button to interrupt playback
- [x] Current phrase display (text appears during TTS)
- [x] Mobile-responsive UI with OK1TRL amber terminal design
- [x] 600 Hz tone generation with envelope shaping

**Nice-to-Have for MVP:**
- [x] Auto-play mode with 3-second pause between phrases ✅ IMPLEMENTED
- [x] Visual category descriptions in dropdown
- [x] Phrase counter/progress indicator (shuffle: remaining in deck, sequential: X of Y)

### Phase 2: Polish & Expansion

**Content Expansion:**
- [ ] All 6 content categories fully populated
- [ ] Equipment & Antennas category
- [ ] RST signal reports
- [ ] Longer conversational phrases

**User Experience:**
- [ ] Settings panel:
  - WPM speed adjustment (keep Farnsworth ratios)
  - Auto-play pause duration
  - Tone frequency (400-800 Hz)
- [ ] Dark mode toggle
- [ ] Keyboard shortcuts (Space = Next, P = Pause, etc.)

### Phase 3: Advanced Features (Future)

**Audio Enhancements:**
- [ ] Realistic CW filters/audio effects
- [ ] Background noise/QRM simulation (optional)
- [ ] Variable tone (simulate real stations)

**Progressive Web App:**
- [ ] Install as mobile app
- [ ] Offline manifest
- [ ] Background audio playback (if possible)

**Content Management:**
- [ ] Custom phrase lists (import/export JSON)
- [ ] Favorite phrases/categories
- [ ] Practice history (which categories used, not performance)

---

## Next Steps

1. ✅ Review and refine this PRD → **COMPLETE**
2. ✅ Define MVP scope → **CONFIRMED: Phase 1 features above**
3. ✅ Research CW content → **COMPLETE: 7 categories documented**
4. ✅ Implement Phase 1 MVP → **COMPLETE**
   - [x] Create data structures for all categories (including bonus contest phrases)
   - [x] Implement Farnsworth timing algorithm
   - [x] Build UI (mobile-first amber terminal design - OK1TRL theme)
   - [x] Add category selector with all 7 categories
   - [x] Implement shuffle toggle with localStorage
   - [x] Test audio playback sequence
   - [x] Add auto-play functionality
   - [x] Add progress indicator
5. **Next:** Test on mobile devices (primary use case)
6. **Optional:** Convert to PWA (see pwa-instructions.md)
7. **Future:** Gather feedback, iterate on Phase 2 features

---

## Technical Implementation Notes

### Farnsworth Timing Calculation

Standard timing (at character speed C):
- Dot = 1 unit
- Dash = 3 units
- Intra-character gap = 1 unit
- Character gap = 3 units
- Word gap = 7 units

Farnsworth timing (character speed C, effective speed E):
- Character elements: same as speed C
- Adjusted character gap = `(C/E × 3) - 3` units (extra spacing)
- Adjusted word gap = `(C/E × 7) - 7` units (extra spacing)

**Example:** 25 WPM character, 20 WPM effective:
- Character elements at 25 WPM timing
- Character gap = (25/20 × 3) - 3 = 0.75 extra units → 3.75 total
- Word gap = (25/20 × 7) - 7 = 1.75 extra units → 8.75 total

### Callsign Generation Algorithm

```javascript
function generateCallsign(region = 'US') {
  const formats = {
    US: {
      prefix: ['K', 'W', 'N', 'A'],
      number: '0-9',
      suffix: '1-3 letters'
    },
    // etc.
  };
  // Implementation in code
}
```

---

## Research Sources

- [CW Morse Code Reference Guide - W6AER](https://w6aer.com/cw-morse-code-reference-guide/)
- [Morse code abbreviations - Wikipedia](https://en.wikipedia.org/wiki/Morse_code_abbreviations)
- [Wave Talkers Reference: Top 100 CW Words](https://wavetalkers.com/resources/references/cw_100.php)
- [Amateur radio call signs - Wikipedia](https://en.wikipedia.org/wiki/Amateur_radio_call_signs)
- [Prosigns for Morse code - Wikipedia](https://en.wikipedia.org/wiki/Prosigns_for_Morse_code)
- [Ham Radio Call Signs & Prefixes - Electronics Notes](https://www.electronics-notes.com/articles/ham_radio/call-signs/amateur-radio-callsigns.php)

