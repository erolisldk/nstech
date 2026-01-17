# NSTech AI Chatbot - Ücretsiz Kurulum Kılavuzu

🎉 **Tamamen ücretsiz! Sadece Gemini API kullanıyor.**

---

## 🚀 Hızlı Başlangıç

### 1. Test Et (Hemen)

```bash
# chatbot.html dosyasını tarayıcıda aç
open chatbot.html
# veya
python3 -m http.server 8000
# Sonra: http://localhost:8000/chatbot.html
```

✅ Chatbot çalışıyor! Gemini API'niz zaten kodda tanımlı.

---

## 📱 Website'ye Entegre Et

### Seçenek 1: Widget (Önerilen) ⭐

Tüm sayfalarınıza ekleyin (index.html, kontakt.html, karriere.html vb.):

**`</body>` etiketinden ÖNCE ekleyin:**

```html
<!-- NSTech AI Chat Widget -->
<style>
    #nstech-chat-widget { position: fixed; z-index: 99999; }
    #nstech-chat-button {
        position: fixed; bottom: 20px; right: 20px;
        width: 60px; height: 60px; border-radius: 50%;
        background: linear-gradient(135deg, #0056b3 0%, #003d82 100%);
        border: none; color: white; font-size: 28px; cursor: pointer;
        box-shadow: 0 4px 20px rgba(0, 86, 179, 0.4);
        transition: all 0.3s ease;
        display: flex; align-items: center; justify-content: center;
    }
    #nstech-chat-button:hover { transform: scale(1.1); }
    #nstech-chat-button.active { background: linear-gradient(135deg, #dc2626 0%, #991b1b 100%); }
    #nstech-chat-iframe-container {
        position: fixed; bottom: 90px; right: 20px;
        width: 400px; height: 600px; border-radius: 20px;
        box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
        overflow: hidden; display: none; z-index: 99998;
    }
    #nstech-chat-iframe-container.active { display: block; }
    @media (max-width: 500px) {
        #nstech-chat-iframe-container {
            bottom: 0; right: 0; left: 0; top: 0;
            width: 100%; height: 100%; border-radius: 0;
        }
    }
</style>

<div id="nstech-chat-widget">
    <button id="nstech-chat-button" onclick="toggleNSTechChat()">💬</button>
    <div id="nstech-chat-iframe-container">
        <iframe src="chatbot.html" style="width:100%;height:100%;border:none;border-radius:20px;"></iframe>
    </div>
</div>

<script>
function toggleNSTechChat() {
    const btn = document.getElementById('nstech-chat-button');
    const container = document.getElementById('nstech-chat-iframe-container');
    if (container.classList.contains('active')) {
        container.classList.remove('active');
        btn.classList.remove('active');
        btn.innerHTML = '💬';
    } else {
        container.classList.add('active');
        btn.classList.add('active');
        btn.innerHTML = '✕';
    }
}
document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
        const container = document.getElementById('nstech-chat-iframe-container');
        const btn = document.getElementById('nstech-chat-button');
        if (container.classList.contains('active')) {
            container.classList.remove('active');
            btn.classList.remove('active');
            btn.innerHTML = '💬';
        }
    }
});
</script>
```

**VEYA** sadece bu satırı ekleyin:

```html
<script src="chatbot-widget.js"></script>
```

### Seçenek 2: Ayrı Sayfa

```html
<!-- Menüye link ekle -->
<a href="chatbot.html" target="_blank">
    <i class="fas fa-comments"></i> Live Chat
</a>
```

---

## 🎨 Özelleştirmeler

### 1. Chatbot Yanıtlarını Değiştir

`chatbot.html` dosyasında **SYSTEM_PROMPT** bölümünü düzenleyin:

```javascript
// Satır ~200 civarı
const SYSTEM_PROMPT = `
Du bist der offizielle AI-Assistent von NSTech GmbH...

// Buraya kendi bilgilerinizi ekleyin:
- Ek servisler
- Güncel fiyatlar
- Özel kampanyalar
- İletişim bilgileri
`;
```

### 2. Renkleri Değiştir

```css
/* Mavi yerine yeşil yapmak için: */
background: linear-gradient(135deg, #22c55e 0%, #16a34a 100%);
```

### 3. Pozisyon Değiştir

```css
/* Sağ alt yerine sol alt: */
#nstech-chat-button {
    left: 20px;  /* right: 20px; yerine */
    bottom: 20px;
}
```

### 4. Otomatik Açılma

```javascript
// 10 saniye sonra otomatik aç
setTimeout(() => {
    toggleNSTechChat();
}, 10000);
```

---

## 🔧 Gelişmiş Özellikler

### Email Bildirimi Ekle

Önemli sorularda email gönder:

```javascript
// sendMessage() fonksiyonunda ekle:
if (message.toLowerCase().includes('teklif') || message.toLowerCase().includes('fiyat')) {
    // Email gönder
    fetch('/api/send-email', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            subject: 'Chat: Teklif Talebi',
            message: `User: ${message}`
        })
    });
}
```

### Konuşma Geçmişini Kaydet

```javascript
// localStorage'a kaydet
localStorage.setItem('chatHistory', JSON.stringify(conversationHistory));

// Sayfa yüklendiğinde geri yükle
window.onload = () => {
    const saved = localStorage.getItem('chatHistory');
    if (saved) {
        conversationHistory = JSON.parse(saved);
        // Mesajları göster
    }
};
```

### Hızlı Yanıtları Güncelle

```html
<!-- chatbot.html içinde quick-replies bölümü -->
<div class="quick-reply" onclick="sendQuickReply('Yeni soru')">
    🎯 Yeni Başlık
</div>
```

