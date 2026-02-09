# 🔧 Grid Survivor - Technical Documentation

Documentazione tecnica per sviluppatori che vogliono comprendere o modificare il codice.

---

## 📐 **Architettura del Codice**

### **Struttura File**
```
grid-survivor.html (singolo file ~4200 righe)
├── <head>
│   ├── Meta tags & title
│   └── <style> (righe 8-1536)
│       ├── Layout & Grid
│       ├── UI Components
│       ├── Animations
│       ├── Overlays & Modals
│       └── Responsive Media Queries
│
└── <body>
    ├── HTML Structure (righe 1537-1543)
    │   ├── Game Container
    │   ├── Grid & Cells (generati dinamicamente)
    │   ├── Stats Display
    │   ├── Bonus Display
    │   └── Overlays (tutorial, game over, leaderboard)
    │
    └── <script> (righe 1544-4180)
        ├── i18n System (righe 1544-1960)
        ├── Firebase Config (righe 1968-1990)
        ├── Tutorial System (righe 1992-2050)
        ├── Constants & State (righe 2279-2395)
        ├── Game Logic (righe 2396-3000)
        ├── Bonus System (righe 3000-3200)
        ├── UI Updates (righe 3200-3400)
        ├── Audio System (righe 2023-2130)
        └── Leaderboard (righe 3700-3900)
```

---

## 🎮 **Core Game State**

### **gameState Object**
```javascript
gameState = {
    // Scoring
    score: 0,
    cellsEliminated: 0,
    currentStreak: 0,
    bestStreak: 0,
    pointsStreak: 0,
    
    // Lives & Safety
    lives: 3,
    activeShield: false,
    
    // Selection & Timer
    selectedCell: null,
    timeRemaining: TIMER_DURATION,
    timerInterval: null,
    isGameActive: false,
    isProcessingReveal: false,
    isPaused: false,
    
    // Cells
    eliminatedCells: new Set(),
    
    // Bonuses
    bonusCells: new Map(),          // Map<cellIndex, bonusObject>
    collectedBonuses: [],
    allBonusesInGame: null,
    bonusHintShown: false,
    
    // Power-ups Active
    doublePointsRemaining: 0,
    visionActive: false,
    safeCells: [],
    lifelineActive: false,
    lifelineCells: [],
    luckyActive: false,
    malusActive: false,
    malusFound: false,
    
    // Danger Zone
    dangerZone: { 
        row: 0, 
        col: 0, 
        dir: { dr: 1, dc: 1 } 
    },
    
    // Meta
    roundNumber: 0,
    gameStarted: false,
    victoryAchieved: false
}
```

---

## 📊 **Sistema di Punteggio**

### **Calcolo Punti per Cella**

#### **1. Punti Base con Streak**
```javascript
// Esponenziale fino a streak 10
if (pointsStreak <= 10) {
    points = BASE_POINTS * Math.pow(MULTIPLIER, pointsStreak - 1);
    // Esempio: 10, 12, 14, 17, 21, 26, 32, 38, 46, 56, 384
}

// Incrementale da streak 11+
else {
    points = 384; // Cap
    for (let s = 11; s <= pointsStreak; s++) {
        bonus = BASE_BONUS + ((s - 11) * BONUS_INCREMENT);
        points += bonus;
    }
}
```

**Costanti:**
```javascript
const BASE_POINTS = 10;
const POINTS_MULTIPLIER = 1.2;
const CAP_STREAK = 10;
const BASE_BONUS = 20;
const BONUS_INCREMENT = 2;
```

#### **2. Punteggio Posizionale (v1.2)**
```javascript
function calculatePositionScore(row, col) {
    const center = 3; // Centro griglia 7×7
    const distance = Math.abs(row - center) + Math.abs(col - center);
    
    const scoreMap = {
        0: 150,  // Centro
        1: 110,
        2: 80,
        3: 50,
        4: 30,
        5: 15,
        6: 10    // Angoli
    };
    
    return scoreMap[distance] || 10;
}

// Applicazione
gameState.score += points;              // Base + streak
gameState.score += positionBonus;       // Posizionale (NO moltiplicatori)
```

#### **3. Moltiplicatori Attivi**
```javascript
// Double Points (bonus x2)
if (doublePointsRemaining > 0) {
    points *= 2;
    doublePointsRemaining--;
}
```

---

## 🎁 **Sistema Bonus**

### **Generazione Bonus (initGrid)**

