# 🎯 Grid Survivor

**Grid Survivor** is a strategic survival game based on a 7x7 grid. Select green cells and avoid red ones to survive as long as possible! Collect special bonuses, dodge evil traps, and climb the leaderboard to become the ultimate Grid Survivor.

🎮 **[Play Now!](https://max64180.github.io/grid-survivor/grid-survivor.html)**

![Grid Survivor](https://img.shields.io/badge/Grid-Survivor-blueviolet?style=for-the-badge&logo=gamepad)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)

---

## 📖 Table of Contents

- [Features](#-features)
- [How to Play](#-how-to-play)
- [Bonus System](#-bonus-system)
- [Malus & Traps](#-malus--traps)
- [Leaderboard](#-leaderboard)
- [Technologies](#-technologies)
- [Installation](#-installation)
- [Firebase Setup](#-firebase-setup)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### 🎮 **Engaging Gameplay**
- **7x7 Grid** with 49 cells to survive
- **8-second timer** per turn - red perimeter shows remaining time
- **3 lives** - each red cell costs one life
- **Dynamic scoring system** with streak bonuses and multipliers
- **Moving red block** that travels across the grid - avoid it!

### 🎁 **Advanced Bonus System**
- **7 regular bonuses**: Shield, Triple, Sniper, Vision, Magnet, Lucky, Extra Life
- **4 point bonuses** (one random per game): x2 Points, +1000, +5000, +10000
- **10 total bonuses** per game
- **Burned bonuses** - Sniper and Triple can burn hidden bonuses (shown crossed out)

### 😈 **Malus & Traps**
- **Bad Luck Malus** (😈) - doubles red cells next turn
- **Cursed Cards** (🎴) - lose 1, 2, or 3 random bonuses from the grid
- **Only one malus per game** (or none - 30% chance)

### 🏆 **Leaderboard System**
- **Local leaderboard** - saved in localStorage
- **Online leaderboard** - Firebase integration (optional)
- **Custom profiles** - choose emoji and name
- **Victory trophy** 🏆 - special symbol for completing all 49 cells

### 🎓 **Interactive Tutorial**
- **8 guided steps** - learn basic mechanics
- **First-time only** - automatically shown on first access
- **Skippable** - skip at any time
- **Animated hand** 👇 - invites you to start the game

### 🎨 **Modern Design**
- **Responsive UI** - works on desktop, tablet, and mobile
- **Smooth animations** - particles, bounce, slide-in, confetti
- **Sound effects** - 10+ synthesized sounds for game events
- **Semi-transparent windows** - see the grid behind popups

---

## 🕹️ How to Play

### 📋 **Objective**
Survive as long as possible by selecting green cells and avoiding red ones. Complete all 49 cells for total victory!

### 🎯 **Basic Rules**

1. **Start Game** 👇 - Click "New Game" to begin
2. **Bonus Preview** - Memorize where the 10 bonuses are hidden (2 seconds)
3. **Select Cell** - You have 8 seconds to choose a cell
4. **Revelation** - Some cells become red (danger!)
5. **Lives** - If you select a red one, lose 1 life (max 3)
6. **Bonuses** - Collect hidden bonuses to help you
7. **Game Over** - Lose if you run out of lives or time expires
8. **Victory** 🏆 - Complete all 49 cells to win!

### ⚙️ **Advanced Mechanics**

- **Moving Red Block** 🟥 - Moves across the grid following a path. Can hit you!
- **Dynamic Difficulty** - Number of red cells decreases as you progress (from 15 to 1)
- **Streak Combo** - Consecutive correct cells multiply points (`1.5^streak`, max x10)
- **Double Points** - Bonus doubles points for 3 turns

---

## 🎁 Bonus System

### 🛡️ **Defensive Bonuses**
| Icon | Name | Effect |
|------|------|--------|
| 🛡️ | **SHIELD** | Saves you from the next red hit |
| ❤️ | **EXTRA LIFE** | Gain an extra life (spawn: 50%/20%/5% for 1/2/3 lives) |

### 💣 **Offensive Bonuses**
| Icon | Name | Effect |
|------|------|--------|
| 💣 | **TRIPLE** | Eliminates 3 safe cells from the grid |
| 🎯 | **SNIPER** | Eliminates 1 guaranteed red cell |

⚠️ **Warning**: If Sniper or Triple eliminates a cell with a bonus underneath, the bonus is **burned** and appears crossed out (blue) in the bar!

### 👁️ **Information Bonuses**
| Icon | Name | Effect |
|------|------|--------|
| 👁️ | **VISION** | Reveals all safe cells for 5 seconds |
| 🧲 | **MAGNET** | Reveals all remaining bonuses for 3 seconds |

### 🍀 **Luck Bonus**
| Icon | Name | Effect |
|------|------|--------|
| 🎲 | **LUCKY** | Halves red cells next turn |

### 💰 **Point Bonuses** (1 random per game)
| Icon | Name | Effect |
|------|------|--------|
| 💰 | **x2 POINTS** | Double points for 3 turns |
| 💵 | **+1000** | +1000 immediate points |
| 💸 | **+5000** | +5000 immediate points |
| 💎 | **+10000** | +10000 immediate points |

---

## 😈 Malus & Traps

### 🎲 **Malus Probability** (per game)
- **30%** - Bad Luck Malus 😈 (slot 10/10)
- **30%** - Card Malus 🎴 (slot 9/10)
- **40%** - No malus

**⚠️ Only ONE malus per game** - never both!

### 😈 **Bad Luck Malus**
- **Effect**: Doubles red cells next turn
- **Popup**: Evil monster laughing + calculation of remaining safe cells
- **Sound**: Evil laugh with 3 distorted notes
- **Smart calculation**: Shows how many TRULY safe cells will remain after doubling

**Example**: 
- Available cells: 49
- Normal reds: 15
- Reds after malus: 30
- **Safe cells: 19** ✅ (not 49!)

### 🎴 **Cursed Cards**
- **Effect**: Choose 1 card among 3 - lose 1, 2, or 3 bonuses!
- **Mechanic**: Animated flip with colors (green=1, orange=2, red=3)
- **Removal**: First removes bonuses from grid, then from collected ones
- **Visual**: Removed bonuses appear crossed out in blue/purple in the bar

---

## 🏆 Leaderboard

### 📊 **Scoring System**
```
Base Points = 10 per cell
Streak Multiplier = 1.5^streak (max 10)
x2 Points Bonus = doubles for 3 turns

Example:
Cell with streak 5 = 10 × (1.5^5) = 10 × 7.59 = 76 points
With x2 bonus = 152 points!
```

### 🥇 **Leaderboard Features**
- **Top 10** - Only the best scores
- **Custom Profile** - Emoji + Name
- **"YOU" Badge** - Highlights your latest score (10 seconds)
- **Medals** - 🥇 🥈 🥉 for top 3
- **Victory Trophy** 🏆 - Special symbol for completing 49/49 cells
- **Dual Save** - Local (localStorage) + Online (Firebase)

---

## 🛠️ Technologies

### **Tech Stack**
```
Frontend:
├── HTML5
├── CSS3 (Grid, Flexbox, Animations, Blur Effects)
└── Vanilla JavaScript (ES6+)

Backend/Database:
├── Firebase Realtime Database (optional)
└── LocalStorage (always active fallback)

Audio:
└── Web Audio API (synthesized sounds)

Features:
├── Responsive Design
├── Touch Support
└── Zero Dependencies (no npm/webpack)
```

### **Performance**
- **Single HTML File** - everything in one file (<200KB)
- **No Build Step** - open and play
- **Fast Load** - <1 second
- **Offline Ready** - works without internet

---

## 📦 Installation

### **Method 1: Direct Download**
```bash
# 1. Download the file
curl -o grid-survivor.html https://raw.githubusercontent.com/max64180/grid-survivor/main/grid-survivor.html

# 2. Open in browser
open grid-survivor.html
```

### **Method 2: Git Clone**
```bash
# 1. Clone repository
git clone https://github.com/max64180/grid-survivor.git

# 2. Enter directory
cd grid-survivor

# 3. Open in browser
open grid-survivor.html
```

### **Method 3: Live Server (for development)**
```bash
# Using Python
python3 -m http.server 8000

# Using Node.js
npx http-server

# Then open: http://localhost:8000
```

---

## 🔥 Firebase Setup (Optional)

Firebase enables **shared online leaderboard**. The game works perfectly without it!

### **1. Create Firebase Project**
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create new project → Name: "Grid Survivor"
3. Analytics: No (optional)
4. Create project

### **2. Enable Realtime Database**
1. Build → Realtime Database → Create database
2. Location: **europe-west1** (for GDPR compliance) or your preferred region
3. Security Rules: **Test Mode** (temporary)

### **3. Configure Secure Rules**
```json
{
  "rules": {
    "leaderboard": {
      ".read": true,
      ".write": true,
      "$entry": {
        ".validate": "newData.hasChildren(['name', 'emoji', 'score', 'cells', 'streak', 'timestamp']) && newData.child('score').isNumber() && newData.child('name').isString()"
      }
    }
  }
}
```

### **4. Get Credentials**
1. Project Settings ⚙️ → General
2. Your apps → Web app (</>) → Register app
3. Copy the `firebaseConfig` object

### **5. Update HTML File**
Open `grid-survivor.html` and find (around line 1410):

```javascript
// ═══════════════════════════════════════════════════════════════════════════
// FIREBASE CONFIGURATION
// ═══════════════════════════════════════════════════════════════════════════
const firebaseConfig = {
    apiKey: "YOUR_API_KEY_HERE",
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.europe-west1.firebasedatabase.app",
    projectId: "your-project",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123def456"
};
```

Replace with your credentials!

### **6. Deploy**
```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize
firebase init hosting
# - Use existing project
# - Public directory: . (dot)
# - Single-page app: No

# Deploy
firebase deploy
```

**🎉 Done!** Online leaderboard is now active at: `https://your-project.web.app`

---

## 🤝 Contributing

Contributions welcome! Follow these steps:

### **1. Fork & Clone**
```bash
git clone https://github.com/max64180/grid-survivor.git
cd grid-survivor
git checkout -b feature/amazing-feature
```

### **2. Develop**
- Test on Chrome, Firefox, Safari
- Keep code commented
- Respect existing style

### **3. Commit & Push**
```bash
git add .
git commit -m "✨ Add: amazing feature"
git push origin feature/amazing-feature
```

### **4. Pull Request**
Open PR on GitHub with detailed description!

### **🐛 Report Bug**
[Open Issue](https://github.com/max64180/grid-survivor/issues) with:
- Bug description
- Steps to reproduce
- Screenshot/video
- Browser + OS

---

## 📝 Roadmap

### **v1.0 - Current** ✅
- [x] Core gameplay (7x7, timer, lives)
- [x] 7 bonuses + 4 point bonuses
- [x] 2 malus types (Bad Luck, Cards)
- [x] Local + Firebase leaderboard
- [x] Interactive tutorial
- [x] Synthesized audio
- [x] Victory with confetti
- [x] Completion trophy

### **v1.1 - Next** 🔜
- [ ] Zen mode (no timer)
- [ ] Hardcore mode (1 life only)
- [ ] Achievement system
- [ ] Daily challenges

### **v1.2 - Planned** 📅
- [ ] Turn-based multiplayer
- [ ] Custom grid sizes (5x5, 9x9, 11x11)
- [ ] Seasonal themes (Christmas, Halloween, etc)
- [ ] Statistics dashboard

### **v2.0 - Future** 🚀
- [ ] Mobile app (PWA/React Native)
- [ ] Tournament mode
- [ ] Replay system
- [ ] Level editor

---

## 📄 License

This project is released under the **MIT License**.

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

See [LICENSE](LICENSE) for full text.

---

## 👨‍💻 Author

**[Your Name]**

- 🌐 Portfolio: [your-website.com](https://your-website.com)
- 💼 LinkedIn: [@your-profile](https://linkedin.com/in/your-profile)
- 🐦 Twitter: [@your-handle](https://twitter.com/your-handle)
- 📧 Email: your.email@example.com

---

## 🙏 Acknowledgments

- 🤖 **Claude AI** (Anthropic) - development assistance
- 🧪 **Beta Testers** - valuable feedback
- 🎨 **Community** - suggestions and bug reports
- 📚 [MDN Web Docs](https://developer.mozilla.org) - JS/HTML/CSS documentation

---

## 📊 Statistics

![GitHub stars](https://img.shields.io/github/stars/max64180/grid-survivor?style=social)
![GitHub forks](https://img.shields.io/github/forks/max64180/grid-survivor?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/max64180/grid-survivor?style=social)

![Size](https://img.shields.io/github/repo-size/max64180/grid-survivor)
![Last Commit](https://img.shields.io/github/last-commit/max64180/grid-survivor)
![Issues](https://img.shields.io/github/issues/max64180/grid-survivor)
![License](https://img.shields.io/github/license/max64180/grid-survivor)

---

## 🎮 Tips & Tricks

### **Advanced Strategies**
1. **Use VISION strategically** - Activate when few safe cells remain
2. **Preventive SHIELD** - Use before risky situations
3. **Early MAGNET** - Discover bonuses early for planning
4. **LUCKY + critical situations** - Halve reds when needed
5. **Final SNIPER** - Perfect for eliminating last cell without risk

### **Malus Management**
- **Bad Luck Malus** 😈 - Doubles reds → Use LUCKY or VISION after
- **Cursed Cards** 🎴 - Lose bonuses → Choose strategically (1-3)
- **Mental Game** - Malus are part of the game, stay calm!

### **High Score Tips**
- **Streak Combo** - Keep streak high (exponential points)
- **x2 Points** - Use when you have high streak
- **Extra Lives** - More lives = more turns = more points
- **Point Bonuses** - +10000 can make the difference!

---

<div align="center">

## ⭐ **If you like Grid Survivor, leave a star on GitHub!** ⭐

[🎮 Play Now](https://max64180.github.io/grid-survivor/grid-survivor.html) • [🐛 Report Bug](https://github.com/max64180/grid-survivor/issues) • [💡 Request Feature](https://github.com/max64180/grid-survivor/issues) • [📖 Wiki](https://github.com/max64180/grid-survivor/wiki)

---

**Made with ❤️, ☕ and lots of 🎮**

*Grid Survivor v1.0 - 2025*

</div>