---

## 📊 Maliyetler & Limitler

### Gemini API (Ücretsiz Tier)

| Özellik | Limit |
|---------|-------|
| **Günlük Request** | 1,500 / gün |
| **Dakikalık Request** | 60 / dakika |
| **Aylık Maliyet** | **$0** (Ücretsiz) |

**Hesaplama**: 
- Ortalama konuşma: 10 mesaj
- Günde 150 konuşma yapabilirsiniz (ÜCRETSİZ!)

### Limit Aşımında Ne Olur?

- 429 Error alırsınız
- Chatbot "Şu anda yoğunuz" mesajı gösterir
- Bir sonraki dakikada/günde otomatik düzelir

**Çözüm** (ihtiyaç halinde):
- Gemini API Pro (ücretli) geçin: $0.00025/request (~$7/ay 30k request için)

---

## 🐛 Sorun Giderme

### Problem: Chatbot yanıt vermiyor

**Kontrol Et**:
```javascript
// Console'da (F12) şunu çalıştır:
console.log('API Key:', GEMINI_API_KEY.substring(0, 10) + '...');
// AIzaSyA64_ görmelisiniz
```

**Çözüm**: API key doğru mu kontrol edin

---

### Problem: "API Error: 429"

**Sebep**: Günlük/dakikalık limit aşıldı

**Çözüm**:
```javascript
// Rate limiting ekle
let lastRequestTime = 0;
function sendMessage() {
    const now = Date.now();
    if (now - lastRequestTime < 2000) { // 2 saniye bekle
        alert('Lütfen biraz bekleyin...');
        return;
    }
    lastRequestTime = now;
    // ... rest of code
}
```

---

### Problem: CORS hatası

**Sebep**: Dosyayı direkt açıyorsunuz (file://)

**Çözüm**: Web server kullanın
```bash
# Python
python3 -m http.server 8000

# Node.js
npx http-server

# VS Code
# Live Server extension
```

---

## 📈 Analytics & İzleme

### Google Analytics Entegrasyonu

```javascript
// Her mesajda Google Analytics'e gönder
function addMessage(text, sender) {
    // ... existing code
    
    // GA tracking
    if (typeof gtag !== 'undefined') {
        gtag('event', 'chat_message', {
            'event_category': 'chat',
            'event_label': sender,
            'value': text.length
        });
    }
}
```

### Basit İstatistik

```javascript
// Konuşma sayısını say
let chatCount = parseInt(localStorage.getItem('nstech_chat_count') || '0');
chatCount++;
localStorage.setItem('nstech_chat_count', chatCount);

console.log(`Total chats: ${chatCount}`);
```

---

## 🔒 Güvenlik & DSGVO

### API Key Güvenliği

⚠️ **Önemli**: API key frontend'de görünür. Production için:

1. **Backend proxy oluştur** (server.js'e ekle):

```javascript
// server.js
app.post('/api/chat', async (req, res) => {
    const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${process.env.GEMINI_API_KEY}`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(req.body)
    });
    const data = await response.json();
    res.json(data);
});
```

2. **Frontend'de proxy kullan**:

```javascript
// chatbot.html
const response = await fetch('/api/chat', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(requestBody)
});
```

3. **.env'e taşı**:
```env
GEMINI_API_KEY=AIzaSyA64_I1K4dJR3Qpxo82knmOVFsUvs6Ng7A
```

### DSGVO Uyumu

```html
<!-- Cookie banner ekle -->
<div id="cookie-notice" style="position:fixed;bottom:0;left:0;right:0;background:#1a1a1a;color:white;padding:20px;text-align:center;">
    <p>Wir verwenden Cookies und AI-Chatbot. <a href="datenschutz.html" style="color:#0056b3;">Datenschutz</a></p>
    <button onclick="acceptCookies()" style="background:#0056b3;color:white;border:none;padding:10px 20px;border-radius:5px;cursor:pointer;">Akzeptieren</button>
</div>

<script>
function acceptCookies() {
    localStorage.setItem('cookies_accepted', 'true');
    document.getElementById('cookie-notice').style.display = 'none';
}
if (localStorage.getItem('cookies_accepted')) {
    document.getElementById('cookie-notice').style.display = 'none';
}
</script>
```

---

## ✅ Deployment Checklist

```bash
□ chatbot.html dosyası projeye eklendi
□ Widget kodu sayfalara eklendi (index.html, kontakt.html vb.)
□ Lokal test edildi (http://localhost:8000)
□ Mobile'da test edildi (F12 → Device Toolbar)
□ API key çalışıyor (mesaj gönder/al)
□ DSGVO cookie notice eklendi
□ (Opsiyonel) Backend proxy oluşturuldu
□ Git push yapıldı

→ CHATBOT LIVE! 🎉
```

---

## 🎯 Özet

| Özellik | Durum |
|---------|-------|
| **Maliyet** | ✅ $0 (Ücretsiz) |
| **Kurulum** | ✅ 5 dakika |
| **Bakım** | ✅ Minimal |
| **Ölçeklenebilirlik** | ✅ 1,500 konuşma/gün |
| **Özelleştirme** | ✅ Full control |
| **DSGVO** | ⚠️ Cookie notice ekle |

---

## 📞 Destek

**Sorun mu var?**
1. Console'u aç (F12) → Hataları kontrol et
2. API key'i kontrol et
3. Network tab'de request'leri incele

**Yardım**:
- Email: dev@nstech.de
- Dokümantasyon: Bu dosya

---

**Hazır!** 🚀 Chatbot'unuz tamamen ücretsiz ve çalışır durumda!
