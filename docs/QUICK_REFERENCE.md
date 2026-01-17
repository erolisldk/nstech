# NSTech Website - Quick Reference Guide

🚀 **Schnellstart für Entwickler**

---

## ⚡ Schnell-Checkliste vor jedem Commit

```bash
# 1. Mehrsprachigkeit (30 Sekunden)
□ Deutsche Version geändert?
□ Englische Version auch geändert?
□ Kein deutscher Text in EN-Files?

# 2. Responsive (60 Sekunden)
□ F12 → Device Toolbar (Ctrl+Shift+M)
□ Mobile 375px: OK?
□ Desktop 1280px: OK?

# 3. Commit
git add .
git commit -m "..."
git push
```

---

## 📁 Projektstruktur

```
nstech/
├── index.html              # Homepage DE
├── index-en.html           # Homepage EN
├── leistungen.html         # Services DE
├── services-en.html        # Services EN (noch zu erstellen!)
├── iso-zertifizierung.html # ISO DE
├── uber-uns.html           # About DE
├── kontakt.html            # Contact DE
├── contact.html            # Contact EN
├── karriere.html           # Career DE
├── career.html             # Career EN
├── datenschutz.html        # Privacy (nur DE)
├── impressum.html          # Legal (nur DE)
├── assets/
│   └── black.png           # Logo
├── blog/
│   ├── index.html          # Blog Übersicht
│   └── *.html              # Blog Artikel
├── n8n-workflows/
│   ├── nstech-chatbot.json # n8n Workflow
│   └── README.md           # Setup-Anleitung
├── docs/
│   ├── QUALITY_RULES.md    # ⭐ Qualitätsregeln (LESEN!)
│   └── QUICK_REFERENCE.md  # Dieses Dokument
├── server.js               # Express Server (Email API)
├── package.json
└── README.md
```

---

## 🎨 Design System

### Farben (Tailwind Config)

```javascript
nstech: {
  blue: '#0056b3',    // Primärfarbe
  dark: '#1a1a1a',    // Texte, Überschriften
  light: '#f4f7f6',   // Hintergründe
  accent: '#00d2d3',  // Akzente (selten verwendet)
  green: '#22c55e'    // Erfolg, Positives
}
```

### Verwendung:
```html
<button class="bg-nstech-blue text-white">Primary Button</button>
<h1 class="text-nstech-dark">Überschrift</h1>
<section class="bg-nstech-light">Heller Hintergrund</section>
```

### Typografie

```html
<!-- Überschriften -->
<h1 class="text-3xl md:text-4xl lg:text-5xl font-bold text-nstech-dark">
<h2 class="text-2xl md:text-3xl lg:text-4xl font-bold text-nstech-dark">
<h3 class="text-xl md:text-2xl font-bold text-gray-900">

<!-- Body Text -->
<p class="text-base md:text-lg text-gray-700">

<!-- Small Text -->
<span class="text-sm text-gray-600">
```

### Spacing

```html
<!-- Sections -->
<section class="py-12 md:py-16 lg:py-24">

<!-- Container -->
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

<!-- Cards -->
<div class="p-6 md:p-8 rounded-xl">
```

### Komponenten-Klassen

```html
<!-- Button Primary -->
<a class="px-8 py-4 bg-nstech-blue text-white rounded-full font-bold hover:bg-blue-700 transition">

<!-- Button Secondary -->
<a class="px-8 py-4 border-2 border-nstech-blue text-nstech-blue rounded-full font-bold hover:bg-nstech-blue hover:text-white transition">

<!-- Card -->
<div class="bg-white p-8 rounded-2xl shadow-lg border border-gray-100">

<!-- Input -->
<input class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-nstech-blue focus:border-transparent">
```

---

## 🌐 Mehrsprachigkeit - Patterns

### Dateinamen-Konvention

| Deutsch | Englisch | Beschreibung |
|---------|----------|--------------|
| `index.html` | `index-en.html` | Homepage |
| `leistungen.html` | `services-en.html` | Services |
| `uber-uns.html` | `about-en.html` | About |
| `kontakt.html` | `contact.html` | Contact |
| `karriere.html` | `career.html` | Career |

