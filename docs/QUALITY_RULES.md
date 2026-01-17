# NSTech Website - Qualitätssicherungsregeln

Version: 2.0  
Datum: 17. Januar 2026  
Verantwortlich: NSTech Development Team

---

## 📋 Übersicht

Dieses Dokument definiert die verbindlichen Qualitätsregeln für die NSTech Website. Jede Änderung MUSS diese Regeln erfüllen, bevor sie deployed wird.

**KRITISCH**: Nach dem API Key Security Incident vom 17.01.2026 wurde REGEL 3 hinzugefügt.

---

## ✅ REGEL 1: Mehrsprachigkeits-Kontrolle (DE/EN)

### Beschreibung
**Nach jeder Änderung MUSS überprüft werden, dass alle Inhalte sowohl in Deutsch als auch in Englisch existieren.**

### Geltungsbereich
Diese Regel gilt für:
- ✅ Alle Seiten mit Sprach-Varianten (index.html ↔ index-en.html)
- ✅ Navigationselemente (Desktop + Mobile)
- ✅ Footer-Links
- ✅ Call-to-Action Buttons
- ✅ Formulare und deren Labels
- ✅ Meta-Tags (title, description)
- ✅ Fehlermeldungen

### Ausnahmen
- ❌ Blog-Artikel (können zunächst nur auf Deutsch sein)
- ❌ Legal Pages (Datenschutz/Impressum nur auf Deutsch erforderlich)

### Checkliste: Mehrsprachigkeit

#### Bei neuen Seiten:
- [ ] Deutsche Version erstellt (z.B. `leistungen.html`)
- [ ] Englische Version erstellt (z.B. `services-en.html`)
- [ ] Beide Seiten haben identische Struktur
- [ ] Alle Texte übersetzt (kein Lorem Ipsum, kein deutscher Text in EN-Version)
- [ ] Meta-Tags übersetzt (title, description, keywords)
- [ ] Sprachschalter verlinkt auf korrespondierende Seite

#### Bei Änderungen an bestehenden Seiten:
- [ ] Änderung in deutscher Version durchgeführt
- [ ] Exakt gleiche Änderung in englischer Version durchgeführt
- [ ] Inhaltsvergleich: Absätze, Überschriften, Listen identisch
- [ ] Bilder/Icons: gleiche Assets in beiden Versionen

#### Navigation:
- [ ] Neuer Menüpunkt in DE-Navigation hinzugefügt
- [ ] Korrespondierender Menüpunkt in EN-Navigation hinzugefügt
- [ ] Mobile-Menü in beiden Sprachen aktualisiert
- [ ] Sprachschalter (DE/EN Buttons) auf allen Seiten funktional

#### Formulare:
- [ ] Input-Labels übersetzt
- [ ] Placeholder-Texte übersetzt
- [ ] Button-Texte übersetzt
- [ ] Validierungsmeldungen übersetzt
- [ ] Erfolgs-/Fehlermeldungen übersetzt

### Verifizierungs-Methode

```bash
# Automatischer Check (kann als Pre-Commit Hook verwendet werden)
# Vergleicht Seitenstrukturen

# 1. Zähle Abschnitte
grep -c "<section" index.html
grep -c "<section" index-en.html
# Sollten identisch sein

# 2. Prüfe Navigation
grep -o 'href="[^"]*"' index.html | wc -l
grep -o 'href="[^"]*"' index-en.html | wc -l
# Sollten identisch sein

# 3. Suche nach deutschem Text in EN-Dateien
grep -E "(Startseite|Über Uns|Kontakt|Unsere|Wir)" *-en.html
# Sollte LEER sein
```

### Beispiele

#### ✅ KORREKT:
```html
<!-- index.html -->
<a href="kontakt.html">Kontakt</a>

<!-- index-en.html -->
<a href="contact.html">Contact</a>
```

#### ❌ FALSCH:
```html
<!-- index.html -->
<a href="kontakt.html">Kontakt</a>

<!-- index-en.html -->
<a href="contact.html">Kontakt</a> <!-- Deutscher Text in EN-Version! -->
```

---

## ✅ REGEL 2: Responsive Design Kontrolle

### Beschreibung
**Nach jeder Änderung MUSS überprüft werden, dass die Website auf allen Geräten korrekt dargestellt wird.**