```javascript
// 1. Posizioni interne (esclude bordi)
const interiorPositions = [];
for (let row = 1; row < GRID_SIZE - 1; row++) {
    for (let col = 1; col < GRID_SIZE - 1; col++) {
        interiorPositions.push(row * GRID_SIZE + col);
    }
}
shuffle(interiorPositions); // Randomizza

// 2. Vite Extra (0-3)
const rand = Math.random();
let extraLivesCount;
if (rand < 0.25) extraLivesCount = 0;
else if (rand < 0.75) extraLivesCount = 1;
else if (rand < 0.95) extraLivesCount = 2;
else extraLivesCount = 3;

// 3. Bonus Punti (1 garantito)
const pointRoll = Math.random();
if (pointRoll < 0.40) selectedPointBonus = x2_POINTS;
else if (pointRoll < 0.60) selectedPointBonus = PLUS_750;
else if (pointRoll < 0.80) selectedPointBonus = PLUS_1500;
else selectedPointBonus = PLUS_3000;

// 4. Pool espanso bonus regolari
const expandedPool = [];
bonusPool.forEach(bonus => {
    expandedPool.push(bonus);
    if (Math.random() < 0.7) {
        expandedPool.push(bonus); // 70% duplicato
    }
});

// 5. Malus (0-1)
const malusRoll = Math.random();
if (malusRoll < 0.30) {
    bonusCells.set(lastSlot, MALUS_TRAP);
} else if (malusRoll < 0.60) {
    bonusCells.set(secondLastSlot, CARD_MALUS);
}
// 40% nessun malus
```

### **Preview Bonus (showBonusPreview)**

```javascript
const delayBetween = 300;  // 0.3s tra bonus
const showDuration = 400;  // 0.4s acceso
const totalDuration = (numBonus * delayBetween) + showDuration;

bonusCellsArray.forEach(([cellIndex, bonus], i) => {
    setTimeout(() => {
        cell.classList.add('bonus-preview');
        cell.textContent = bonus.icon;
        
        setTimeout(() => {
            cell.classList.remove('bonus-preview');
            cell.textContent = '';
        }, showDuration);
    }, i * delayBetween);
});
```

---

## 🎯 **Danger Zone System**

### **Inizializzazione**
```javascript
function initDangerZone() {
    // Posizione casuale interna
    const row = 1 + Math.floor(Math.random() * (GRID_SIZE - 2));
    const col = 1 + Math.floor(Math.random() * (GRID_SIZE - 2));
    
    // Direzione diagonale casuale
    const signs = [-1, 1];
    const dr = signs[Math.floor(Math.random() * 2)];
    const dc = signs[Math.floor(Math.random() * 2)];
    
    gameState.dangerZone = { row, col, dir: { dr, dc } };
}
```

### **Movimento (ogni round)**
```javascript
function moveDangerZone() {
    const dz = gameState.dangerZone;
    let newRow = dz.row + dz.dir.dr;
    let newCol = dz.col + dz.dir.dc;
    
    // Rimbalzo sui bordi
    if (newRow < 0 || newRow >= GRID_SIZE) {
        dz.dir.dr *= -1;
        newRow = dz.row + dz.dir.dr;
    }
    if (newCol < 0 || newCol >= GRID_SIZE) {
        dz.dir.dc *= -1;
        newCol = dz.col + dz.dir.dc;
    }
    
    dz.row = newRow;
    dz.col = newCol;
}
```

### **Estrazione Celle Rosse**
```javascript
function extractDangerCells(pool, count) {
    const dz = gameState.dangerZone;
    
    // Partiziona: dentro (dist ≤ 2) vs fuori
    const inside = [];
    const outside = [];
    
    pool.forEach(idx => {
        const row = Math.floor(idx / GRID_SIZE);
        const col = idx % GRID_SIZE;
        const dist = Math.abs(row - dz.row) + Math.abs(col - dz.col);
        
        if (dist <= 2) inside.push(idx);
        else outside.push(idx);
    });
    
    // Pesca ~75% da inside, resto da outside
    const insideCount = Math.min(
        Math.ceil(count * 0.75),
        inside.length
    );
    const outsideCount = count - insideCount;
    
    shuffle(inside);
    shuffle(outside);
    
    return [
        ...inside.slice(0, insideCount),
        ...outside.slice(0, outsideCount)
    ];
}
```

---

## ⏱️ **Timer System**

