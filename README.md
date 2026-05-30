# 📡 ESP32 WiFi Scanner & Network Analyzer

<div align="center">

![ESP32](https://img.shields.io/badge/Platform-ESP32-blue?style=for-the-badge&logo=espressif)
![Arduino](https://img.shields.io/badge/Framework-Arduino-teal?style=for-the-badge&logo=arduino)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**ESP32 asosidagi portativ tarmoq tahlil qurilmasi**  
O'z WiFi tarmog'ini tarqatadi → Brauzer orqali boshqarish → Real-vaqt tarmoq skanerlash

</div>

---

## 📋 Mundarija

- [Loyiha haqida](#-loyiha-haqida)
- [Imkoniyatlar](#-imkoniyatlar)
- [Qanday ishlaydi](#-qanday-ishlaydi)
- [Kerakli komponentlar](#-kerakli-komponentlar)
- [O'rnatish](#-ornatish)
- [Foydalanish](#-foydalanish)
- [Web interfeys](#-web-interfeys)
- [Texnik tafsilotlar](#-texnik-tafsilotlar)
- [Xavfsizlik ogohlantirishlar](#️-xavfsizlik-ogohlantirishlar)
- [Muammolarni hal qilish](#-muammolarni-hal-qilish)
- [Hissa qo'shish](#-hissa-qoshish)

---

## 🔍 Loyiha haqida

Bu loyiha **ESP32** mikrokontrolleri asosida qurilgan portativ tarmoq tahlil qurilmasidir. Qurilma o'zi mustaqil Access Point (hotspot) yaratadi, siz unga ulanasiz va brauzer orqali grafik interfeyda tarmoqlarni ko'rishingiz, ularning signalini tahlil qilishingiz va tarmoq paketlarini kuzatishingiz mumkin.

> **Maqsad:** Ta'lim maqsadlarida tarmoq xavfsizligini o'rganish, WiFi muhitini tahlil qilish va tarmoq diagnostikasini olib borish.

---

## ✨ Imkoniyatlar

### 🔎 WiFi Scanner
- Atrofdagi barcha WiFi tarmoqlarini skanerlash
- SSID, BSSID (MAC manzil), signal kuchi (RSSI), kanal va shifrlash turini ko'rsatish
- Signal kuchini real-vaqtda yangilab turish
- Tarmoqlarni signal kuchi bo'yicha saralash

### 📦 Packet Sniffer (Monitor Mode)
- Havoda uchib yurgan WiFi paketlarni ushlash
- Paket turlarini (Beacon, Probe, Data, Management) tahlil qilish
- MAC manzillar statistikasini ko'rsatish
- Vaqt bo'yicha paket grafigini chizish

### 📡 Deauthentication Detektor
- Tarmoqqa yuborilayotgan deauth paketlarni aniqlash
- Potensial hujumlarni logga yozish
- Hujum qilinayotgan tarmoq va qurilmani ko'rsatish

### 🌐 Web Interfeys
- Qurilmaning o'zida joylashgan to'liq grafik boshqaruv paneli
- Mobil va desktop brauzerlar uchun moslik
- Real-vaqt ma'lumot yangilash (WebSocket orqali)
- Dark/Light tema qo'llab-quvvatlash

---

## ⚙️ Qanday ishlaydi

```
┌─────────────────────────────────────────────────────────┐
│                    ISHLASH JARAYONI                      │
│                                                          │
│  1. ESP32 yoqiladi                                       │
│         ↓                                                │
│  2. "ESP32-Scanner" nomli WiFi tarqatadi                 │
│         ↓                                                │
│  3. Telefon/Laptop ulanadi (parol: 12345678)             │
│         ↓                                                │
│  4. Brauzerga 192.168.4.1 yoziladi                       │
│         ↓                                                │
│  5. Web boshqaruv paneli ochiladi                        │
│         ↓                                                │
│  6. Scan / Sniff / Monitor buyruqlari beriladi           │
│         ↓                                                │
│  7. Natijalar real-vaqtda ekranda ko'rsatiladi           │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠 Kerakli komponentlar

### Hardware

| Komponent | Miqdor | Izoh |
|-----------|--------|------|
| ESP32 Dev Board | 1 | WROOM-32 yoki WROVER tavsiya etiladi |
| USB kabel (micro/Type-C) | 1 | Dastur yuklash va quvvat uchun |
| Li-Po batareya (ixtiyoriy) | 1 | Portativ foydalanish uchun |
| TP4056 zaryadlovchi (ixtiyoriy) | 1 | Batareya bilan ishlatsangiz |
| Kichik OLED ekran (ixtiyoriy) | 1 | 0.96" I2C SSD1306 |

### Software

| Dastur | Versiya | Link |
|--------|---------|------|
| Arduino IDE | 2.x yoki 1.8.x | [arduino.cc](https://www.arduino.cc) |
| ESP32 Board Package | ≥ 2.0.0 | Arduino Board Manager |
| ESPAsyncWebServer | Latest | Library Manager |
| AsyncTCP | Latest | Library Manager |
| ArduinoJSON | ≥ 6.x | Library Manager |

---

## 📥 O'rnatish

### 1. ESP32 Board Package qo'shish

Arduino IDE → **File → Preferences → Additional Board URLs** ga quyidagini qo'shing:

```
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
```

Keyin: **Tools → Board → Board Manager** → `esp32` qidiring → O'rnating

### 2. Kutubxonalarni o'rnatish

**Tools → Manage Libraries** bo'limiga kiring va quyidagilarni o'rnating:

```
✅ ESPAsyncWebServer
✅ AsyncTCP
✅ ArduinoJson
✅ Adafruit SSD1306 (OLED ekran ishlatilsa)
```

### 3. Kodni yuklash

```bash
# Repozitoriyni klonlash
git clone https://github.com/username/esp32-wifi-scanner.git

# Arduino IDE da ochish
cd esp32-wifi-scanner
open esp32_scanner.ino
```

### 4. Board sozlamalari

Arduino IDE da quyidagi sozlamalarni o'rnating:

| Sozlama | Qiymat |
|---------|--------|
| Board | ESP32 Dev Module |
| CPU Frequency | 240MHz |
| Flash Size | 4MB |
| Partition Scheme | Default 4MB |
| Upload Speed | 115200 |

### 5. Yuklash

Board ni USB orqali ulang → **Upload** tugmasini bosing.

---

## 📱 Foydalanish

### Birinchi marta ulash

1. ESP32 ga quvvat bering
2. Telefon yoki laptopda WiFi sozlamalarini oching
3. **`ESP32-Scanner`** tarmog'ini toping
4. Parol: **`12345678`**
5. Brauzerga **`192.168.4.1`** yozing
6. Boshqaruv paneli ochiladi ✅

### Asosiy buyruqlar

```
🔍 [SCAN]    — Atrofdagi WiFi tarmoqlarni skanerlash
📡 [SNIFF]   — Paket sniffer rejimini yoqish/o'chirish  
📊 [STATS]   — Tarmoq statistikasini ko'rish
🔄 [REFRESH] — Ma'lumotlarni yangilash
⚙️  [SETTINGS] — Qurilma sozlamalari
```

---

## 🖥 Web Interfeys

```
┌──────────────────────────────────────────────┐
│  📡 ESP32 Network Analyzer          [⚙️] [🌙] │
├──────────────────────────────────────────────┤
│                                               │
│  [ WiFi Scan ] [ Packet Sniff ] [ Deauth ]   │
│                                               │
├──────────────────────────────────────────────┤
│  # │ SSID          │ Signal │ CH │ Security  │
│  1 │ HomeNetwork   │ ████▒  │  6 │ WPA2     │
│  2 │ Neighbor_5G   │ ███▒▒  │ 36 │ WPA3     │
│  3 │ OpenWiFi      │ ██▒▒▒  │  1 │ NONE     │
│  ...                                          │
├──────────────────────────────────────────────┤
│  Packets: 1,247  │  Rate: 23/s  │  ⏱ 00:42  │
└──────────────────────────────────────────────┘
```

---

## 🔧 Texnik tafsilotlar

### Arxitektura

```
ESP32
├── Core 0: WiFi / Sniffer vazifasi
├── Core 1: Web server / WebSocket
├── SPIFFS: HTML/CSS/JS fayllar saqlash
└── RAM: Real-vaqt paket buffer
```

### API Endpointlar

| Endpoint | Metod | Tavsif |
|----------|-------|--------|
| `/` | GET | Asosiy sahifa |
| `/scan` | GET | WiFi skanerlash |
| `/sniff/start` | POST | Sniffer yoqish |
| `/sniff/stop` | POST | Sniffer o'chirish |
| `/stats` | GET | Statistika JSON |
| `/ws` | WS | WebSocket ulanish |

### WebSocket Xabarlari

```json
// Serverdan keladigan scan natijasi
{
  "type": "scan_result",
  "networks": [
    {
      "ssid": "HomeNetwork",
      "bssid": "AA:BB:CC:DD:EE:FF",
      "rssi": -65,
      "channel": 6,
      "encryption": "WPA2",
      "hidden": false
    }
  ]
}

// Serverdan keladigan paket ma'lumoti
{
  "type": "packet",
  "src_mac": "11:22:33:44:55:66",
  "dst_mac": "FF:FF:FF:FF:FF:FF",
  "packet_type": "Beacon",
  "ssid": "SomeNetwork",
  "channel": 11,
  "rssi": -72
}
```

---

## ⚠️ Xavfsizlik ogohlantirishlar

> **MUHIM:** Bu qurilma faqat **ta'lim va qonuniy tarmoq tahlili** maqsadida yaratilgan.

```
❌ TAQIQLANGAN:
   • Boshqalar tarmoqlariga ruxsatsiz kirish
   • Deauth hujumlari amalga oshirish
   • Paketlardan shaxsiy ma'lumot o'g'irlash
   • Qonun bilan himoyalangan tarmoqlarni buzish

✅ RUXSAT ETILGAN:
   • O'z tarmoqlaringizni tekshirish
   • Tarmoq diagnostikasi va monitoring
   • Ta'lim maqsadida laboratoriya muhitida foydalanish
   • CTF (Capture The Flag) musobaqalarida ishlatish
```

**Qonuniy mas'uliyat:** Ushbu qurilmani noto'g'ri maqsadlarda ishlatganingiz uchun to'liq javobgarlik foydalanuvchi zimmasida. Muallif hech qanday huquqiy javobgarlik olmaydi.

---

## 🐛 Muammolarni hal qilish

### ESP32 tarmoq tarqatmayapti
```
✔ USB quvvat berish yetarlimi? (≥500mA)
✔ Kodni qayta yuklang
✔ Serial Monitor da boot xabarlarini tekshiring (115200 baud)
```

### 192.168.4.1 ochilmayapti
```
✔ WiFi ga to'liq ulandingizmi?
✔ Telefonning mobil interneti o'chirilganmi?
✔ Boshqa brauzer sinab ko'ring
```

### Paketlar ko'rinmayapti
```
✔ Monitor rejimi to'g'ri ishlamoqdami? (Serial logga qarang)
✔ ESP32 antennasi yaqin tarmoqlarni ko'rmoqdami?
✔ [SNIFF] tugmasi yoqilganmi?
```

### Kompilyatsiya xatosi
```
✔ ESP32 board package versiyasi ≥ 2.0.0 ekanligini tekshiring
✔ Barcha kutubxonalar o'rnatilganmi?
✔ Board: "ESP32 Dev Module" tanlanganmi?
```

---

## 📸 Prototip rasmlari

> Rasm fayllarini `images/` papkasiga joylashtiring

```
images/
├── prototype_top.jpg      — Qurilma yuqoridan
├── prototype_side.jpg     — Yon ko'rinish
├── web_interface.png      — Web boshqaruv paneli
├── scan_result.png        — Scan natijasi
└── wiring_diagram.png     — Ulash sxemasi
```

---

## 🗺 Rivojlanish rejasi

- [x] WiFi tarmoqlarni skanerlash
- [x] Web interfeys
- [x] Paket sniffer
- [x] Deauth detektor
- [ ] OLED ekranda natijalarni ko'rsatish
- [ ] SD karta ga log yozish
- [ ] GPS bilan wardriving xarita
- [ ] Batareya holati indikatori
- [ ] MQTT orqali masofaviy monitoring
- [ ] OTA (Over-the-Air) yangilanish

---

## 🤝 Hissa qo'shish

Pull Request lar mamnuniyat bilan qabul qilinadi!

```bash
# Fork qiling
# Feature branch yarating
git checkout -b feature/yangi-imkoniyat

# O'zgarishlarni commit qiling
git commit -m "feat: yangi imkoniyat qo'shildi"

# Push qiling
git push origin feature/yangi-imkoniyat

# Pull Request oching
```

---

## 📄 Litsenziya

MIT License — batafsil [LICENSE](LICENSE) faylga qarang.

---

<div align="center">

**ESP32 bilan qurilgan ❤️**  
Savollar uchun Issue oching yoki [Telegram](https://t.me/username) orqali murojaat qiling

⭐ Yoqsa, yulduzcha bosing!

</div>