### Geltungsbereich
Diese Regel gilt für:
- ✅ Alle HTML-Seiten
- ✅ Alle Komponenten (Navigation, Footer, Cards, Formulare)
- ✅ Alle Breakpoints (Mobile, Tablet, Desktop)
- ✅ Alle Bilder und Medien
- ✅ Alle interaktiven Elemente

### Test-Breakpoints

| Device | Viewport | Tailwind Breakpoint |
|--------|----------|---------------------|
| **Mobile (klein)** | 320px - 374px | Default (< sm) |
| **Mobile (groß)** | 375px - 639px | Default (< sm) |
| **Tablet** | 640px - 1023px | `sm:` und `md:` |
| **Desktop** | 1024px - 1279px | `lg:` |
| **Large Desktop** | 1280px+ | `xl:` |

### Checkliste: Responsive Design

#### Layout:
- [ ] Kein horizontales Scrollen auf mobilen Geräten (< 640px)
- [ ] Alle Container passen in Viewport
- [ ] Grid-Layouts brechen korrekt um (z.B. `md:grid-cols-3` → mobile: 1 Spalte)
- [ ] Padding/Margins sind auf Mobile angemessen (nicht zu groß/klein)

#### Navigation:
- [ ] Desktop-Navigation (768px+): Horizontal sichtbar
- [ ] Mobile-Navigation (< 768px): Hamburger-Menü funktional
- [ ] Sprachschalter auf allen Viewports sichtbar
- [ ] Keine überlappenden Elemente
- [ ] Logo skaliert korrekt

#### Typografie:
- [ ] Überschriften (h1-h6) skalieren mit Tailwind responsive classes:
  - `text-2xl md:text-3xl lg:text-4xl`
- [ ] Texte bleiben lesbar (min. 16px auf Mobile)
- [ ] Keine abgeschnittenen Texte
- [ ] Line-height angemessen für Mobile

#### Bilder & Medien:
- [ ] Bilder skalieren mit `max-w-full` oder `w-full`
- [ ] `aspect-ratio` definiert oder `object-cover` verwendet
- [ ] Keine verzerrten Bilder
- [ ] Lazy-loading aktiviert für Performance
- [ ] Alt-Texte vorhanden

#### Buttons & Interaktive Elemente:
- [ ] Mindestgröße 44x44px (Touch-Target)
- [ ] Genug Abstand zwischen klickbaren Elementen (min. 8px)
- [ ] Hover-Effekte nur auf Desktop (`:hover` nicht auf Touch)
- [ ] Active/Focus-States definiert

#### Formulare:
- [ ] Input-Felder 100% Breite auf Mobile
- [ ] Labels über Inputs (nicht links)
- [ ] Submit-Buttons groß genug für Touch
- [ ] Keine horizontalen Input-Gruppen auf Mobile

#### Tabellen:
- [ ] Overflow-x-auto für große Tabellen
- [ ] Alternative Card-Layout auf Mobile (falls nötig)
- [ ] Keine abgeschnittenen Inhalte

#### Footer:
- [ ] Grid bricht um: `md:grid-cols-4` → Mobile: 1 Spalte
- [ ] Links bleiben klickbar
- [ ] Copyright-Text lesbar

### Verifizierungs-Methode

#### Browser DevTools Test:
```
1. Öffne Chrome/Firefox DevTools (F12)
2. Toggle Device Toolbar (Ctrl+Shift+M)
3. Teste folgende Geräte:
   - iPhone SE (375 x 667)
   - iPhone 14 Pro (393 x 852)
   - iPad (768 x 1024)
   - iPad Pro (1024 x 1366)
   - Desktop (1920 x 1080)
4. Prüfe Landscape & Portrait Orientierung
```

#### Automatische Tests:
```bash
# Lighthouse CI für Mobile Performance
npx lighthouse https://nstech.de --only-categories=performance --preset=mobile --quiet

# Responsive Image Check
grep -r 'max-w-full\|w-full' *.html | wc -l
# Alle Bilder sollten responsive classes haben
```

#### Manuelle Checkliste pro Seite:
- [ ] Mobile (375px): Scrollen Sie gesamte Seite, kein overflow-x
- [ ] Tablet (768px): Grid-Layouts korrekt umgebrochen
- [ ] Desktop (1280px): Alle Elemente nutzen verfügbaren Platz

### Häufige Fehler vermeiden