### **Perimetrale SVG**
```javascript
function startTimer() {
    const svg = document.getElementById('timer-perimeter');
    const rect = document.getElementById('timer-rect');
    
    // Calcola perimetro rettangolo
    const width = gridWrap.offsetWidth;
    const height = gridWrap.offsetHeight;
    const perimeter = 2 * (width + height);
    
    // Setup dasharray
    rect.style.strokeDasharray = perimeter;
    rect.style.strokeDashoffset = 0;
    
    // Countdown
    const interval = setInterval(() => {
        gameState.timeRemaining -= 100;
        
        const fraction = gameState.timeRemaining / TIMER_DURATION;
        const offset = perimeter * (1 - fraction);
        rect.style.strokeDashoffset = offset;
        
        // Cambia colore
        if (fraction < 0.2) svg.classList.add('danger');
        else if (fraction < 0.4) svg.classList.add('warning');
        
        // Suoni tick
        if (gameState.timeRemaining <= 3000 && ...) {
            playTickSound();
        }
        
        // Scaduto
        if (gameState.timeRemaining <= 0) {
            clearInterval(interval);
            endGame();
        }
    }, 100);
}
```

---

## 🔊 **Audio System**

### **Web Audio API (Procedural)**
```javascript
function getAudioCtx() {
    if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    return audioCtx;
}

function playTickSound() {
    if (!soundEnabled) return;
    
    const ctx = getAudioCtx();
    const now = ctx.currentTime;
    
    const oscillator = ctx.createOscillator();
    const gainNode = ctx.createGain();
    
    oscillator.connect(gainNode);
    gainNode.connect(ctx.destination);
    
    oscillator.type = 'sine';
    oscillator.frequency.setValueAtTime(1200, now);
    
    gainNode.gain.setValueAtTime(0.15, now);
    gainNode.gain.exponentialRampToValueAtTime(0.001, now + 0.05);
    
    oscillator.start(now);
    oscillator.stop(now + 0.05);
}
```

**Suoni Implementati:**
- `playTickSound()` - Timer tick (1200 Hz)
- `playLifeLostSound()` - Vita persa (600→150 Hz sawtooth)
- `playShieldSound()` - Shield attivato (400→800 Hz)
- `playEvilLaughSound()` - Malus (150→500 Hz square)
- `playPositionScoreHighSound()` - Centro griglia (880 Hz)
- `playPositionScoreLowSound()` - Bordi (660 Hz)

---

## 🌐 **Internazionalizzazione**

### **Sistema i18n**
```javascript
window.GridSurvivorI18N = {
    currentLang: localStorage.getItem('gridSurvivorLang') || 'it',
    
    strings: {
        it: { /* ... */ },
        en: { /* ... */ }
    },
    
    t: function(key) {
        return this.strings[this.currentLang][key] 
            || this.strings['it'][key] 
            || key;
    },
    
    changeLang: function(lang) {
        this.currentLang = lang;
        localStorage.setItem('gridSurvivorLang', lang);
        location.reload();
    }
};

// Helper globale
window.t = (key) => window.GridSurvivorI18N.t(key);

// Template strings con variabili
function tpl(key, vars) {
    let str = t(key);
    Object.keys(vars).forEach(k => {
        str = str.replace(`{${k}}`, vars[k]);
    });
    return str;
}

// Uso
updateMessage(tpl('msgOhNo', {count: 5}), 'danger');
// Output: "💥 OH NO! Una delle 5 caselle era la tua!"
```

---

## 🏆 **Leaderboard System**

### **Dual Storage**
```javascript
// Locale (fallback sempre attivo)
function saveToLocalLeaderboard(entry) {
    let leaderboard = JSON.parse(
        localStorage.getItem('gridSurvivorLeaderboard') || '[]'
    );
    leaderboard.push(entry);
    leaderboard.sort((a, b) => b.score - a.score);
    leaderboard = leaderboard.slice(0, 10); // Top 10
    localStorage.setItem('gridSurvivorLeaderboard', JSON.stringify(leaderboard));
}

// Online (Firebase)
async function saveToOnlineLeaderboard(entry) {
    if (!useOnlineLeaderboard || !database) return;
    
    try {
        const ref = database.ref('leaderboard');
        await ref.push(entry);
        
        // Mantieni solo top 10
        const snapshot = await ref.orderByChild('score').limitToLast(10).once('value');
        // ... cleanup
    } catch (error) {
        console.error('Firebase save failed:', error);
    }
}
```

### **Entry Structure**
```javascript
{
    name: "Player",
    emoji: "🎮",
    score: 2500,
    cells: 45,
    streak: 12,
    victory: false,  // true se 49 celle
    timestamp: Date.now()
}
```

---

## 🎨 **CSS Architecture**

### **Naming Convention**
```
.component-name { }         // Main component
.component-name-modifier { } // Variant
.component-name.state { }    // State class
```

