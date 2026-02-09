# ✅ CHECKLIST VELOCE - Pubblica Grid Survivor in 15 Minuti

## 1️⃣ Firebase (5 minuti)

- [ ] Vai su https://console.firebase.google.com
- [ ] "Aggiungi progetto" → nome: `grid-survivor`
- [ ] Disabilita Analytics
- [ ] Menu → "Realtime Database" → "Crea database"
- [ ] Location: `europe-west1`
- [ ] Modalità: "test mode"
- [ ] ⚙️ → Impostazioni progetto → App web `</>` → `grid-survivor-web`
- [ ] **COPIA** il `firebaseConfig` (tutto il blocco)

## 2️⃣ GitHub (3 minuti)

- [ ] Vai su https://github.com
- [ ] "New repository" → nome: `grid-survivor`
- [ ] Public ✅
- [ ] Add README ✅
- [ ] "Create repository"

## 3️⃣ Modifica File (2 minuti)

- [ ] Apri `grid-survivor.html` in un editor di testo
- [ ] Cerca `YOUR_API_KEY` (circa riga 895)
- [ ] **SOSTITUISCI** tutto il blocco `firebaseConfig` con i tuoi dati
- [ ] Salva il file

## 4️⃣ Upload (2 minuti)

- [ ] Nel repository GitHub → "Add file" → "Upload files"
- [ ] Trascina `grid-survivor.html`
- [ ] Trascina `README.md` (opzionale)
- [ ] Commit message: "Initial release 🎮"
- [ ] "Commit changes"

## 5️⃣ GitHub Pages (3 minuti)

- [ ] Repository → "Settings" (tab in alto)
- [ ] Menu → "Pages"
- [ ] Branch: `main` (o `master`)
- [ ] Folder: `/ (root)`
- [ ] "Save"
- [ ] Aspetta 1-2 minuti
- [ ] Visita: `https://TUO-USERNAME.github.io/grid-survivor/grid-survivor.html`

---

## 🎉 FATTO!

Il tuo gioco è online! Condividi il link con gli amici!

---

## 🔧 Test che Funzioni

1. [ ] Apri il link del gioco
2. [ ] Gioca una partita
3. [ ] Salva il punteggio con un nome
4. [ ] Apri classifica → vedi "🌐 Classifica Online Globale" (verde)
5. [ ] Apri il gioco da un altro browser → il punteggio è lì!

Se vedi "💾 Classifica Locale" (arancione) = Firebase non configurato correttamente

---

## 🆘 Problemi?

**Firebase non si connette:**
- Controlla di aver copiato TUTTO il blocco `firebaseConfig`
- Verifica che `databaseURL` contenga il link corretto
- Apri Console browser (F12) → vedi errori?

**Gioco non si carica:**
- Aspetta 2-3 minuti dopo aver attivato Pages
- Verifica l'URL: deve finire con `/grid-survivor.html`
- Hard refresh: Ctrl+F5 (Win) / Cmd+Shift+R (Mac)

**Regole Firebase scadute (dopo 30 giorni):**
```json
{
  "rules": {
    "leaderboard": {
      ".read": true,
      ".write": true,
      ".indexOn": ["score"]
    }
  }
}
```

---

## 📱 Bonus: URL Breve

Il tuo link è troppo lungo?

Usa **bit.ly** o **tinyurl.com** per creare:
`https://bit.ly/grid-survivor-ITA` → più facile da condividere!