#### ❌ FALSCH:
```html
<!-- Feste Breiten -->
<div style="width: 800px">...</div>

<!-- Keine responsive Textgrößen -->
<h1 class="text-6xl">Überschrift</h1>

<!-- Kein Mobile-Menü -->
<nav class="flex space-x-8">...</nav>
```

#### ✅ KORREKT:
```html
<!-- Max-width mit Container -->
<div class="max-w-7xl mx-auto px-4">...</div>

<!-- Responsive Textgrößen -->
<h1 class="text-3xl md:text-5xl lg:text-6xl">Überschrift</h1>

<!-- Mobile + Desktop Navigation -->
<nav>
  <div class="hidden md:flex space-x-8">...</div>
  <div class="md:hidden">Hamburger Menu</div>
</nav>
```

### Tailwind CSS Responsive Pattern

```html
<!-- Standard-Muster für responsive Komponenten -->

<!-- Grid: Mobile 1col, Tablet 2col, Desktop 3col -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

<!-- Padding: Mobile klein, Desktop groß -->
<section class="py-12 md:py-16 lg:py-24">

<!-- Text: Skaliert mit Viewport -->
<h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl">

<!-- Flex Direction: Mobile vertikal, Desktop horizontal -->
<div class="flex flex-col md:flex-row gap-4">

<!-- Hidden auf bestimmten Größen -->
<div class="hidden md:block">Desktop only</div>
<div class="md:hidden">Mobile only</div>
```

---

## 🔄 Workflow: Änderungen durchführen

### Schritt-für-Schritt Prozess

```
1. ÄNDERUNG PLANEN
   └─ Welche Seiten betroffen?
   └─ DE + EN erforderlich?
   └─ Responsive-kritisch?

2. ENTWICKLUNG
   └─ Deutsche Version ändern
   └─ Englische Version anpassen
   └─ Tailwind responsive classes nutzen

3. LOKALER TEST
   └─ Browser DevTools (F12)
   └─ Teste Mobile (375px)
   └─ Teste Tablet (768px)
   └─ Teste Desktop (1280px+)

4. CHECKLISTEN DURCHGEHEN
   └─ REGEL 1: DE/EN Checkliste
   └─ REGEL 2: Responsive Checkliste

5. CODE REVIEW
   └─ Zweites Paar Augen
   └─ Checklisten abhaken

6. DEPLOYMENT
   └─ Git commit mit Checklist in Message
   └─ Push to production

7. POST-DEPLOYMENT CHECK
   └─ Live-Website testen
   └─ Beide Sprachen prüfen
   └─ Mobile Device real testen
```

### Git Commit Template

```bash
git commit -m "
feat: Add ISTQB logo to stats section

✅ REGEL 1 - Mehrsprachigkeit:
- [x] Deutsche Version (index.html, leistungen.html)
- [x] Englische Version (index-en.html, services-en.html)
- [x] Alle Texte übersetzt
- [x] Navigation aktualisiert

✅ REGEL 2 - Responsive:
- [x] Mobile (375px) getestet
- [x] Tablet (768px) getestet
- [x] Desktop (1280px+) getestet
- [x] Logo skaliert korrekt
"
```

---

## 📊 Monitoring & Reporting

### Wöchentliche Checks

**Jeden Montag**:
- [ ] Alle Seiten auf Deutsch durchklicken
- [ ] Alle Seiten auf Englisch durchklicken
- [ ] Mobile Test auf echtem Gerät
- [ ] Lighthouse Score überprüfen (sollte > 90 sein)

### Monatliche Audits

**Jeden 1. des Monats**:
- [ ] Vollständiger Mehrsprachigkeits-Vergleich
- [ ] Cross-Browser Test (Chrome, Firefox, Safari, Edge)
- [ ] Performance-Analyse
- [ ] Broken Links Check
- [ ] Accessibility Audit (WCAG 2.1 AA)

### Tools & Automatisierung

```bash
# Broken Links finden
npm install -g broken-link-checker
blc https://nstech.de -ro

# Lighthouse CI
npm install -g @lhci/cli
lhci autorun --collect.url=https://nstech.de

# Accessibility Check
npm install -g pa11y
pa11y https://nstech.de
```

---

## 🚨 Eskalation bei Regelverstoß

### Severity Levels

#### 🔴 KRITISCH (Sofort fixen):
- Fehlendes DE/EN auf Hauptseiten
- Broken Layout auf Mobile
- Nicht funktionierende Navigation
- Formular nicht nutzbar

