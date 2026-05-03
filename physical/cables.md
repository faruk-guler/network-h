# Ağ Kabloları

> Fiziksel katmanda kullanılan kablo türleri: Twisted Pair ve Fiber Optik.

---

## 1. Twisted Pair (Bükümlü Çift)

Birbirine sarılmış bakır tel çiftlerinden oluşur. Bükme işlemi elektromanyetik girişimi (EMI) azaltır. **RJ-45** konnektör kullanır, maksimum mesafesi **100 metredir.**

| Tür | Açıklama |
| :--- | :--- |
| **UTP** | Korumasız, esnek, ucuz. Ev ve ofis ağlarında yaygın. |
| **STP** | Metal korumalı, EMI'ye karşı dayanıklı. Endüstriyel ortamlarda kullanılır. |

### Kategoriler

| Kategori | Hız | Durum |
| :--- | :--- | :--- |
| Cat 3 / 4 | 10–16 Mbps | ⛔ Tarihi |
| Cat 5 | 1 Gbps | ⚠️ Eskimiş |
| Cat 5e | 1 Gbps | ✅ Temel standart |
| Cat 6 | 1 Gbps / 10 Gbps (55 m) | ✅ Önerilir |
| Cat 6A | 10 Gbps | ✅ 10G için ideal |
| Cat 7 | 10 Gbps | ✅ STP, endüstriyel |
| Cat 8 | 40 Gbps (30 m) | 🏢 Veri merkezi |

### Pinout — T568B

| Pin | Renk | Sinyal |
| :---: | :--- | :---: |
| 1 | 🟠 Turuncu-Beyaz | TX+ |
| 2 | 🟠 Turuncu | TX− |
| 3 | 🟢 Yeşil-Beyaz | RX+ |
| 4 | 🔵 Mavi | — |
| 5 | 🔵 Mavi-Beyaz | — |
| 6 | 🟢 Yeşil | RX− |
| 7 | 🟤 Kahverengi-Beyaz | — |
| 8 | 🟤 Kahverengi | — |

> **T568A'da** 1–2 yeşil, 3–6 turuncu olur. Geri kalan pinler aynıdır.

### Kablo Türleri

| Tür | Bağlantı | Kullanım |
| :--- | :--- | :--- |
| **Düz (Straight)** | T568B ↔ T568B | PC–switch, switch–router |
| **Çapraz (Crossover)** | T568A ↔ T568B | PC–PC, switch–switch |
| **Rollover (Console)** | Tamamen ters | PC → router/switch konsol portu |

> 💡 Modern cihazlarda **Auto-MDI/X** özelliği sayesinde çapraz kabloya gerek kalmaz.

---

## 2. Fiber Optik Kablolar

Veriyi **ışık darbeleri** ile taşır. EMI'den etkilenmez, çok daha uzun mesafe ve yüksek hız sunar. Işık, çekirdek ile kılıf arasındaki kırılma indisi farkıyla **tam iç yansıma** prensibiyle iletilir.

| Özellik | 🟡 Single-Mode (SMF) | 🟠 Multi-Mode (MMF) |
| :--- | :--- | :--- |
| Çekirdek çapı | ~9 µm | 50 / 62.5 µm |
| Işık kaynağı | Lazer | LED / VCSEL |
| Maks. mesafe | 10 km → yüzlerce km | ~550 m |
| Kılıf rengi | 🟡 Sarı | 🟠 Turuncu / 🔵 Aqua / 🟢 Yeşil |
| Kullanım | WAN, ISP, omurga | Bina içi, kampüs, DC rack |

### OM Sınıfları (Multi-Mode)

| Sınıf | Hız | Mesafe | Renk |
| :--- | :--- | :--- | :--- |
| OM1 | 1 Gbps | 275 m | 🟠 Turuncu |
| OM2 | 1 Gbps | 550 m | 🟠 Turuncu |
| OM3 | 10 Gbps | 300 m | 🔵 Aqua |
| OM4 | 10 Gbps | 550 m | 🔵 Aqua |
| OM5 | 100 Gbps | 150 m | 🟢 Açık Yeşil |

### Bağlantı Türleri

Fiber ışığı tek yönde taşır; iletim ve alım için **ayrı lif** gerekir.

| Tür | Lif | Kullanım |
| :--- | :---: | :--- |
| **Simplex** | 1 | Tek yönlü aktarım |
| **Duplex** | 2 | Switch–switch, sunucu bağlantıları |
| **MPO/MTP** | 12–24 | 40G/100G/400G veri merkezi |

> ⚠️ Duplex kabloda TX ve RX lifleri ters takılırsa bağlantı kurulamaz — en yaygın saha hatasıdır.

### Konnektörler

| Konnektör | Kullanım |
| :--- | :--- |
| **LC** | Veri merkezi, SFP portu — en yaygın |
| **SC** | ISP, eski kurulumlar |
| **ST** | Eski kampüs ağları |
| **MPO/MTP** | 40G/100G/400G yüksek yoğunluklu bağlantı |

### SFP Modülleri

Switch ve router'lar fiber bağlantı için **SFP yuvası** kullanır; modül seçimi mesafe ve hıza göre yapılır.

| Modül | Hız | Tipik Mesafe |
| :--- | :--- | :--- |
| SFP | 1 Gbps | 550 m – 80 km |
| SFP+ | 10 Gbps | 300 m – 80 km |
| QSFP+ | 40 Gbps | 100 m – 10 km |
| QSFP28 | 100 Gbps | 100 m – 10 km |

---

## 3. Karşılaştırma

| Özellik | Twisted Pair | Fiber Optik |
| :--- | :--- | :--- |
| İletim | Elektrik | Işık |
| Maks. hız | 40 Gbps | 100+ Gbps |
| Maks. mesafe | 100 m | 10 km+ |
| EMI direnci | ⚠️ Orta | ✅ Mükemmel |
| Maliyet | ✅ Düşük | ❌ Yüksek |
| Kurulum | ✅ Kolay | ⚠️ Özel ekipman |

---

## 4. Özet

- 🏠 **Ev / Ofis** → Cat 5e yeterli, yeni kurulumda Cat 6 veya Cat 6A tercih edin.
- ⚡ **10G veya yüksek EMI** → Cat 6A STP veya Multi-Mode Fiber.
- 🌐 **Uzun mesafe / omurga** → Single-Mode Fiber + SFP+ modül.
- 🔌 **Sonlandırma** → T568B standardını benimseyin, her iki ucu aynı yapın.
- ⚠️ **Fiber'de** APC (yeşil) ile UPC (mavi) konnektörleri birbirine takmayın.
