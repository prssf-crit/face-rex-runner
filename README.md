# 🦖 Face-Rex Runner – Levels Edition

**Face-Rex Runner** is a browser-based, single-file game inspired by Chrome’s offline T-Rex.
In this version, you play **as yourself**: upload your face to replace the T-Rex, run through evolving levels, and dodge dynamically generated obstacles.
Everything runs **entirely client-side** — no frameworks, no servers, no network calls.

---

## 🎮 Features
- **Adaptive difficulty:** each new level increases one of three variables — *speed*, *obstacle size*, or *obstacle frequency* — never decreasing or repeating the same variable twice in a row.
- **Obstacle clusters:** sometimes 2–3 obstacles appear in tight formation for rhythmic challenge.
- **Physics-aware design:** all obstacle heights remain within the player’s jumpable limit.
- **Player control:** move **← / → (A / D)** to adjust position; **Space / ▲ / tap** to jump; **P** to pause; **R** to reset.
- **Offline-ready:** open `index.html` directly in any modern browser.
- **Dark-mode aware** and responsive across devices.

---

## 🧩 Technical Overview
| Component | Description |
|------------|--------------|
| **Stack** | Pure HTML5, CSS, vanilla JavaScript |
| **Rendering** | `<canvas>` 2D API |
| **Game loop** | `requestAnimationFrame` with bounded time-step |
| **Physics** | Gravity-based vertical motion, kinematically capped jump height |
| **Level logic** | Deterministic, incremental one-variable evolution |
| **Persistence** | `localStorage` stores best score |
| **Performance** | DPR capped at 1.5 for smooth motion on hi-DPI screens |

---

## ⚙️ Controls
| Action | Key / Gesture |
|:-------|:---------------|
| Start / Jump | **Space**, **▲**, or tap |
| Move left / right | **← / →** or **A / D** |
| Pause / Resume | **P** |
| Reset | **R** |
| Upload face | “Upload face” button in header |

---

## 🧠 Difficulty Model
At each level-up (every ~300 score points):
1. Exactly **one variable** increases:
   - **Speed:** world scrolls slightly faster.
   - **Size:** obstacle height range widens.
   - **Frequency:** obstacles (and clusters) appear more often, with tighter gaps.
2. Previously increased variable is excluded from the next roll, ensuring deterministic but varied progression.
3. Physical fairness maintained: no obstacle ever exceeds your jumpable reach (`v² / 2g × 0.88`).

---

## 📈 Cluster Generation
- **Chance:** starts around 20 %, grows up to ~55 % at higher levels.
- **Count:** 1–3 obstacles per cluster.
- **Inner gap:** 8–24 px, capped by an overall cluster span (~200 px).
- **Between-cluster gap:** dynamically adjusted per level to balance pacing.

---

## 🏁 Game Stats Displayed
- **Score:** increases with distance and speed.
- **Best:** stored locally between sessions.
- **Level:** current difficulty stage.
- **Speed:** current multiplier relative to starting pace.

---

## 🧱 Project Structure
```
index.html   # Entire game (HTML, CSS, and JS combined)
README.md    # Documentation (this file)
```

That’s it — drop `index.html` anywhere, and it runs.

---

## 🚀 Running Locally
1. Download or clone the repository.
2. Open `index.html` in any modern browser (Chrome, Edge, Safari, Firefox).
3. Upload an image of yourself if desired.
4. Play — no build tools, servers, or dependencies required.

---

## 🌐 Deploy Online
### GitHub Pages
1. Push the files to a new repository.
2. In **Settings ▸ Pages**, set branch = `main`, folder = `/ (root)`.
3. Wait a few seconds — your game appears at
   `https://<username>.github.io/<repo>/`.

### Netlify or Vercel
- Drag-and-drop the folder → instant deployment with HTTPS.

---

## 🔒 Privacy
All logic and data live in your browser tab.
Your uploaded image never leaves your device and is not transmitted or stored remotely.

---

## 🧑‍💻 Customisation Tips
- Tune **game feel** via constants near the top of the script:
  ```js
  const G = 2200;   // gravity
  const JUMP_VY = -780;  // jump velocity
  const INITIAL_BASE_SPEED = 240; // starting world speed
  ```
- Adjust **cluster behaviour**:
  ```js
  let clusterChance = 0.22;
  let clusterGapMin = 12;
  let clusterGapMax = 24;
  ```
- All variables are documented inline with comments for easy modification.

---

## 🪙 License
**MIT License** — free for personal, educational, and commercial use with attribution.

> Based on *Face-Rex Runner – Levels Edition*  

---

## 🏗️ Future Ideas
- Inertia for smoother left/right motion.
- Power-ups (score multipliers, shield).
- “Level up” visual banner.
- Optional background music toggle.
