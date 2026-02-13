# 03 - Veri Bağlantı Katmanı: MAC Adresi ve Switching

Veri Bağlantı Katmanı (OSI Layer 2), **aynı ağ** içindeki cihazlar arasındaki iletişimi sağlar. Bu katmanın iki kahramanı vardır: **MAC Adresi** ve **Switch**.

> 💡 **Benzetme:** IP adresi şehir adresi, MAC adresi ise **TC kimlik numarası** gibidir. IP değişebilir ama MAC (genellikle) sabittir.

---

## 🆔 MAC Adresi (Media Access Control)

### MAC Adresi Nedir?

Her ağ kartının (NIC) fabrikada atanan **benzersiz fiziksel adresidir**.

- **Uzunluk:** 48 bit (6 byte)
- **Format:** `AA:BB:CC:DD:EE:FF` veya `AA-BB-CC-DD-EE-FF`
- **Hexadecimal:** 0-9 ve A-F karakterleri kullanılır

### Yapısı

```text
AA:BB:CC:DD:EE:FF
└──────┘ └──────┘
 OUI       NIC
(Üretici)  (Benzersiz)
```

| Bölüm | Bit | Açıklama |
| :--- | :--- | :--- |
| **OUI** (İlk 3 byte) | 24 bit | Üretici kodu (IEEE tarafından atanır) |
| **NIC** (Son 3 byte) | 24 bit | Cihaza özel benzersiz numara |

### Bilinen OUI Örnekleri

| OUI | Üretici |
| :--- | :--- |
| `00:1A:2B` | Ayrix Communications |
| `00:50:56` | VMware |
| `DC:A6:32` | Raspberry Pi |
| `F4:5C:89` | Apple |
| `00:0C:29` | VMware Virtual NIC |

### Özel MAC Adresleri

| Adres | Anlamı |
| :--- | :--- |
| `FF:FF:FF:FF:FF:FF` | **Broadcast** (tüm cihazlara) |
| `01:00:5E:xx:xx:xx` | **Multicast** (gruba) |

### MAC Adresini Görme

```bash
# Windows
ipconfig /all           # "Physical Address" satırı
getmac                  # Sadece MAC

# Linux
ip link show            # "link/ether" satırı
ifconfig                # "ether" satırı

# Mac
ifconfig en0            # "ether" satırı
```

---

## 🔀 Switch (Anahtarlayıcı)

### Switch Nedir?

Switch, aynı ağdaki cihazları birbirine bağlayan **Layer 2** cihazdır. Verileri **MAC adresine** göre doğru porta yönlendirir.

### Hub vs Switch

| Özellik | Hub | Switch |
| :--- | :--- | :--- |
| **Çalışma** | Gelen veriyi **tüm portlara** gönderir | Sadece **hedef porta** gönderir |
| **Akıllılık** | Aptal (Layer 1) | Akıllı (Layer 2) |
| **Çarpışma** | Collision domain paylaşılır | Her port ayrı collision domain |
| **Performans** | Düşük | Yüksek |
| **Kullanım** | Eski, artık kullanılmıyor | Modern ağların temel taşı |

> 💡 **Hub = Hoparlör** (herkese bağırır), **Switch = Telefon** (sadece aranan kişiyle konuşur)

---

## 📢 Çarpışma ve Yayın Alanları (Domains)

### 1. Collision Domain (Çarpışma Alanı)

Veri paketlerinin birbiriyle çarpışabileceği alandır.

- **Hub:** Tüm portlar **tek bir** collision domain'dir. İki kişi aynı anda konuşursa veri bozulur.
- **Switch:** Her port **ayrı bir** collision domain'dir. Herkes aynı anda hatası konuşabilir.

### 2. Broadcast Domain (Yayın Alanı)

Bir cihaz broadcast (`FF:FF:FF:FF:FF:FF`) gönderdiğinde, bu mesajın ulaştığı tüm cihazlar grubudur.

- **Switch:** Broadcast'i tüm portlara yayar (Flooding). Yani bir Switch'e bağlı tüm cihazlar aynı broadcast domain'dedir.
- **VLAN:** Bir switch'i sanal olarak bölerek broadcast domain'leri ayırabilir (Bkz: Bölüm 07).
- **Router:** Broadcast'i **geçirmez!** Router her zaman broadcast domain'i sonlandırır.

> 💡 **Özet:**
>
> - Switch, **Collision Domain**'leri ayırır.
> - Router (veya VLAN), **Broadcast Domain**'leri ayırır.

