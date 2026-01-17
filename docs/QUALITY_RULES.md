# NSTech Website - Qualitätssicherungsregeln

Version: 1.0  
Datum: 17. Januar 2025  
Verantwortlich: NSTech Development Team

---

## 📋 Übersicht

Dieses Dokument definiert die verbindlichen Qualitätsregeln für die NSTech Website. Jede Änderung MUSS diese Regeln erfüllen, bevor sie deployed wird.

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

## 📞 Verantwortlichkeiten

- **Content (DE/EN)**: Erol Işıldak
- **Development**: NSTech Dev Team
- **QA Testing**: NSTech QA Team
- **Deployment**: DevOps Team

---

## 🎯 Zusammenfassung

### Die 2 Goldenen Regeln:

1. **🌐 REGEL 1**: Jede Änderung = Deutsch UND Englisch
2. **📱 REGEL 2**: Jede Änderung = Mobile, Tablet UND Desktop

**Keine Ausnahmen ohne explizite Genehmigung!**

---

**Dokument-Status**: ✅ Aktiv und verbindlich  
**Nächste Review**: 17. Februar 2025
