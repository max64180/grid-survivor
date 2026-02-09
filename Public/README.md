# 🎮 Grid Survivor - Sopravvivi alla Griglia!

[![Version](https://img.shields.io/badge/version-1.2.2-blue.svg)](https://github.com)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-Active-success.svg)](https://github.com)

Un roguelike puzzle game innovativo dove devi eliminare tutte le 49 celle di una griglia 7×7 senza perdere le tue 3 vite. Memorizza i bonus, evita le trappole e sopravvivi!

![Grid Survivor Banner](https://via.placeholder.com/800x200/667eea/ffffff?text=Grid+Survivor)

---

## 🎯 **Caratteristiche Principali**

### **🎮 Gameplay Core**
- **Griglia 7×7** (49 celle totali)
- **Sistema a vite** (3 cuori all'inizio)
- **Timer countdown** con visualizzazione perimetrale SVG
- **Danger Zone invisibile** che si muove come una pallina da biliardo
- **Sistema di punteggio complesso** con streak multipliers e bonus posizionali

### **✨ Sistema Bonus (20+ tipi)**
- **10 bonus** posizionati casualmente ogni partita
- **Preview iniziale** di 3.4 secondi (delay 0.3s tra bonus)
- Bonus positivi: SHIELD, TRIPLE, VISION, LIFELINE, LUCKY, +750/1500/3000 punti
- Bonus negativi: MALUS (raddoppia celle rosse), CARD MALUS (perdi bonus)
- Bonus speciali: MYSTERY, PORTAL, GHOST

### **🎯 Sistema Punteggio Innovativo**
#### **Punteggio Base con Streak**
- +10 punti per cella eliminata
- Moltiplicatori esponenziali fino a streak 10
- Sistema incrementale da streak 11+
- Double Points power-up

#### **⭐ Punteggio Posizionale (NEW v1.2)**
Bonus basato sulla posizione della cella nella griglia:
```
Centro (distanza 0): +150 punti 🔥
Distanza 1: +110 punti
Distanza 2: +80 punti
Distanza 3: +50 punti
Distanza 4: +30 punti
Distanza 5: +15 punti
Angoli (distanza 6): +10 punti
```
**Totale possibile:** ~2.350 punti bonus posizionali completando tutte le celle!

**Animazione floating score:**
- Numeri dorati che salgono dalla cella
- Glow intenso per punteggi alti (≥100)
- Audio feedback differenziato (centro vs bordi)
- Responsive su tutti i dispositivi

### **🌐 Sistema Multilingua**
- 🇮🇹 Italiano
- 🇬🇧 English
- Supporto completo UI, tutorial, messaggi

### **🏆 Leaderboard System**
- **Doppio sistema:** Locale (localStorage) + Online (Firebase)
- Top 10 globale
- Badge per nuovi punteggi
- Medaglie 🥇🥈🥉
- Emoji personalizzate
- Trophy 🏆 per vittoria completa (49 celle)

### **📚 Tutorial Interattivo**
- 8 step guidati con illustrazioni
- Spiegazione di ogni meccanica
- Multilingua
- Completamento salvato (una volta sola)

### **🎨 UI/UX**
- Design gradient viola/blu moderno
- Animazioni CSS fluide
- Responsive design (mobile, tablet, desktop)
- Pause system
- Victory/Game Over modals eleganti
- Shield indicator animato
- Sound toggle (10+ effetti audio)

---

## 🚀 **Quick Start**

### **Giocare Online**
Apri semplicemente `grid-survivor.html` nel browser o visita:
```
https://tuo-username.github.io/grid-survivor/grid-survivor.html
```

### **Installazione Locale**
```bash
# Clona il repository
git clone https://github.com/tuo-username/grid-survivor.git

# Apri il file
cd grid-survivor
open grid-survivor.html
```

**Requisiti:** Nessuno! È un singolo file HTML standalone.

---

## 🎮 **Come Si Gioca**

### **Obiettivo**
Elimina tutte le 49 celle della griglia senza perdere tutte e 3 le vite.

### **Meccaniche**
1. **Seleziona una cella** entro 10 secondi (timer perimetrale)
2. Alcune celle diventano **rosse** (pericolose)
3. Se selezioni una cella rossa → **perdi 1 vita** ❤️
4. Se selezioni una cella sicura → **elimini la cella** e guadagni punti
5. **Memorizza i bonus** mostrati all'inizio
6. La **Danger Zone** invisibile influenza dove appaiono le celle rosse
7. Accumula **streak** per moltiplicatori maggiori
8. Le celle al **centro** danno più punti posizionali

### **Bonus Speciali**
- 🛡️ **SHIELD:** Ti salva dal prossimo colpo
- 👁️ **VISION:** Rivela 3 celle sicure per 5 secondi
- 🎯 **TRIPLE:** Elimina 3 celle sicure automaticamente
- 🔫 **SNIPER:** Elimina 1 cella rossa garantita
- 🧲 **MAGNET:** Mostra tutti i bonus per 3 secondi
- 🍀 **LUCKY:** Dimezza le celle rosse al prossimo turno
- ❤️ **LIFE+:** Guadagna 1 vita extra (max 3)
- 🆘 **LIFELINE:** Scelta multipla (5 celle, almeno 1 sicura)
- 💰 **+750/1500/3000:** Punti istantanei

### **Malus**
- 😈 **SFORTUNA:** Raddoppia celle rosse al prossimo turno
- 🃏 **CARTE MALEDETTE:** Scegli una carta, perdi 1-3 bonus

---

## 📊 **Statistiche e Bilanciamento**

### **Composizione Bonus (ogni partita)**
- **10 bonus totali**
- **0-3 vite extra** (media: ~1)
- **1 bonus punti** garantito (40% x2, 20% +750, 20% +1500, 20% +3000)
- **7-9 bonus regolari** (mix casuale)
- **0-1 malus** (60% probabilità)

### **Sistema Difficulty**
La difficoltà scala dinamicamente:
- Più celle elimini → più celle rosse appaiono
- Danger Zone concentra le celle rosse in una zona mobile
- Malus possono raddoppiare le celle rosse

### **Punteggi Attesi**
- **Principiante:** 200-500 punti (10-20 celle)
- **Intermedio:** 500-1200 punti (20-35 celle)
- **Esperto:** 1200-2500 punti (35-45 celle)
- **Vittoria completa:** 2500-4000+ punti (49 celle)

---

## 🔧 **Tecnologie Utilizzate**

### **Frontend**
- **HTML5** - Struttura
- **CSS3** - Styling, animazioni, responsive
- **JavaScript (ES6+)** - Game logic
- **SVG** - Timer perimetrale animato

### **Backend/Storage**
- **Firebase Realtime Database** - Leaderboard online
- **localStorage** - Salvataggio locale (leaderboard, lingua, tutorial)

### **API & Libraries**
- **Web Audio API** - Effetti sonori procedurali
- **Firebase SDK 9.x** - Integrazione database
- **Nessuna dipendenza npm** - Tutto standalone!

---

## 📱 **Supporto Dispositivi**

### **Desktop**
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

### **Mobile**
- ✅ iOS Safari 14+
- ✅ Chrome Mobile 90+
- ✅ Samsung Internet 14+

### **Responsive Breakpoints**
- **Desktop:** >768px - Full size
- **Tablet:** ≤768px - Reduced font sizes
- **Mobile:** ≤480px - Compact layout

---

## 🆕 **Changelog**

### **v1.2.2** (Febbraio 2026) - Current
#### Fixed
- 🐛 Risolto: griglia si allarga durante bonus preview
- 🐛 Risolto: punteggio posizionale coperto da notifiche bonus
- 🐛 Risolto: font punteggio troppo grande su mobile
- 🐛 Risolto: animazione punteggio non saliva (overflow hidden)

#### Changed
- ⚡ Preview bonus velocizzato: delay 0.5s → 0.3s (durata totale: 5.4s → 3.4s)
- 📱 Font punteggio posizionale responsive (0.75em-1.4em)
- 🎯 Z-index punteggio aumentato a 2500 (sempre visibile)

### **v1.2.0** (Febbraio 2026)
#### Added
- ⭐ **Sistema punteggio posizionale** (+10 a +150 basato su distanza dal centro)
- ✨ Animazione floating score con glow
- 🔊 Audio feedback differenziato per posizione
- 📊 ~2.350 punti bonus totali per completamento

#### Fixed
- 🐛 Bug traduzione nomi mostri in inglese

### **v1.1.0** (Febbraio 2026)
- 🌐 Sistema internazionalizzazione completo
- 📚 Tutorial interattivo 8-step
- 🏆 Leaderboard Firebase + locale
- 🎮 20+ bonus types
- 🎯 Danger Zone system

### **v1.0.0** (Gennaio 2026)
- 🎮 Release iniziale
- Core gameplay mechanics
- Sistema vite e punteggio base

---

## 🎯 **Roadmap Futura**

### **In Considerazione**
- 🎯 **Daily Challenge** (seed fisso giornaliero)
- ⏱️ **Time Attack Mode** (3 minuti, massimo punteggio)
- 🎁 **Bonus RADAR** (rivela Danger Zone per 5s)
- 📊 **Statistiche avanzate** (heatmap celle, win rate)
- 👥 **Co-op Mode** (2 giocatori, turni alternati)
- 🎨 **Temi stagionali** (Halloween, Natale)
- 🏆 **Achievement system** (badge sbloccabili)
- 📐 **Dimensioni griglia variabili** (5×5, 9×9, 11×11)

Vedi [ANALISI_EVOLUZIONI_GRID_SURVIVOR.md](./ANALISI_EVOLUZIONI_GRID_SURVIVOR.md) per dettagli completi.

---

## 🛠️ **Configurazione Firebase**

### **Setup Leaderboard Online**
1. Crea progetto Firebase: https://console.firebase.google.com
2. Abilita Realtime Database
3. Configura regole di sicurezza:
```json
{
  "rules": {
    "leaderboard": {
      ".read": true,
      ".write": true
    }
  }
}
```
4. Copia le credenziali in `firebaseConfig` (riga ~1968)
5. Pubblica!

### **Modalità Solo Locale**
Il gioco funziona perfettamente anche senza Firebase, usando solo localStorage.

---

## 📄 **Documentazione Aggiuntiva**

- [MODIFICHE_IMPLEMENTATE.md](./MODIFICHE_IMPLEMENTATE.md) - Log modifiche v1.2
- [SISTEMA_SPAWN_BONUS.md](./SISTEMA_SPAWN_BONUS.md) - Dettagli sistema bonus
- [ANALISI_EVOLUZIONI_GRID_SURVIVOR.md](./ANALISI_EVOLUZIONI_GRID_SURVIVOR.md) - Roadmap futuro
- [danger-zone-mockups.html](./danger-zone-mockups.html) - Mockup visuali Danger Zone

---

## 🤝 **Contribuire**

### **Bug Reports**
Apri una Issue su GitHub con:
- Descrizione del bug
- Steps per riprodurlo
- Screenshot/video se possibile
- Browser e dispositivo

### **Feature Requests**
Le feature request sono benvenute! Discutiamone nelle Issues.

### **Pull Requests**
1. Fork del repository
2. Crea un branch (`git checkout -b feature/AmazingFeature`)
3. Commit (`git commit -m 'Add AmazingFeature'`)
4. Push (`git push origin feature/AmazingFeature`)
5. Apri una Pull Request

---

## 🎮 **Easter Eggs**

- Admin reset classifica: aggiungi `?admin=GRIDWIN2024` all'URL
- 10 mostri diversi con nomi tradotti
- Animazione speciale per vittoria completa (49 celle)

---

## 📜 **Licenza**

Questo progetto è distribuito sotto licenza MIT. Vedi il file [LICENSE](LICENSE) per dettagli.

---

## 👨‍💻 **Autore**

Creato con ❤️ e ☕

- Website: [tuo-sito.com](https://tuo-sito.com)
- GitHub: [@tuo-username](https://github.com/tuo-username)

---

## 🙏 **Ringraziamenti**

- Anthropic Claude per supporto sviluppo
- Firebase per hosting leaderboard
- Comunità open-source

---

## 📞 **Supporto**

Hai domande? Contattami:
- 📧 Email: tuo-email@example.com
- 💬 Discord: tuo-username#1234
- 🐦 Twitter: [@tuo-username](https://twitter.com/tuo-username)

---

<div align="center">

**⭐ Se ti piace il gioco, lascia una stella su GitHub! ⭐**

[Play Now](https://tuo-username.github.io/grid-survivor) • [Report Bug](https://github.com/tuo-username/grid-survivor/issues) • [Request Feature](https://github.com/tuo-username/grid-survivor/issues)

Made with 🎮 and JavaScript

</div>