### Switch Nasıl Çalışır?

Switch'in içinde bir **MAC Adresi Tablosu** (CAM Table) vardır:

#### Adım 1: Öğrenme (Learning)

```text
PC-A (MAC: AA:AA:AA) → Port 1'den Frame gönderir
Switch: "AA:AA:AA, Port 1'de! Tabloma yazıyorum."
```

#### Adım 2: Yönlendirme (Forwarding)

```text
Frame hedefi: BB:BB:BB
Switch: "BB:BB:BB var mı tablomda? Evet, Port 3!"
Frame → Sadece Port 3'e gönderilir ✅
```

#### Adım 3: Bilinmeyen Hedef (Flooding)

```text
Frame hedefi: CC:CC:CC
Switch: "CC:CC:CC tablomda yok! Tüm portlara gönder (flood)."
CC:CC:CC cevap verince → Tabloya eklenir
```

### MAC Adresi Tablosu Örneği

| MAC Adresi | Port | Tip |
| :--- | :--- | :--- |
| AA:AA:AA:AA:AA:AA | Fa0/1 | Dynamic |
| BB:BB:BB:BB:BB:BB | Fa0/3 | Dynamic |
| CC:CC:CC:CC:CC:CC | Fa0/5 | Dynamic |

**Tabloyu Görme (Cisco):**

```text
Switch# show mac address-table
```

---

## 🔗 ARP (Address Resolution Protocol)

### ARP Nedir?

Bir cihaz, hedef IP adresini bilir ama MAC adresini bilmez. ARP, **IP → MAC** çevirisini yapar.

### ARP Nasıl Çalışır?

```text
PC-A (192.168.1.10): "192.168.1.20'nin MAC adresi ne?"

1. ARP Request (Broadcast):
   "Kim 192.168.1.20? MAC'ini bana söyle!"
   → FF:FF:FF:FF:FF:FF (Herkese gönderilir)

2. ARP Reply (Unicast):
   PC-B: "Ben 192.168.1.20'yim, MAC'im BB:BB:BB:BB:BB:BB"
   → Sadece PC-A'ya gönderilir

3. PC-A, ARP tablosuna yazar:
   192.168.1.20 → BB:BB:BB:BB:BB:BB
```

### ARP Tablosunu Görme

```bash
# Windows / Linux / Mac
arp -a

# Örnek çıktı:
# 192.168.1.1    00-1a-2b-3c-4d-5e    dynamic
# 192.168.1.20   bb-bb-bb-bb-bb-bb    dynamic
```

---

## 🏷️ Ethernet Frame Yapısı

Layer 2'de veri, **Frame** (çerçeve) olarak taşınır:

```text
┌──────────┬──────────┬──────┬──────────┬──────┬─────┐
│ Preamble │ Dest MAC │ Src  │ EtherType│ Data │ FCS │
│ (8 byte) │ (6 byte) │ MAC  │ (2 byte) │      │(4b) │
│          │          │(6b)  │          │      │     │
└──────────┴──────────┴──────┴──────────┴──────┴─────┘
```

| Alan | Boyut | Açıklama |
| :--- | :--- | :--- |
| **Preamble** | 8 byte | Senkronizasyon (10101010...) |
| **Dest MAC** | 6 byte | Hedef MAC adresi |
| **Src MAC** | 6 byte | Kaynak MAC adresi |
| **EtherType** | 2 byte | Üst katman protokolü (0x0800=IPv4, 0x86DD=IPv6) |
| **Data** | 46-1500 byte | Taşınan veri (payload) |
| **FCS** | 4 byte | Hata kontrolü (CRC) |

---

## 💡 Özet

| Kavram | Açıklama |
| :--- | :--- |
| **MAC Adresi** | 48-bit benzersiz fiziksel adres |
| **Switch** | MAC tablosuna göre frame yönlendiren Layer 2 cihaz |
| **ARP** | IP → MAC çevirisi yapan protokol |
| **Frame** | Layer 2'nin veri birimi (PDU) |
| **Broadcast** | FF:FF:FF:FF:FF:FF → Herkese gönder |

---

**Navigasyon:**

- [⬅️ Önceki: Fiziksel Bağlantı](./02-Fiziksel-Baglanti-Kablolama-ve-Medya.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: IP Adresleme ve CIDR](./04-IP-Adresleme-ve-Subnetting-IP-Adresi-ve-CIDR.md)
