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

## 🔗 ARP (Address Resolution Protocol)

### ARP Nedir?
RFC 826 ile tanımlanan, IP adresinden MAC adresini bulan protokoldür. Öğrenilen IP-MAC eşleşmeleri RAM'de geçici olarak saklanır. Bilgisayar kapatılınca veya süre dolunca silinir. Bu sayede aynı cihaza her veri gönderildiğinde tekrar ARP isteği yapılmaz.

> **"IP adresini biliyorum, ama kapıyı çalmak için isim lazım."**

---

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
