# 01 - OSI ve TCP/IP Modelleri: Ağ İletişiminin Katmanları

Bilgisayarlar birbirleriyle nasıl konuşur? Bu sorunun cevabı **katmanlı model** mimarisindedir. İki önemli model vardır: **OSI** (teorik) ve **TCP/IP** (pratik).

> 💡 **Benzetme:** OSI modeli, bir mektubun yazılması, zarflanması, adresinin yazılması ve postaya verilmesi gibi adımları tanımlar. Her katman bir göreve odaklanır.

---

## 📚 OSI Modeli (7 Katman)

OSI (Open Systems Interconnection), ağ iletişimini **7 katmana** ayıran teorik bir modeldir.

### Katmanlar (Yukarıdan Aşağıya)

| # | Katman | İngilizce | Görevi | PDU | Örnek |
|---|--------|-----------|--------|-----|-------|
| 7 | **Uygulama** | Application | Kullanıcı ile etkileşim | Data | HTTP, FTP, DNS, SMTP |
| 6 | **Sunum** | Presentation | Veri formatı, şifreleme | Data | SSL/TLS, JPEG, ASCII |
| 5 | **Oturum** | Session | Bağlantı yönetimi | Data | NetBIOS, RPC |
| 4 | **Taşıma** | Transport | Uçtan uca iletim | Segment | TCP, UDP |
| 3 | **Ağ** | Network | Yönlendirme, adresleme | Packet | IP, ICMP, ARP |
| 2 | **Veri Bağlantı** | Data Link | Yerel iletim, hata kontrolü | Frame | Ethernet, Wi-Fi, MAC |
| 1 | **Fiziksel** | Physical | Elektrik sinyali, kablolar | Bits | Kablo, Fiber, Wi-Fi sinyali |

### Hatırlamak İçin

**Yukarıdan aşağıya (7→1):**

> **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

**Aşağıdan yukarıya (1→7):**

> **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

---

### Her Katmanın Detaylı Açıklaması

#### 7. Uygulama Katmanı (Application)

Kullanıcının doğrudan etkileşimde olduğu katman.

- **Protokoller:** HTTP, HTTPS, FTP, SSH, DNS, SMTP, POP3, IMAP
- **Örnek:** Web tarayıcısında bir URL yazdığınızda

#### 6. Sunum Katmanı (Presentation)

Verinin **formatını** belirler, sıkıştırır ve şifreler.

- **Görevler:** Şifreleme (TLS/SSL), Sıkıştırma (ZIP), Format dönüşümü
- **Örnek:** HTTPS'deki SSL/TLS şifreleme

#### 5. Oturum Katmanı (Session)

İki cihaz arasındaki **oturumu** (session) açar, yönetir ve kapatır.

- **Görevler:** Bağlantı kurma, sürdürme, sonlandırma
- **Örnek:** Uzaktaki bir sunucuya oturum açma

#### 4. Taşıma Katmanı (Transport)

Veriyi **parçalara** (segment) böler ve uçtan uca güvenilir iletim sağlar.

- **TCP:** Güvenilir, sıralı, bağlantı odaklı (3-way handshake)
- **UDP:** Hızlı, güvenilir değil, bağlantısız
- **Port numaraları** bu katmanda tanımlanır

| Özellik | TCP | UDP |
|---------|-----|-----|
| Güvenilirlik | ✅ Garantili teslimat | ❌ Kaybolabilir |
| Hız | Daha yavaş | Daha hızlı |
| Bağlantı | Bağlantı odaklı | Bağlantısız |
| Kullanım | Web, e-posta, dosya | Video, ses, oyun, DNS |

#### 3. Ağ Katmanı (Network)

**IP adresleme** ve **yönlendirme** (routing) bu katmanda yapılır.

- **Cihaz:** Router
- **Protokoller:** IPv4, IPv6, ICMP, OSPF, BGP
- **PDU:** Packet (Paket)

#### 2. Veri Bağlantı Katmanı (Data Link)

**MAC adresleme** ve yerel ağ iletişimi bu katmanda yapılır.

- **Cihaz:** Switch
- **Protokoller:** Ethernet (802.3), Wi-Fi (802.11)
- **PDU:** Frame (Çerçeve)

#### 1. Fiziksel Katman (Physical)

Veriyi **elektrik sinyalleri**, ışık veya radyo dalgaları olarak taşır.

- **Cihaz:** Kablolar, Hub, Repeater
- **Ortam:** Bakır kablo, Fiber optik, Kablosuz
- **PDU:** Bits (0 ve 1'ler)

---

## 🌐 TCP/IP Modeli (4 Katman)

TCP/IP, internetin **pratik** modelidir. OSI'nin basitleştirilmiş halidir.

| # | TCP/IP Katmanı | OSI Karşılığı | Protokoller |
|---|---------------|---------------|-------------|
| 4 | **Uygulama** | 7+6+5 (Application + Presentation + Session) | HTTP, DNS, FTP, SSH, SMTP |
| 3 | **Taşıma** | 4 (Transport) | TCP, UDP |
| 2 | **İnternet** | 3 (Network) | IP, ICMP, ARP |
| 1 | **Ağ Erişimi** | 2+1 (Data Link + Physical) | Ethernet, Wi-Fi |

---

## 🔀 Veri Akışı: Kapsülleme ve Dekapsülleme

### Kapsülleme (Encapsulation) — Gönderen Taraf

Veri yukarıdan aşağıya her katmanda bir **başlık** (header) eklenerek sarılır:

```text
[Uygulama] → Data
                ↓
[Taşıma]   → TCP Header + Data = Segment
                ↓
[Ağ]       → IP Header + Segment = Packet
                ↓
[Veri Bağ] → MAC Header + Packet + Trailer = Frame
                ↓
[Fiziksel] → 01101001... (Bits)
```

### Dekapsülleme (Decapsulation) — Alıcı Taraf

Alıcı, aşağıdan yukarıya her katmanda başlıkları **soyar** ve veriye ulaşır.

---

## 🎯 Günlük Hayattan Örnek

**Web sayfası açma süreci:**

```text
1. [Uygulama]    Tarayıcı: "google.com istiyorum" (HTTP GET)
2. [Sunum]       SSL/TLS ile şifrele
3. [Oturum]      Oturum aç
4. [Taşıma]      TCP bağlantısı kur (3-way handshake), port 443
5. [Ağ]          IP adresi ekle (kaynak → hedef)
6. [Veri Bağ]    MAC adresi ekle, frame oluştur
7. [Fiziksel]    Elektrik sinyali olarak kabloya gönder
```

---

## 💡 Neden Katmanlı Model?

1. **Modülerlik:** Her katman bağımsız geliştirilir
2. **Sorun Giderme:** Sorun hangi katmanda? (Layer 1? Layer 3?)
3. **Standartlaşma:** Farklı üreticiler aynı dili konuşur
4. **Esneklik:** Bir katman değişse bile diğerleri etkilenmez

---

**Navigasyon:**

- [⬅️ Önceki: Network Nedir?](./00-Giris-Network-Nedir.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Fiziksel Bağlantı](./02-Fiziksel-Baglanti-Kablolama-ve-Medya.md)
