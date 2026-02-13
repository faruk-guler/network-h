# 02 - Fiziksel Bağlantı: Kablolama ve İletim Ortamı

Ağ iletişiminin **en temel katmanı** fiziksel bağlantıdır. Veriler sonuçta elektrik sinyalleri, ışık darbeleri veya radyo dalgaları olarak taşınır.

> 💡 **Benzetme:** Fiziksel katman, şehirleri birbirine bağlayan **asfalt yollar** gibidir. Yol kalitesi ne kadar iyi olursa, trafik o kadar hızlı akar.

---

## 🔌 Kablolu Bağlantılar

### 1. Bakır Kablolar (Twisted Pair / UTP-STP)

En yaygın ağ kablolarıdır. İçlerinde bükümlü çift teller bulunur.

#### UTP vs STP

| Tür | Açıklama | Korumalı mı? | Kullanım |
| :--- | :--- | :--- | :--- |
| **UTP** | Unshielded Twisted Pair | ❌ Korumasız | Ofis, ev ağları |
| **STP** | Shielded Twisted Pair | ✅ Korumalı | Endüstriyel ortamlar |

#### Kablo Kategorileri

| Kategori | Hız | Bant Genişliği | Mesafe | Kullanım |
| :--- | :--- | :--- | :--- | :--- |
| **Cat5** | 100 Mbps | 100 MHz | 100m | Eski ağlar |
| **Cat5e** | 1 Gbps | 100 MHz | 100m | Yaygın kullanım |
| **Cat6**| 1 Gbps | 250 MHz | 100m | Ofis ağları |
| **Cat6a** | 10 Gbps | 500 MHz | 100m | Veri merkezleri |
| **Cat7** | 10 Gbps | 600 MHz | 100m | Profesyonel |
| **Cat8** | 25-40 Gbps | 2000 MHz | 30m | Veri merkezi switch |

> 💡 **Tavsiye:** Yeni kurulumlar için minimum **Cat6** kullanın.

#### RJ45 Konnektör ve Renk Sırası

**T568B Standardı (En yaygın):**

| Pin | Renk | Sinyal |
| :--- | :--- | :--- |
| 1 | 🟠 Turuncu-Beyaz | TX+ |
| 2 | 🟠 Turuncu | TX- |
| 3 | 🟢 Yeşil-Beyaz | RX+ |
| 4 | 🔵 Mavi | — |
| 5 | 🔵 Mavi-Beyaz | — |
| 6 | 🟢 Yeşil | RX- |
| 7 | 🟤 Kahverengi-Beyaz | — |
| 8 | 🟤 Kahverengi | — |

#### Kablo Tipleri

| Tip | Kullanım | Açıklama |
| :--- | :--- | :--- |
| **Düz (Straight)** | PC → Switch, Switch → Router | Her iki uç aynı sıra (T568B ↔ T568B) |
| **Çapraz (Crossover)** | PC ↔ PC, Switch ↔ Switch | Bir uç T568A, diğeri T568B |
| **Rollover (Console)** | PC → Router/Switch (konsol) | Yönetim erişimi için |

> 💡 **Not:** Modern cihazlar **Auto-MDI/X** özelliğiyle kablo tipini otomatik algılar.

---

### 2. Fiber Optik Kablolar

Veriyi **ışık** olarak taşır. Elektromanyetik girişimden etkilenmez!

| Tür | Çekirdek | Mesafe | Hız | Kullanım |
| :--- | :--- | :--- | :--- | :--- |
| **Single-Mode (SM)** | 9 µm | 100+ km | 100 Gbps+ | ISP, WAN |
| **Multi-Mode (MM)** | 50/62.5 µm | 300m-2km | 10-100 Gbps | Veri merkezi, LAN |

**Avantajları:**

- 🚀 Çok yüksek hız
- 📏 Uzun mesafe
- 🛡️ Elektromanyetik parazite dayanıklı
- 🔒 Dinlemeye karşı güvenli

**Dezavantajları:**

- 💰 Daha pahalı
- 🔧 Kurulumu zor (hassas)
- ⚠️ Bükülmeye dayanıksız

---

### 3. Koaksiyel Kablo (Eski)

- **Kullanım:** Eski Ethernet (10Base2, 10Base5), kablolu TV
- **Durum:** Ağ kullanımında artık kullanılmıyor, kablolu TV'de hala aktif

---

## 📡 Kablosuz Bağlantılar

### Wi-Fi (802.11 Standartları)

| Standart | Adı | Bant Genişliği | Hız (Teorik) |
| :--- | :--- | :--- | :--- |
| **802.11n** | Wi-Fi 4 | 2.4 GHz / 5 GHz | 600 Mbps |
| **802.11ac** | Wi-Fi 5 | 5 GHz | 3.5 Gbps |
| **802.11ax** | Wi-Fi 6 / 6E | 2.4 / 5 / 6 GHz | 9.6 Gbps |
| **802.11be** | Wi-Fi 7 | 2.4 / 5 / 6 GHz | 46 Gbps |

#### 2.4 GHz vs 5 GHz

| Özellik | 2.4 GHz | 5 GHz |
| :--- | :--- | :--- |
| **Menzil** | Uzun | Kısa |
| **Hız** | Düşük | Yüksek |
| **Duvar geçişi** | İyi | Zayıf |
| **Kalabalık** | Çok (mikrodalgalar, bluetooth) | Az |

### Bluetooth

- **Menzil:** 1-100 metre (sınıfına göre)
- **Kullanım:** Kulaklık, klavye, mouse, dosya transferi
- **Hız:** 1-3 Mbps

### Hücresel (Mobil) Ağlar

| Nesil | Hız | Özellik |
| :--- | :--- | :--- |
| **3G** | 2-20 Mbps | Temel internet |
| **4G/LTE** | 50-300 Mbps | HD video akışı |
| **5G** | 1-10 Gbps | Ultra düşük gecikme, IoT |

---

## 📏 Bağlantı Ortamı Karşılaştırma

| Özellik | UTP | Fiber | Wi-Fi |
| :--- | :--- | :--- | :--- |
| **Hız** | 1-10 Gbps | 100+ Gbps | 0.6-9.6 Gbps |
| **Mesafe** | 100m | 100+ km | 30-100m |
| **Maliyet** | Düşük | Yüksek | Orta |
| **Kurulum** | Kolay | Zor | Çok kolay |
| **Güvenlik** | Orta | Yüksek | Düşük (şifreleme gerekir) |
| **Parazit** | Etkilenir | Etkilenmez | Çok etkilenir |

---

## 💡 Pratik İpuçları

1. **Ev ağı:** Cat5e veya Cat6 + Wi-Fi 5/6 yeterlidir
2. **Ofis ağı:** Cat6 + yönetilebilir switch + Wi-Fi 6
3. **Veri merkezi:** Cat6a veya Fiber + 10 Gbps switch
4. **Uzun mesafe:** Mutlaka Fiber optik kullanın
5. **Kablo testi:** Kurulumdan sonra her kabloyu **kablo tester** ile test edin

---

**Navigasyon:**

- [⬅️ Önceki: OSI ve TCP/IP Modelleri](./01-Temel-Kavramlar-OSI-ve-TCPIP-Modelleri.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: MAC Adresi ve Switching](./03-Veri-Baglanti-Katmani-MAC-Adresi-ve-Switching.md)