### Sprachschalter-Code

```html
<!-- In deutscher Seite -->
<div class="flex items-center space-x-2">
  <a href="leistungen.html" class="px-3 py-1.5 bg-nstech-blue text-white rounded-md">DE</a>
  <a href="services-en.html" class="px-3 py-1.5 text-gray-600 hover:bg-gray-100 rounded-md">EN</a>
</div>

<!-- In englischer Seite -->
<div class="flex items-center space-x-2">
  <a href="leistungen.html" class="px-3 py-1.5 text-gray-600 hover:bg-gray-100 rounded-md">DE</a>
  <a href="services-en.html" class="px-3 py-1.5 bg-nstech-blue text-white rounded-md">EN</a>
</div>
```

### Häufige Übersetzungen

| Deutsch | Englisch |
|---------|----------|
| Startseite | Home |
| Leistungen / QA Testing | Services / QA Testing |
| ISO-Zertifizierung | ISO Certification |
| Über Uns | About Us |
| Karriere | Career |
| Kontakt | Contact |
| Mehr erfahren | Learn More |
| Jetzt anfragen | Request Now |
| Beratungsgespräch vereinbaren | Schedule Consultation |
| Kostenlos | Free |
| Jahre Erfahrung | Years of Experience |
| Projekte | Projects |
| Zertifiziert | Certified |

---

## 📱 Responsive Breakpoints

### Tailwind Standard Breakpoints

```
Default:  0px - 639px   (Mobile)
sm:       640px+        (Large Mobile / Small Tablet)
md:       768px+        (Tablet)
lg:       1024px+       (Desktop)
xl:       1280px+       (Large Desktop)
2xl:      1536px+       (Extra Large)
```

### Häufige Patterns

```html
<!-- Grid: 1col → 2col → 3col -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

<!-- Flex Direction: Vertikal → Horizontal -->
<div class="flex flex-col md:flex-row gap-4">

<!-- Text Size: Klein → Mittel → Groß -->
<h1 class="text-2xl md:text-4xl lg:text-5xl">

<!-- Padding: Klein → Groß -->
<section class="py-12 md:py-16 lg:py-24">

<!-- Hide/Show -->
<div class="hidden md:block">Desktop only</div>
<div class="md:hidden">Mobile only</div>
```

---

## 🛠️ Entwickler-Tools

### Lokaler Development Server

```bash
# NPM Server starten (Port 3000)
npm start

# Alternative: Python Simple Server
python3 -m http.server 8000

# Alternative: Live Server (VS Code Extension)
# Rechtsklick auf HTML → "Open with Live Server"
```

### Browser DevTools Shortcuts

```
F12              : DevTools öffnen
Ctrl+Shift+M     : Device Toolbar (Responsive)
Ctrl+Shift+C     : Element Picker
Ctrl+R           : Reload
Ctrl+Shift+R     : Hard Reload (Cache leeren)
```

### Lighthouse Performance Test

```bash
# Im Browser (Chrome)
F12 → Lighthouse Tab → "Generate Report"

# CLI
npx lighthouse https://nstech.de --view
```

### Git Workflow

```bash
# Status prüfen
git status

# Änderungen stagen
git add .

# Commit mit Quality-Check Message
git commit -m "feat: Add feature X

✅ DE/EN both updated
✅ Responsive tested (375px, 1280px)
"

# Push
git push origin main
```

---

## 📧 Email System (Resend API)

### API Endpoints

```javascript
// Newsletter Subscribe
POST /api/newsletter
Body: { email: "user@example.com" }

// Contact Form
POST /api/send-email
Body: {
  name: "Max Mustermann",
  email: "max@example.com",
  company: "Firma GmbH",
  message: "Ich interessiere mich für..."
}
```

### Testing

```bash
# Server starten
npm start

# Test mit curl
curl -X POST http://localhost:3000/api/send-email \
  -H "Content-Type: application/json" \
  -d '{"name":"Test","email":"test@test.de","message":"Test"}'
```

---