#### 🟡 MEDIUM (Innerhalb 48h fixen):
- Inkonsistente Übersetzungen
- Kleine Layout-Shifts
- Fehlende Alt-Texte
- Performance-Issues (Score < 80)

#### 🟢 NIEDRIG (Backlog):
- Typos
- Kleine CSS-Optimierungen
- Nice-to-have Features

---

## 📝 Änderungshistorie

| Datum | Version | Änderung | Autor |
|-------|---------|----------|-------|
| 17.01.2025 | 1.0 | Initiale Erstellung der Quality Rules | NSTech Dev Team |

---

## ✅ REGEL 3: API Key & Security Kontrolle

### Beschreibung
**API Keys, Secrets, Passwörter und andere sensitive Daten DÜRFEN NIEMALS in Git committed werden.**

### Geltungsbereich
Diese Regel gilt für:
- ✅ Alle API Keys (Gemini, Resend, Stripe, etc.)
- ✅ Database Credentials
- ✅ OAuth Secrets & Tokens
- ✅ Private Keys (.pem, .key Dateien)
- ✅ Passwörter und Hashes
- ✅ Environment-spezifische Konfigurationen

### Verbotene Praktiken

#### ❌ NIEMALS:
```javascript
// FALSCH - API Key direkt im Code
const GEMINI_API_KEY = 'AIzaSyA64_I1K4dJR3Qpxo82knmOVFsUvs6Ng7A';

// FALSCH - In Konfigurationsdatei
export const config = {
  apiKey: 're_MZMBTTVt_AaFmTRdsCk5HVYHQaxsrsRwH'
};

// FALSCH - In README/Dokumentation
RESEND_API_KEY=re_MZMBTTVt_AaFmTRdsCk5HVYHQaxsrsRwH
```

#### ✅ KORREKT:
```javascript
// RICHTIG - Environment Variable
const GEMINI_API_KEY = process.env.GEMINI_API_KEY;

// RICHTIG - Placeholder in Dokumentation
// .env.example
GEMINI_API_KEY=your_gemini_api_key_here
RESEND_API_KEY=your_resend_api_key_here

// RICHTIG - Config mit ENV
export const config = {
  apiKey: process.env.RESEND_API_KEY
};
```

### Checkliste: Security

#### Vor jedem Commit:
- [ ] Keine API Keys in Code-Dateien (`.js`, `.html`, `.ts`, `.py`)
- [ ] Keine Secrets in Konfigurationsdateien
- [ ] Keine Credentials in README/Dokumentation
- [ ] `.env` Datei ist in `.gitignore` enthalten
- [ ] `.env.example` existiert (mit Placeholders)
- [ ] Sensitive Dateien in `.gitignore` gelistet

#### .gitignore Mindestanforderungen:
```gitignore
# Environment variables - NEVER COMMIT!
.env
.env.local
.env.development
.env.production
.env.test

# API Keys and Secrets
config.js
secrets.js
*.key
*.pem
credentials.json

# Logs (können Secrets enthalten)
logs/
*.log
npm-debug.log*
```

#### Bei API Key Exposure:
1. **SOFORT Key invalidieren/löschen** (Google AI Studio, Resend, etc.)
2. Neuen Key generieren
3. Key in `.env` speichern (NICHT committen!)
4. Git History cleanen:
   ```bash
   # Mit git-filter-repo
   pip install git-filter-repo
   git filter-repo --replace-text <(echo "EXPOSED_KEY==>REMOVED_KEY")
   git push origin --force --all
   ```
5. Team informieren
6. Security-Incident dokumentieren

### Verifizierungs-Methode

#### Pre-Commit Check:
```bash
# Suche nach API Key Patterns
git diff --cached | grep -E "(api[_-]?key|API[_-]?KEY|secret|SECRET|password|PASSWORD|token|TOKEN)" && echo "⚠️  WARNUNG: Möglicherweise API Key gefunden!"

# Suche nach Email-Adressen in neuen Dateien
git diff --cached | grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" && echo "⚠️  WARNUNG: Email-Adresse gefunden!"

# Suche nach Key-Patterns (Base64, Hex, etc.)
git diff --cached | grep -E "(AIza[0-9A-Za-z_-]{35}|sk_live_[0-9A-Za-z]{24,}|pk_live_[0-9A-Za-z]{24,})" && echo "⚠️  WARNUNG: API Key Pattern gefunden!"
```

