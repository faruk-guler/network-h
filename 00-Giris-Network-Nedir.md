# 00 - Network (Ağ) Nedir? - Dijital Dünyaya Giriş

**Network (Ağ)**, iki veya daha fazla cihazın **veri paylaşmak** için birbirine bağlandığı yapıdır. İnternet, dünyanın en büyük ağıdır!

> 💡 **Benzetme:** Network, cihazlar arasındaki "yollar ve köprüler" sistemidir. Tıpkı şehirleri birbirine bağlayan karayolları gibi.

---

## 🌐 Neden Ağlara İhtiyaç Duyarız?

### 1. 📤 Kaynak Paylaşımı

Tek bir yazıcıyı ofisteki herkes kullanabilir. Dosyalar merkezi bir sunucudan paylaşılır.

### 2. 💬 İletişim

E-posta, mesajlaşma, video konferans — hepsi ağ sayesinde mümkün.

### 3. ⚡ Hız ve Verimlilik

Flash belekle dosya taşımak yerine, ağ üzerinden **saniyeler** içinde aktarım yaparsınız.

### 4. 💰 Maliyet Tasarrufu

Her bilgisayara ayrı yazıcı, internet hattı veya depolama almak yerine **paylaşımlı** kaynaklar kullanılır.

### 5. 🔒 Merkezi Yönetim

Tüm cihazları tek merkezden yönetir, güncellersiniz. Güvenlik politikaları merkezi olarak uygulanır.

---

## 📊 Ağ Türleri

### LAN (Local Area Network) — Yerel Alan Ağı

- **Kapsam:** Tek bina veya küçük alan (ev, ofis, okul)
- **Hız:** Çok yüksek (100 Mbps - 10 Gbps)
- **Örnek:** Evinizde modem ile bağlı tüm cihazlar bir LAN oluşturur

```text
[PC] ←→ [Switch] ←→ [Yazıcı]
            ↕
         [Laptop]
```

### WAN (Wide Area Network) — Geniş Alan Ağı

- **Kapsam:** Şehirler, ülkeler, kıtalar arası
- **Hız:** LAN'dan düşük (genellikle)
- **Örnek:** İnternet, dünyanın en büyük WAN'ıdır!

```text
İstanbul Ofisi ←──── WAN ────→ Ankara Ofisi
```

### MAN (Metropolitan Area Network) — Metropoliten Ağ

- **Kapsam:** Bir şehir veya kampüs
- **Örnek:** Üniversite kampüsünü birbirine bağlayan ağ

### Diğer Ağ Türleri

| Tür | Kapsam | Örnek |
| :--- | :--- | :--- |
| **PAN** | Kişisel (1-10m) | Bluetooth kulaklık |
| **LAN** | Yerel (1 bina) | Ofis ağı |
| **MAN** | Şehir | Kampüs ağı |
| **WAN** | Ülke/Dünya | İnternet |
| **WLAN** | Kablosuz LAN | Wi-Fi ağı |

---

## 🏗️ Ağ Topolojileri (Fiziksel Yapı)

Topoloji, cihazların birbirine **nasıl bağlandığını** gösteren haritadır.

### 1. Yıldız (Star) Topolojisi

Tüm cihazlar merkezi bir cihaza (Switch/Hub) bağlıdır.

- **Durum:** Günümüzde en yaygın olanıdır.
- **Benzetme:** Bir tekerleğin telleri ve merkezi.
- **Artısı:** Bir kablo koparsa sadece o cihaz gider, diğerleri çalışmaya devam eder.

### 2. Örgü (Mesh) Topolojisi

Her cihazın diğer tüm cihazlara (veya çoğuna) doğrudan bağlı olduğu yapıdır.

- **Durum:** Kritik ağlarda (Internet omurgası) kullanılır.
- **Artısı:** En yüksek yedeklilik. Bir yol kapanırsa mutlaka başka bir yol vardır.

### 3. Otobüs (Bus) Topolojisi

Tüm cihazlar tek bir ana kabloya (omurga) bağlıdır.

- **Durum:** Çok eskidir, artık kullanılmaz.
- **Benzetme:** Tek bir koridora açılan odalar.

### 4. Halka (Ring) Topolojisi

Her cihazın iki komşusu vardır ve veri bir halka şeklinde döner.

- **Durum:** Nadir kullanılır (Token Ring).

### 5. Hibrit (Hybrid)

Yukarıdakilerin karışımı (Örn: Yıldız-Ağaç yapısı).

---

## 🖥️ Ağ Cihazları

### Switch (Anahtarlayıcı)

- **Görevi:** Aynı ağdaki cihazları birbirine bağlar
- **Katman:** Layer 2 (Data Link)
- **Benzetme:** Bir binanın iç telefon santralı

### Router (Yönlendirici)

- **Görevi:** Farklı ağları birbirine bağlar
- **Katman:** Layer 3 (Network)
- **Benzetme:** Şehirler arası kavşak polisi

### Modem

- **Görevi:** Dijital sinyali analog'a (ve tersi) çevirir
- **Kullanım:** ISP bağlantısı (ADSL, fiber, kablolu)

### Access Point (Erişim Noktası)

- **Görevi:** Kablosuz (Wi-Fi) bağlantı sağlar
- **Benzetme:** Bir odanın kablosuz vericisi

---

## 🔑 Temel Ağ Terimleri

| Terim | Açıklama |
| :--- | :--- |
| **IP Adresi** | Cihazın ağdaki kimlik numarası (Örn: 192.168.1.10) |
| **MAC Adresi** | Ağ kartının fiziksel adresi (Örn: AA:BB:CC:DD:EE:FF) |
| **Port** | Uygulamaların iletişim noktası (Örn: HTTP=80, SSH=22) |
| **Bandwidth** | Bant Genişliği - Veri taşıma kapasitesi (Örn: 100 Mbps) |
| **Latency** | Gecikme - Verinin hedefe ulaşma süresi (Ping süresi) |
| **Firewall** | Güvenlik Duvarı - Ağ trafiğini filtreleyen sistem |
| **DNS** | Alan Adı Sistemi - Domain adını IP'ye çevirir |
| **DHCP** | Dinamik Ana Makine Yapılandırma Protokolü - Otomatik IP dağıtır |

---

## 📚 Öğrenme Yolu

Bu dokümantasyonu sırasıyla takip etmeniz önerilir:

```text
00 - Network Nedir? (Buradasınız! ✅)
 ↓
01 - OSI ve TCP/IP Modelleri
 ↓
02 - Fiziksel Bağlantı (Kablolama)
 ↓
03 - MAC Adresi ve Switching
 ↓
04 - IP Adresleme ve Subnetting (⭐ En Önemli!)
 ↓
05 - Routing (Yönlendirme)
 ↓
06 - Uygulama Protokolleri (DNS, DHCP, HTTP)
 ↓
07 - VLAN Temelleri
 ↓
99 - Araçlar ve Komutlar (Pratik!)
```

---

**Navigasyon:**

- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: OSI ve TCP/IP Modelleri](./01-Temel-Kavramlar-OSI-ve-TCPIP-Modelleri.md)
