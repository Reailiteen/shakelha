# Shakelha (شكلها)
## Game Design Document (GDD)

---

## 1. Game Overview

**Shakelha** is a competitive Arabic word board game inspired by Scrabble. Two players compete on a shared board by forming valid Arabic words using letter tiles drawn from a common pool. Players score points based on letter values, word length, and board multipliers. The player with the highest score at the end of the match wins.

- Genre: Word / Board Game  
- Language: Arabic (Modern Standard Arabic)  
- Platform: iOS (launch), Android (future)  
- Modes: PvP, PvC  
- Tone: Competitive, challenging, light, fun  

---

## 2. Core Inspiration & Differentiation

Shakelha is inspired by Scrabble with the following key differences:

- Board size reduced to **11×11**
- Letter rack size reduced to **6 letters**
- Faster, mobile-friendly matches
- Arabic-specific language rules and dictionary
- Digital-first UI and match flow

---

## 3. Board Design

- Grid: **11×11**
- Center tile: **Double Word (DW)**
- Full rotational symmetry
- All multipliers are **consumed on first use**

### 3.1 Multiplier Types
- DL – Double Letter
- TL – Triple Letter
- DW – Double Word
- TW – Triple Word

### 3.2 Multiplier Distribution
| Type | Count |
|----|----|
| DL | 16 |
| TL | 8 |
| DW | 8 |
| TW | 4 |

### 3.3 Multiplier Layout (Coordinates)
- TW: (1,1), (1,11), (11,1), (11,11)
- DW: (6,6), (3,3), (3,9), (9,3), (9,9), (6,2), (2,6), (6,10), (10,6)
- TL: (2,4), (2,8), (4,2), (4,10), (8,2), (8,10), (10,4), (10,8)
- DL: (1,6), (6,1), (6,11), (11,6),
      (3,5), (3,7),
      (5,3), (5,9),
      (7,3), (7,9),
      (9,5), (9,7),
      (5,5), (5,7),
      (7,5), (7,7)

### 3.4 First Move Rules
- First word must pass through center tile (6,6)
- Triple Word tiles are inactive on the first move
- Maximum word multiplier on first move: **2×**

---

## 4. Letter System

### 4.1 Letter Pool
- Total tiles: **~95**
- No wildcard / blank tiles at launch

### 4.2 Distribution & Values
Arabic letters are divided into frequency tiers:
- Core letters: high frequency, low points
- Common modifiers: medium frequency, medium points
- Rare letters: low frequency, high points
- Special letters: very low frequency, situational value

Letter distribution and values are fixed and shared between all players and AI.

### 4.3 Player Rack
- Rack size: **6 letters**
- Rack refills to 6 letters after each turn if tiles remain
- Optional one-time shuffle per match (future toggle)

---

## 5. Arabic Language Rules

- No diacritics (tashkeel)
- Strict letter identity:
  - ة ≠ ه
  - ى ≠ ي
- Hamza variants (أ / إ / آ) are separate tiles but normalized internally
- No proper nouns (people, places, brands)
- Modern Standard Arabic only
- No dialect or slang
- Prefixes allowed only if explicitly approved in dictionary
- Dictionary-based validation only (no grammar logic)

---

## 6. Dictionary Scope

- Curated, game-first Arabic dictionary
- Modern Standard Arabic only
- Launch size: **15,000–25,000 words**
- Explicit inclusion required for:
  - Plurals
  - Feminine forms
  - Verb tenses
- Dual forms (ـان / ـين) disallowed at launch
- Server-side updates only
- Dictionary normalization:
  - Remove diacritics
  - Normalize hamza forms
  - Preserve ة and ى distinctions

---

## 7. Turn Structure

1. Player forms a word using rack letters
2. Placement is validated visually
3. Player submits the word
4. Word is validated against dictionary
5. Score is calculated and displayed
6. Letters are removed and rack refilled
7. Turn passes to opponent

Players may manually pass.
Two consecutive passes by both players end the match.

---

## 8. Match Formats & Timing System

### 8.1 Match Types
- PvP (Player vs Player)
- PvC (Player vs Computer)

### 8.2 Turn-Based Timing Modes
Players choose a timing mode before match start:

| Mode | Time per Turn |
|----|----|
| Blitz | 1 minute |
| Standard | 2 minutes |
| Classic | 3 minutes |

PvC Easy may disable timers.
PvC Medium and Hard use selected timing mode.

---

### 8.3 Timeout Handling & Bot Intervention

If a player fails to play before the timer expires:

1. A **bot immediately plays a move** on behalf of the player
2. The bot selects:
   - A valid move
   - The **least profitable legal word** available
   - No premium tile optimization
   - No rare-letter optimization
3. The move is clearly marked as **“Auto-played”**

### 8.4 Forfeit & Bot Takeover Rules

- If a player times out **twice consecutively**:
  - The player **immediately forfeits**
  - A bot permanently replaces the player
  - Match continues as PvC for the remaining player
- This applies to PvP only
- Prevents stalling, griefing, and rage quitting

---

## 9. Scoring Rules

- Base score: sum of letter values
- Word length bonus applied
- Letter multipliers applied first
- Word multipliers applied second
- Maximum word multiplier: **3×**
- Endgame penalties may apply for unused letters

---

## 10. AI Design (PvC & Auto-Play)

### 10.1 AI Difficulty Levels
- Easy: short words, frequent mistakes
- Medium: balanced, human-like play
- Hard: strategic, limited lookahead, fair

### 10.2 AI Constraints
- Uses same dictionary as players
- Cannot play obscure or ultra-rare words
- Cannot exceed rack size
- Cannot see future tiles or player rack

### 10.3 Auto-Play Bot Rules
- Used only on player timeout
- Always selects the **lowest scoring valid move**
- Never uses TW unless forced
- Never blocks opponent strategically

---

## 11. UI Flow & Interaction Rules

### 11.1 Core Screens
- Home
- Mode Selection
- Timing Mode Selection
- Match Screen
- End Match Screen

### 11.2 Match Screen Layout
- Board centered
- Player rack at bottom
- Timer visible
- Scores visible
- Clear turn indicator

### 11.3 Interaction Rules
- Tap or drag letters to board
- Drag back to rack to undo
- Invalid placements highlighted in red
- Valid placements highlighted in green
- Submit enabled only when placement is valid

### 11.4 Feedback Rules
- Successful word:
  - Tile snap animation
  - Score breakdown shown
- Invalid word:
  - Board shake
  - Explicit error message

---

## 12. End Conditions

The match ends when:
- Letter pool is empty and a player empties their rack
- Both players pass consecutively
- A player forfeits due to timeout rules

Winner is the player with the highest score.

---

## 13. Explicitly Out of Scope (Launch)

- Power-ups
- Wildcards
- Cosmetic monetization
- Blitz variants beyond timing modes
- Ranked seasons

These may be added post-launch.

---