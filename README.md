# 👑 Dixit Ludo — Offline React Edition (for AWS S3 & Mobile)

**Dixit Ludo** has been rebuilt as an offline-ready **React 18** application tailored for AWS S3 static hosting and **Mobile Phone Browsers (iOS Safari / Android Chrome)**. All AI logic has been stripped out to keep gameplay simple and focused on **2, 3, or 4 Human Players**.

---

## 📱 Minimal Centered Phone Layout & Full Screen Mode
- **Full Screen Mode (`⛶`)**:
  - A new **Full Screen Toggle (`⛶` / `🗗`)** button is available in the top-right header at all times, as well as a dedicated **`⛶ Play in Full Screen`** button inside the initial Setup Modal.
  - Tapping this button requests browser Fullscreen (`requestFullscreen`), immersing you in an edge-to-edge gaming experience without address bars or browser chrome.
- **Dead-Center Phone Screen Alignment**: On mobile phone screens (`@media (max-width: 600px)`), the entire game workspace (`.app-main`) uses `justify-content: center` and `min-height: calc(100vh - 54px)`, positioning **the Ludo board (`.board-wrapper`) 100% perfectly in the center of the phone screen**!
- **Uniform Perfectly Square Grid (`repeat(15, 1fr)`)**:
  - The 15×15 CSS Grid uses equal columns and rows (`repeat(15, 1fr)`) so that every single path square on the board is a **100% identical, mathematically perfect square**.
- **Massive Invisible Touch Targets for Mobile (Accessibility)**:
  - While tokens look beautifully proportioned on screen (`22px` on phones), tapping something that small is frustrating.
  - We added a massive invisible `::after` pseudo-element expanding the physical tap area of all glowing (valid) tokens to **250% of their visual size (`~55px`)**! This greatly exceeds Apple's 44px recommendation, making the game incredibly easy and forgiving to play on small mobile phones!
- **Floating External Dice Boxes**:
  - The dice rolling boxes have been completely **removed from inside the colored base yards**, giving the tokens plenty of spacious, uncluttered room in their home base!
  - Instead, the dice boxes now **float completely outside the Ludo board** in the 4 corners of your screen!
  - **Red** rolls on the Top-Left, **Green** on the Top-Right, **Yellow** on the Bottom-Right, and **Blue** on the Bottom-Left.
  - Just tap the floating, glowing dice outside your corner of the board to roll!

---

## ⚡ Instant Dice Rolling & Ultra-Snappy Turn Shifting
- **Instant Dice Display (`75ms`)**: When you tap the pulsing dice, the rolled number appears **immediately in 75ms** (reduced from 380ms!), giving instant tactile feedback!
- **Zero-Lag Turn Shifting (`60ms - 220ms`)**:
  - When a token finishes moving or enters a base/goal, the turn immediately shifts to the next player in **60ms** (reduced from 300ms!).
  - If you roll and have **zero valid moves**, the turn automatically skips in **220ms** (reduced from 850ms!).
  - If you roll and have **only 1 valid move**, that token automatically starts moving in **120ms** (reduced from 450ms!).
  - Hop-by-hop step animations run at **85ms per square** for a crisp, high-tempo game flow.

---

## 🎮 Player Selection (Stacked Mobile Layout) & Blue vs. Green 2-Player Default
- **Stacked Mobile Player Selection**: On mobile phone viewports, the Player Selection cards are cleanly stacked vertically from top to bottom:
  - **Top Card**: **2 Players** (`👥 Blue & Green`)
  - **Middle Card**: **3 Players** (`👤👤👤 Red, Green, Yellow`)
  - **Bottom Card**: **4 Players** (`👑👑 All 4 Colors`)
- **2-Player Default**: When launching the game or starting a new match, **2 Players** is selected by default for quick 1v1 gameplay.
- **Diagonally Opposite Sides (`Blue vs. Green`)**: Selecting **2 Players** always enables **Blue vs. Green** (Bottom-Left vs. Top-Right diagonal corners). The inactive Red and Yellow base yards automatically dim out (`grayscale + 22% opacity`) so it is visually unmistakable which opposite sides are in play!
- **New Game Safety Confirmation**: Whenever any game is currently on the screen (`!isGameOver && !showSetupModal`), tapping the **`🎮 New Game`** button in the top right header will **always** trigger a Confirmation Modal (`⚠️ Game in Progress: An existing game is currently underway. Do you want to start a new game?`), preventing accidental resets of any ongoing game!

---

