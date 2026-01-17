# NSTech AI Chatbot - n8n Workflow

Einfacher AI-gestützter Chatbot für die NSTech Website, der Fragen zu QA Testing und ISO-Zertifizierung beantwortet.

## 🎯 Funktionen

- Beantwortet Fragen zu NSTech Services (QA Testing, ISO-Zertifizierung)
- Mehrsprachig (Deutsch/Englisch)
- Conversation Memory für kontextbezogene Antworten
- ISTQB und ISO-Expertise eingebaut
- Professionelle, DSGVO-konforme Kommunikation

## 📋 Voraussetzungen

1. **n8n Installation**: 
   - Cloud: [n8n.cloud](https://n8n.cloud) (empfohlen für Anfänger)
   - Self-hosted: [Installation Guide](https://docs.n8n.io/hosting/)

2. **Google Gemini API Key**:
   - Kostenlos verfügbar bei [Google AI Studio](https://aistudio.google.com/app/apikey)
   - Klicken Sie auf "Create API key in new project"

## 🚀 Installation

### Schritt 1: Workflow importieren

1. Öffnen Sie n8n
2. Klicken Sie auf **Workflows → Import from File**
3. Wählen Sie `nstech-chatbot.json`
4. Workflow wird geladen

### Schritt 2: Gemini API konfigurieren

1. Öffnen Sie den Node **"Gemini AI Model"**
2. Klicken Sie auf **Credential → Create New**
3. Geben Sie Ihren Google Gemini API Key ein
4. Klicken Sie auf **Save**

### Schritt 3: Testen

1. Klicken Sie oben rechts auf **🗨 Open chat**
2. Testen Sie mit Fragen wie:
   - "Was bietet NSTech an?"
   - "Wie kann ich ISO 9001 Zertifizierung erhalten?"
   - "Welche Test-Automatisierung Tools nutzt ihr?"
   - "Kosten für QA Beratung?"

### Schritt 4: Aktivieren

1. Toggle oben rechts auf **Active** setzen
2. Workflow ist nun live!

## 🌐 Website-Integration

### Option 1: iFrame Einbindung

```html
<!-- In Ihre HTML-Seite einfügen -->
<iframe 
  src="https://YOUR-N8N-INSTANCE.com/webhook/nstech-website-chat"
  width="100%" 
  height="600" 
  style="border: none; border-radius: 12px;">
</iframe>
```

### Option 2: Chat-Widget (empfohlen)

Fügen Sie diesen Code in Ihre Website ein (z.B. vor `</body>`):

```html
<!-- NSTech AI Chat Widget -->
<div id="nstech-chat-widget">
  <button id="chat-toggle" style="
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    border-radius: 30px;
    background: linear-gradient(135deg, #0056b3 0%, #003d82 100%);
    border: none;
    color: white;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 12px rgba(0,86,179,0.4);
    z-index: 9999;
  ">
    💬
  </button>
  
  <div id="chat-container" style="
    position: fixed;
    bottom: 90px;
    right: 20px;
    width: 380px;
    height: 600px;
    border-radius: 12px;
    box-shadow: 0 8px 24px rgba(0,0,0,0.2);
    display: none;
    z-index: 9998;
  ">
    <iframe 
      src="https://YOUR-N8N-INSTANCE.com/webhook/nstech-website-chat"
      width="100%" 
      height="100%" 
      style="border: none; border-radius: 12px;">
    </iframe>
  </div>
</div>

<script>
  const toggleBtn = document.getElementById('chat-toggle');
  const chatContainer = document.getElementById('chat-container');
  
  toggleBtn.addEventListener('click', () => {
    if (chatContainer.style.display === 'none') {
      chatContainer.style.display = 'block';
      toggleBtn.textContent = '✕';
    } else {
      chatContainer.style.display = 'none';
      toggleBtn.textContent = '💬';
    }
  });
</script>
```

**Wichtig**: Ersetzen Sie `YOUR-N8N-INSTANCE.com` mit Ihrer tatsächlichen n8n Webhook-URL!

### Option 3: Popup beim Seitenaufruf

```html
<script>
  // Zeige Chat nach 5 Sekunden automatisch
  setTimeout(() => {
    document.getElementById('chat-container').style.display = 'block';
  }, 5000);
</script>
```

## ⚙️ Anpassungen

### System Message ändern

1. Öffnen Sie den Node **"NSTech AI Agent"**
2. Bearbeiten Sie das Feld **System Message**
3. Passen Sie folgendes an:
   - Tonalität (formell/informell)
   - Verfügbare Services
   - Kontaktinformationen
   - Spezielle Anweisungen

### Temperature einstellen

- **0.0-0.3**: Sehr konsistent, faktisch (empfohlen für Business)
- **0.4-0.7**: Ausgewogene Kreativität
- **0.8-1.0**: Sehr kreativ, variabel

Aktuell: **0.3** (professionell und konsistent)

### Memory erweitern

Standard: **30 Nachrichten**

Für längere Konversationen:
1. Öffnen Sie **"Conversation Memory"** Node
2. Erhöhen Sie **Context Window Length** auf z.B. 50

### Sprache ändern

Der Chatbot antwortet automatisch in der Sprache der Frage. Für nur Deutsch:

```
Antworte IMMER auf Deutsch, unabhängig von der Sprache der Anfrage.
```

## 🔧 Erweiterte Features (Optional)

### Email-Benachrichtigung bei wichtigen Anfragen

1. Fügen Sie einen **"Send Email"** Node hinzu
2. Verbinden Sie ihn mit dem Agent
3. Konfigurieren Sie Trigger-Bedingungen (z.B. wenn "Angebot" oder "Termin" erwähnt wird)

### CRM-Integration

Speichern Sie Leads automatisch:
- Jira für Projektanfragen
- HubSpot für Marketing
- Notion für einfache Tracking

### Kalender-Integration

- Google Calendar Node für Terminvereinbarungen
- Verfügbarkeit prüfen
- Termine automatisch buchen

## 📊 Analytics & Monitoring

### Wichtige Metriken tracken:

1. **Anzahl Konversationen**: n8n Execution History
2. **Häufige Fragen**: Analysieren Sie Logs
3. **Conversion Rate**: Wie viele Chats führen zu Kontaktaufnahmen

### n8n Webhook Analytics

```javascript
// Im Workflow einen "Code" Node hinzufügen
const timestamp = new Date();
const userMessage = $input.item.json.chatInput;

// Log zu Google Sheets oder DB senden
return {
  timestamp,
  message: userMessage,
  response: $input.item.json.response
};
```

## 🔒 Sicherheit & DSGVO

### Best Practices:

1. **API Keys schützen**: Niemals im Code committen
2. **Rate Limiting**: n8n bietet eingebautes Rate Limiting
3. **Datenminimierung**: Speichern Sie nur notwendige Daten
4. **Cookie-Banner**: Informieren Sie über Chat-Nutzung
5. **Datenlöschung**: Implementieren Sie automatische Löschung nach X Tagen

### DSGVO-konforme Konfiguration:

```
Im System Message hinzufügen:

"WICHTIG: Sammle KEINE persönlichen Daten ohne explizite Einwilligung. 
Bei Kontaktanfragen weise auf das DSGVO-konforme Kontaktformular hin."
```

## 🐛 Troubleshooting

### Problem: Chatbot antwortet nicht

**Lösung**:
1. Prüfen Sie ob Workflow **Active** ist
2. Überprüfen Sie Gemini API Key
3. Schauen Sie in n8n **Executions** für Fehler

### Problem: Langsame Antworten

**Lösung**:
1. Reduzieren Sie **Context Window Length**
2. Nutzen Sie Gemini Flash statt Pro
3. Optimieren Sie System Message (kürzer = schneller)

### Problem: "Quota exceeded" Error

**Lösung**:
- Gemini Free Tier hat Limits
- Warten Sie oder upgraden Sie auf kostenpflichtigen Plan
- Alternative: OpenAI, Anthropic Claude

## 💡 Tipps & Best Practices

### 1. Starten Sie einfach
- Nutzen Sie zunächst die Standard-Konfiguration
- Testen Sie ausgiebig
- Sammeln Sie Feedback

### 2. Iterativ verbessern
- Analysieren Sie häufige Fragen
- Passen Sie System Message an
- Fügen Sie FAQs hinzu

### 3. Klare Grenzen setzen
```
Bei technischen Support-Anfragen: "Für detaillierten technischen Support 
kontaktieren Sie bitte unser Team unter support@nstech.de"
```

### 4. Call-to-Actions einbauen
```
"Möchten Sie ein unverbindliches Beratungsgespräch vereinbaren? 
Besuchen Sie: https://nstech.de/kontakt"
```

## 📚 Weitere Ressourcen

- [n8n Dokumentation](https://docs.n8n.io/)
- [Gemini API Docs](https://ai.google.dev/docs)
- [LangChain Agent Guide](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)
- [Chat Trigger Docs](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.chattrigger/)

## 🆘 Support

Bei Fragen oder Problemen:
- **n8n Community**: [community.n8n.io](https://community.n8n.io)
- **NSTech Support**: info@nstech.de
- **Dokumentation**: Dieser README

## 📝 Lizenz

Dieses Workflow-Template ist frei verwendbar für NSTech Projekte.

---

**Erstellt für**: NSTech GmbH  
**Version**: 1.0  
**Letztes Update**: Januar 2025