### **Key Classes**
- `.grid-cell` - Cella base
- `.grid-cell.selected` - Cella selezionata (blu)
- `.grid-cell.eliminated` - Cella eliminata (verde)
- `.grid-cell.revealed` - Cella rossa rivelata
- `.grid-cell.bonus-preview` - Preview bonus (oro)
- `.position-score` - Animazione punteggio posizionale
- `.bonus-notification` - Popup centrale bonus

### **Animations**
```css
@keyframes floatScore {
    0%   { transform: translate(-50%, -50%) scale(0.8); opacity: 1; }
    30%  { transform: translate(-50%, calc(-50% - 15px)) scale(1.2); opacity: 1; }
    100% { transform: translate(-50%, calc(-50% - 50px)) scale(1.4); opacity: 0; }
}

@keyframes heartLost {
    0%   { transform: scale(1); }
    25%  { transform: scale(1.3) rotate(-12deg); }
    50%  { transform: scale(0.8) rotate(8deg); }
    100% { transform: scale(1); opacity: 0.35; }
}
```

---

## 📱 **Responsive Design**

### **Breakpoints**
```css
/* Desktop: default (>768px) */

/* Tablet */
@media (max-width: 768px) {
    .position-score { font-size: 0.9em; }
    .grid-cell { font-size: 1em; }
}

/* Mobile */
@media (max-width: 480px) {
    .position-score { font-size: 0.75em; }
    .grid-cell { font-size: 0.9em; }
    .game-container { padding: 12px; }
}
```

### **Touch Optimization**
```css
.grid-cell {
    cursor: pointer;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
}
```

---

## 🔧 **Costanti Configurabili**

### **Timing**
```javascript
const TIMER_DURATION = 10000;           // 10 secondi per selezione
const BONUS_PREVIEW_DELAY = 300;        // 0.3s tra bonus
const BONUS_PREVIEW_SHOW = 400;         // 0.4s durata singolo bonus
```

### **Bonus**
```javascript
const MAX_BONUSES_PER_GAME = 10;        // Totale bonus
const EXTRA_LIVES_PROBABILITY = {       // Probabilità vite extra
    0: 0.25,
    1: 0.50,
    2: 0.20,
    3: 0.05
};
```

### **Scoring**
```javascript
const BASE_POINTS = 10;
const POINTS_MULTIPLIER = 1.2;
const CAP_STREAK = 10;
const POSITION_SCORE_MAP = {
    0: 150, 1: 110, 2: 80, 3: 50, 4: 30, 5: 15, 6: 10
};
```

---

## 🧪 **Testing & Debug**

### **Console Commands**
```javascript
// In browser console
gameState.lives = 99;              // Vite infinite
gameState.score = 10000;           // Set punteggio
gameState.activeShield = true;     // Attiva shield
document.getElementById('grid-container').style.outline = '2px solid red'; // Debug layout
```

### **URL Parameters**
```
?admin=GRIDWIN2024  →  Abilita admin reset button
```

### **localStorage Keys**
```javascript
'gridSurvivorLeaderboard'  // Array leaderboard locale
'gridSurvivorLang'         // Lingua corrente
'tutorialCompleted'        // Boolean tutorial fatto
```

---

## 🚀 **Performance**

### **Ottimizzazioni Implementate**
- ✅ Singolo file HTML (zero network requests)
- ✅ CSS transitions hardware-accelerated
- ✅ Event delegation (non listener per cella)
- ✅ setTimeout batch per preview bonus
- ✅ Set() per lookup O(1) su celle eliminate
- ✅ Map() per lookup O(1) su bonus

### **Metriche Target**
- Load time: <500ms
- FPS: 60 costanti
- Memory: <50MB
- Bundle size: ~150KB (single HTML)

---

## 🔐 **Sicurezza**

### **Firebase Rules**
```json
{
  "rules": {
    "leaderboard": {
      ".read": true,
      ".write": true,
      ".validate": "newData.hasChildren(['name', 'score', 'timestamp'])",
      "$entry": {
        "score": { ".validate": "newData.isNumber() && newData.val() >= 0" },
        "name": { ".validate": "newData.isString() && newData.val().length <= 20" }
      }
    }
  }
}
```

### **Input Sanitization**
```javascript
function sanitizeName(name) {
    return name
        .trim()
        .slice(0, 20)
        .replace(/[<>]/g, ''); // Basic XSS prevention
}
```

---

## 📚 **Risorse Utili**

- MDN Web Audio API: https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API
- Firebase Realtime Database: https://firebase.google.com/docs/database
- CSS Grid Layout: https://css-tricks.com/snippets/css/complete-guide-grid/
- SVG Paths: https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths

---

**Ultimo aggiornamento:** Febbraio 2026 | **Versione:** 1.2.2