#### Automated Pre-Commit Hook:
```bash
# .git/hooks/pre-commit
#!/bin/bash
if git diff --cached | grep -qE "(AIza[0-9A-Za-z_-]{35}|sk_live_|pk_live_|re_[0-9A-Za-z]{20,})"; then
    echo "❌ COMMIT ABGELEHNT: API Key gefunden!"
    echo "Entfernen Sie den API Key und verwenden Sie .env"
    exit 1
fi
```

### .env Datei Best Practices

#### Struktur:
```env
# ============================================
# NSTech API Configuration
# ============================================
# WICHTIG: Diese Datei NIEMALS committen!
# Kopiere .env.example und fülle deine Keys ein
# ============================================

# Gemini AI API Key
# Hole von: https://aistudio.google.com/app/apikey
GEMINI_API_KEY=

# Resend Email API Key
# Hole von: https://resend.com/api-keys
RESEND_API_KEY=

# Server Configuration
PORT=3000
NODE_ENV=development
```

#### .env.example (für Git):
```env
# API Keys Template - Copy to .env and fill in

GEMINI_API_KEY=your_gemini_api_key_here
RESEND_API_KEY=your_resend_api_key_here
PORT=3000
NODE_ENV=development
```

### Production Deployment

#### Vercel/Netlify:
- ✅ Environment Variables in Dashboard setzen
- ✅ Niemals `.env` hochladen
- ✅ Separate Keys für Production/Staging

#### GitHub Actions:
- ✅ Secrets in Repository Settings speichern
- ✅ Nicht in Logs ausgeben

### Beispiele häufiger Fehler

#### ❌ Fehler 1: API Key in HTML
```html
<script>
const API_KEY = 'AIzaSyA64_I1K4dJR3Qpxo82knmOVFsUvs6Ng7A';
</script>
```

#### ❌ Fehler 2: Credential in README
```markdown
## Setup
Run: RESEND_API_KEY=re_MZMBTTVt npm start
```

#### ❌ Fehler 3: .env in Repository
```bash
# Dateistruktur:
├── .env          # ❌ DARF NICHT COMMITTED SEIN!
├── .gitignore
└── server.js
```

#### ✅ Korrekt:
```bash
# Dateistruktur:
├── .env          # In .gitignore (nicht in Git)
├── .env.example  # ✅ In Git (nur Template)
├── .gitignore    # ✅ Enthält .env
└── server.js     # ✅ Nutzt process.env
```

### Notfall-Prozedur

Falls API Key versehentlich committed wurde:

1. **SOFORT** Key invalidieren (höchste Priorität!)
2. Neuen Key generieren und in `.env` speichern
3. Commit mit Key aus History entfernen:
   ```bash
   # Option 1: git-filter-repo (empfohlen)
   git filter-repo --replace-text replacements.txt
   
   # Option 2: BFG Repo-Cleaner
   java -jar bfg.jar --replace-text replacements.txt
   
   # Option 3: Letzter Commit (nur wenn noch nicht gepusht)
   git reset --soft HEAD~1
   git restore --staged .
   ```
4. Force-Push (Team informieren!):
   ```bash
   git push origin --force --all
   ```
5. Security-Incident dokumentieren
6. Post-Mortem: Warum passiert? Wie verhindern?

---

## 📞 Verantwortlichkeiten

- **Content (DE/EN)**: Erol Işıldak
- **Development**: NSTech Dev Team
- **QA Testing**: NSTech QA Team
- **Security**: Erol Işıldak + Dev Team
- **Deployment**: DevOps Team

---

## 🎯 Zusammenfassung

### Die 3 Goldenen Regeln:

1. **🌐 REGEL 1**: Jede Änderung = Deutsch UND Englisch
2. **📱 REGEL 2**: Jede Änderung = Mobile, Tablet UND Desktop
3. **🔐 REGEL 3**: NIEMALS API Keys, Secrets oder Credentials in Git committen

**Keine Ausnahmen ohne explizite Genehmigung!**

---

**Dokument-Status**: ✅ Aktiv und verbindlich  
**Version**: 2.0 (17. Januar 2026 - Security Regel hinzugefügt)  
**Nächste Review**: 17. Februar 2026