## 🤖 Chatbot (n8n)

### Setup-Schritte (Ultra-Kurz)

1. Importiere `n8n-workflows/nstech-chatbot.json` in n8n
2. Hole Gemini API Key von [Google AI Studio](https://aistudio.google.com/app/apikey)
3. Configure im "Gemini AI Model" Node
4. Aktiviere Workflow
5. Kopiere Webhook-URL
6. Binde in Website ein (siehe `n8n-workflows/README.md`)

### Integration Code (Minimal)

```html
<!-- Vor </body> einfügen -->
<script>
  window.addEventListener('load', () => {
    const chatBtn = document.createElement('button');
    chatBtn.innerHTML = '💬';
    chatBtn.style.cssText = 'position:fixed;bottom:20px;right:20px;width:60px;height:60px;border-radius:50%;background:#0056b3;color:white;border:none;font-size:24px;cursor:pointer;z-index:9999;box-shadow:0 4px 12px rgba(0,86,179,0.4)';
    
    chatBtn.onclick = () => {
      window.open('https://YOUR-N8N-URL/webhook/nstech-website-chat', '_blank', 'width=400,height=600');
    };
    
    document.body.appendChild(chatBtn);
  });
</script>
```

---

## 🐛 Häufige Probleme & Lösungen

### Problem: "Horizontal Scroll auf Mobile"

**Ursache**: Element breiter als Viewport

**Lösung**:
```html
<!-- ❌ FALSCH -->
<div style="width: 1200px">

<!-- ✅ RICHTIG -->
<div class="max-w-7xl mx-auto px-4">
```

### Problem: "Navigation funktioniert nicht auf Mobile"

**Ursache**: JavaScript für Hamburger-Menü fehlt

**Lösung**:
```html
<script>
function toggleMobileMenu() {
  const menu = document.getElementById('mobile-menu');
  menu.classList.toggle('hidden');
}
</script>
```

### Problem: "Texte abgeschnitten"

**Ursache**: Feste Höhen oder overflow:hidden

**Lösung**:
```html
<!-- ❌ FALSCH -->
<div style="height: 200px; overflow: hidden">

<!-- ✅ RICHTIG -->
<div class="min-h-[200px]">
```

### Problem: "Bilder verzerrt"

**Lösung**:
```html
<!-- ✅ Immer verwenden -->
<img src="..." class="w-full h-auto object-cover" alt="...">
```

---

## 📊 Performance Targets

### Lighthouse Scores (Minimum)

- Performance: **90+**
- Accessibility: **95+**
- Best Practices: **95+**
- SEO: **100**

### Optimierungen

```html
<!-- Lazy Loading für Bilder -->
<img src="..." loading="lazy">

<!-- Preconnect zu externen Ressourcen -->
<link rel="preconnect" href="https://fonts.googleapis.com">

<!-- Defer für JavaScript -->
<script src="..." defer></script>
```

---

## ✅ Pre-Deployment Checkliste

```bash
□ Code funktioniert lokal
□ DE + EN beide aktualisiert
□ Responsive getestet (Mobile + Desktop)
□ Keine Console Errors
□ Lighthouse Score > 90
□ Git commit mit sinnvoller Message
□ Quality Rules befolgt
□ README aktualisiert (falls nötig)

→ READY TO DEPLOY ✅
```

---

## 🆘 Support & Ressourcen

### Dokumentation
- **Quality Rules**: [docs/QUALITY_RULES.md](./QUALITY_RULES.md) 📖
- **n8n Chatbot**: [n8n-workflows/README.md](../n8n-workflows/README.md) 🤖
- **Tailwind Docs**: https://tailwindcss.com/docs
- **Resend API**: https://resend.com/docs

### Kontakt
- **Dev Team**: dev@nstech.de
- **Content**: erol@nstech.de
- **Support**: info@nstech.de

---

**Version**: 1.0  
**Letztes Update**: 17. Januar 2025  
**Maintainer**: NSTech Dev Team

---

💡 **Pro-Tipp**: Drucke diese Seite aus oder speichere als Bookmark für schnellen Zugriff!
