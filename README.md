# 👑 Dixit Ludo — Offline React Edition (for AWS S3 & Mobile)

**Dixit Ludo** has been rebuilt as an offline-ready **React 18** application tailored for AWS S3 static hosting and **Mobile Phone Browsers (iOS Safari / Android Chrome)**. All AI logic has been stripped out to keep gameplay simple and focused on **2, 3, or 4 Human Players**.

---

## 📱 Minimal Centered Phone Layout & Pure Corner Dice Rolling
- **Dead-Center Phone Screen Alignment**: On mobile phone screens (`@media (max-width: 600px)`), the entire game workspace (`.app-main`) uses `justify-content: center` and `min-height: calc(100vh - 54px)`, positioning **the Ludo board (`.board-wrapper`) 100% perfectly in the center of the phone screen**!
- **Maximized Board Size & Pure Base Yards (No Color Text Clutter)**:
  - By removing the bottom info/controller box entirely, the board size expands to **min(96vw, 82vh, 560px)**, giving you the largest possible game board on mobile phones without scrolling.
  - The color name text labels ("RED", "GREEN", "YELLOW", "BLUE") inside each colored base yard have been **removed**, leaving clean, vibrant casino-style base yards with only the token circles and the outer corner dice box!
- **Pure Corner-Dice Rolling (No Bottom UI Box)**:
  - The bottom controller box has been **completely removed** for a sleek, minimal, distraction-free interface.
  - All gameplay happens directly on the board:
    - Tap the pulsing dice inside the active player's **Outer Corner Dice Box** to roll.
    - Tap any glowing token on the board to move!

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

## ⚡ Intelligent Auto-Move
- **Automatic Move on Single Option**: When you roll the dice and **only 1 legal move is available**, the game automatically selects and animates that token after a brief `450ms` delay! You never have to manually tap a token when there is zero ambiguity.
- **Automatic Turn Skip**: When you roll and have **zero valid moves**, the turn automatically passes to the next player after `850ms`.

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

## 🚀 How to Deploy to AWS S3 for Mobile Browser Play

1. In your AWS S3 bucket, upload the following files/folders:
   - `index.html`
   - `style.css`
   - `assets/` (containing `logo.jpg`)
2. In your S3 bucket settings, enable **Static website hosting** and set the index document to `index.html`.
3. Open the S3 website URL on your phone browser (Safari/Chrome). Once loaded, you can play offline!

*Note: You can also double-click `index.html` in Finder on your Mac to test it instantly without any local web server.*

---

## 🎲 How to Play

1. **Select Players**: When the app loads, **2 Players** (Blue & Green Opposite) is selected by default. Choose **2 Players**, **3 Players**, or **4 Players**, then tap **🚀 Start Offline Game**.
2. **Roll the Dice**: Look at your outermost corner box! When it's your turn, a glowing dice (`🎲`) will appear inside your corner box—tap it to roll!
3. **Move a Token**: If more than 1 legal move is available, tokens will pulse with a glowing halo—tap any glowing token to watch it hop! (If only 1 token can move, it will move automatically!)
4. **Win**: Guide all 4 of your tokens around the board and into the center Goal!