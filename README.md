# Tic Tac Toe Lux (Cyber-Luxury Android Native App)

A production-grade, cyber-luxury native Android Tic-Tac-Toe application built with **Kotlin**, **Jetpack Compose**, **Material Design 3**, **Room Database**, and **Firebase Firestore with Google Authentication**.

---

## 💎 1. Visual & Audio Identity
- **Cyber-Luxury Dark Gaming Aesthetic**:
  - Deep Obsidian & Midnight Blue canvas (`#070B14`, `#080C14`, `#111827`).
  - Neon Cyan (`#00F0FF`) and Laser Magenta (`#FF007F`) laser markers with glowing bloom.
  - Imperial Gold (`#FFD700`) luxury highlights for trophies, leader crowns, and 6-digit room codes.
  - Layered radial backdrop auras and cyber grid lines.
- **Typography**: Google Font **Outfit** bundled locally in `res/font/` with weights Normal, SemiBold, and Black.
- **Micro-interactions**:
  - Spring-animated markers (`dampingRatio = 0.52f`, `StiffnessMediumLow`).
  - Pulsing turn indicator rings on active player cards.
  - Dynamic neon line strike animation connecting winning cells.
  - Full-screen particle/confetti victory celebration.
  - Low-latency PCM wave audio clips via Android `SoundPool` (`neon_place_x.wav`, `neon_place_o.wav`, `neon_win.wav`, `neon_draw.wav`, `neon_tap.wav`).
  - Tactile haptic feedback (`VibrationEffect` tick for moves, heavy burst pattern for wins, buzz for draws).

---

## 🎮 2. Game Setup Menu (Start Screen)
- **Step 1: Choose Game Type**:
  - `Play vs Bot (AI)` [SOLO] - Single player against algorithmic AI.
  - `2 Players (Same Device)` [OFFLINE LOCAL] - Shared device pass & play.
  - `Play Online Room` [P2P ONLINE] - Real-time online match with a friend using a 6-digit room code.
- **Step 1.5: Bot Difficulty Selection** (Visible when "vs Bot" is selected):
  - **Novice**: Casual fun random moves.
  - **Tactician**: Heuristic threat blocker and win taker.
  - **Grandmaster**: Unbeatable Minimax algorithm with depth pruning and position heuristics.
- **Step 2: Choose Board Boxes / Dimensions**:
  - **Classic 3 × 3** (9 Boxes • 3 in a row to win)
  - **Tactical 4 × 4** (16 Boxes • 4 in a row to win)
  - **Master 5 × 5** (25 Boxes • 4 in a row to win)
- Glowing **"START MATCH NOW"** action button.
- Hardware back handler and in-game exit button to return to setup at any time.

---

## 🏆 3. Clean In-Game Scoreboard & Canvas
- **Top Header**: Brand logo, Sound toggle, Haptics toggle, Share online room, Leaderboard trophy, Statistics chart, Settings gear, Exit back.
- **Live Session Scoreboard**:
  - "LOCAL 2-PLAYER SESSION • TOTAL ROUNDS: N" session banner.
  - VIP Cards side-by-side with player names, pieces, pulsing active turn ring, and large score with explicit `WINS` subtitle.
  - Center Ties badge tracking drawn games.
  - Imperial Gold crown badge on whichever player leads in score.
- **Bottom Controls**:
  - Single-move **Undo** (available in solo and local play).
  - **Play Again / Restart** (automatically alternates starting player).

---

## 🗄️ 4. Local Persistence & Room Database
- `MatchRecordEntity`: Stores `matchId`, `gameMode`, `boardSize`, `difficulty`, `winner`, `moveCount`, and `timestamp`.
- `StreakStatsEntity`: Tracks `totalGamesPlayed`, `xWins`, `oWins`, `draws`, `currentStreak`, `maxStreak`, and `winRate`.
- Clean Stats & Settings bottom sheet with filter tabs for **Global**, **vs AI**, and **Pass & Play**.

---

## 🌐 5. Real-Time Online Multiplayer (Firebase Firestore)
- Firestore schema `/rooms/{roomCode}`.
- Host creates 6-digit code with lobby card, Copy Code, and Android System Share actions.
- Guest enters 6-digit code to join immediately.
- Reactive `Flow` listening to Firestore snapshots synchronizing moves, turn alternation, audio, haptics, and winning line animations on both devices.
- `firestore.rules` zero-trust security configuration included.

---

## 🥇 6. Global Leaderboard & Authentication
- Google Sign-In using Android Jetpack `CredentialManager` (`GetGoogleIdOption`).
- Secure Firestore collection `/leaderboard/{userId}`.
- Modal bottom sheet displaying ranked champions with Gold (#1), Silver (#2), and Bronze (#3) trophies, win percentages, streaks, and one-tap manual sync button.

