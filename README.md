# 🎯 Grid Survivor

Un gioco di sopravvivenza su griglia 7×7 dove devi eliminare caselle evitando le mine nascoste!

![Game Preview](https://img.shields.io/badge/Made%20with-JavaScript-yellow)
![Firebase](https://img.shields.io/badge/Database-Firebase-orange)
![Status](https://img.shields.io/badge/Status-Online-brightgreen)

## 🎮 Gioca Ora!

**[▶️ GIOCA ONLINE](https://TUO-USERNAME.github.io/grid-survivor/grid-survivor.html)**

*(Sostituisci `TUO-USERNAME` con il tuo username GitHub)*

---

## 📖 Come Si Gioca

1. **Obiettivo**: Elimina tutte le 49 caselle senza colpire quelle rosse
2. **Timer**: Hai 8 secondi per scegliere una casella
3. **Vite**: Hai 3 vite - perdine una quando colpisci una casella rossa
4. **Bonus**: Colleziona power-up nascosti:
   - 🛡️ **SCUDO**: Ti salva dalla prossima colpita
   - 💣 **TRIPLO**: Elimina 3 caselle sicure
   - ⏱️ **TEMPO+**: +5 secondi al timer
   - 👁️ **VISIONE**: Rivela caselle sicure
   - 💰 **x2 PUNTI**: Doppi punti per 3 turni
   - 🆘 **LIFELINE**: 5 caselle bonus - se almeno una sopravvive, vai avanti
   - 🎲 **FORTUNA**: Dimezza le celle rosse per 1 turno
   - ❤️ **VITA+**: Guadagna una vita extra
   - 😈 **MALUS**: Trappola! Raddoppia il rischio al prossimo turno

5. **Punteggio**: Il moltiplicatore sale esponenzialmente per ogni casella consecutiva

---

## 🌟 Caratteristiche

- ✅ **Classifica Online Globale** con Firebase Realtime Database
- ✅ **Sistema di vite** con 3 tentativi
- ✅ **Bonus variabili** - ogni partita è diversa
- ✅ **Effetti sonori** sintetizzati (attivabili/disattivabili)
- ✅ **Animazioni fluide** e timer perimetrale
- ✅ **Preview bonus** all'inizio della partita
- ✅ **Responsive design** - gioca anche da mobile
- ✅ **Salvataggio locale + online** - funziona anche offline

---

## 🛠️ Tecnologie

- **HTML5 / CSS3 / JavaScript** (vanilla - no framework)
- **Firebase Realtime Database** per la classifica globale
- **GitHub Pages** per l'hosting gratuito
- **Web Audio API** per i suoni procedurali

---

## 🚀 Installazione Locale

Se vuoi giocare in locale o modificare il gioco:

```bash
# Clona il repository
git clone https://github.com/TUO-USERNAME/grid-survivor.git

# Apri il file HTML
cd grid-survivor
open grid-survivor.html  # macOS
start grid-survivor.html # Windows
xdg-open grid-survivor.html # Linux
```

---

## 🔥 Configurazione Firebase (per sviluppatori)

Se vuoi creare la tua istanza con database personale:

1. Segui la guida completa in `GUIDA_PUBBLICAZIONE.md`
2. Crea un progetto Firebase
3. Sostituisci le credenziali nel file HTML (sezione `firebaseConfig`)
4. Pubblica su GitHub Pages

---

## 📊 Statistiche

- **Celle totali**: 49 (7×7)
- **Bonus per partita**: 10 casuali
- **Difficoltà**: Dinamica (~33% di rischio costante)
- **Punteggio massimo teorico**: ~100.000+ punti

---

## 🎯 Strategie Vincenti

1. **Memorizza i bonus** durante il preview iniziale
2. **Usa il LIFELINE** nei momenti critici con poche celle rimaste
3. **Attiva FORTUNA** quando molte celle sono ancora da eliminare
4. **Risparmia lo SCUDO** per le fasi finali
5. **Fai attenzione ai MALUS** - appaiono come bonus ma sono trappole!

---

## 📝 Licenza

Questo progetto è rilasciato sotto licenza MIT - sentiti libero di modificarlo e condividerlo!

---

## 👨‍💻 Autore

Creato con ❤️ per divertimento e apprendimento

**Contributi benvenuti!** Apri una Issue o una Pull Request se hai idee per migliorare il gioco.

---

## 🏆 Record Mondiale

Il punteggio più alto nella classifica globale è... **ancora da stabilire!**

Sei tu il primo campione? 🎮