## 🎲 Outer Corner Dice Slot & Realistic CSS Die Faces
- **Permanent Outer Corner Box**: Each active player's colored base yard now has a sleek, glassmorphic box (`.outer-dice-box`) located at its outermost corner (Top-Left of Red, Top-Right of Green, Bottom-Right of Yellow, Bottom-Left of Blue).
- **Dynamic Turn Die Appearance**:
  - When it is **NOT** your turn, your corner box is empty (`.dice-empty-slot`).
  - When it **IS** your turn, a glowing **3D Dice (`🎲`)** appears inside your outer corner box and gently pulses (`diceCornerPulse`).
  - Simply tap the dice inside your outer corner box to roll!
- **Realistic 3×3 CSS Die Face (Pure Dots / Pips)**:
  - After rolling, instead of displaying numbers or text symbols, the dice transforms into a **pristine 3D CSS Casino Die (`<DiceFace />`)** with indented navy-black dots (pips) arranged in a 3×3 grid to match the exact number rolled (`1` to `6`)!
  - No redundant numbers are written inside the box — just clean, elegant casino die faces.
  - Rolling a **6** triggers a special golden die face with ruby-red pips and an electric cyan aura (`dice-six-glow`).

---

## 🎯 Mathematically Perfect Token & Base Alignment
- **Centered Base Yard Circles**: The 4 dashed circles (`.yard-circle`) inside every colored base are calibrated to match the 15×15 CSS Grid coordinates (`[2, 2]`, `[2, 3]`, `[3, 2]`, `[3, 3]`, etc.). Tokens **1, 2, 3, 4** sit **100% dead-center** inside their respective circles when waiting in the base yard!
- **Dynamic Stack Separation**: When multiple tokens share a single square on the track, they automatically offset in a clean cluster so every token is clearly visible.

---

## ✨ Zero-Overlap CSS Grid Layout

- **Explicit 15x15 CSS Grid System**: Every square on the board is explicitly locked to its exact row and column coordinate (`gridRow`, `gridColumn`).
- **Spanning Base Yards & Center Goal**: The 4 colored Yard Bases and the Center Crown Goal use CSS Grid spanning (`grid-area: 1 / 1 / 7 / 7`, etc.) as direct children of the board grid. This guarantees **100% pixel-perfect alignment with ZERO overlapping boxes** across mobile phones, tablets, and desktop screens.

---

## 🔊 Rich Web Audio Synthesizer & Sound Effects

All sounds are synthesized natively using the **HTML5 Web Audio API** with zero external audio files needed:
- **AudioContext Unlocking Fix**: Sounds unlock automatically on your first tap/click in any browser (Safari, Chrome, iOS, Android).
- **Dice Roller (`audio.playDiceRoll`)**: 7 rapid wooden tumbler taps with realistic varying pitches.
- **Hop-by-Hop Step Sound (`audio.playStep`)**: Crisp wooden "tock" step sounds play on **every single square** as your token hops along the path!
- **Star Square Chime (`audio.playSafeStar`)**: Sparkling 5-note magical glittering arpeggio chime when any token lands on a Star or Safe Square!
- **Base Exit (`audio.playBaseExit`)**: Cheerful ascending double-beep when a token leaves its base yard.
- **Capture (`audio.playCapture`)**: Dramatic sawtooth laser zap when you capture an opponent's token.
- **Home Goal (`audio.playGoal`)**: Harmonious royal 4-note chord when entering the goal.
- **Victory Fanfare (`audio.playVictory`)**: 6-note trumpet celebration chord progression when a player wins!
- **UI Button Click (`audio.playButton`)**: Responsive tactile sound on every menu selection.

---

## 🚀 How to Deploy to AWS S3 / GitHub Pages for Mobile Play

- **GitHub Pages**: Deployed live on **https://puneetdixit.github.io/ludo/**
- **AWS S3**: Simply upload `index.html`, `style.css`, and `assets/` to any static hosting S3 bucket!

*Note: You can also double-click `index.html` in Finder on your Mac to test it instantly without any local web server.*

---

## 🎲 How to Play

1. **Select Players**: When the app loads, **2 Players** (Blue & Green Opposite) is selected by default. Choose **2 Players**, **3 Players**, or **4 Players**, then tap **🚀 Start Offline Game**.
2. **Roll the Dice**: Look at your outermost corner box! When it's your turn, a glowing dice (`🎲`) will appear inside your corner box—tap it to roll!
3. **Move a Token**: If more than 1 legal move is available, tokens will pulse with a glowing halo—tap any glowing token to watch it hop! (If only 1 token can move, it will move automatically!)
4. **Win**: Guide all 4 of your tokens around the board and into the center Goal!