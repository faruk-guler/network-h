# 🔀 Switch (Anahtar) Nasıl Çalışır?

Switch, **Layer 2 (Veri Bağlantı Katmanı)** cihazıdır. Ağdaki cihazları birbirine bağlar ve gelen frame'i **yalnızca doğru porta** iletir — hub gibi herkese değil.

> 💡 **Benzetme:** Hub bir megafondur; konuştuğunu herkes duyar. Switch ise akıllı bir postacıdır; mektubu yalnızca doğru adrese götürür.

---

## 1. MAC Adres Tablosu (CAM Tablosu)

Switch'in tüm zekası **MAC Address Table** (CAM — Content Addressable Memory) adı verilen bir tabloya dayanır. Bu tablo, hangi MAC adresinin hangi portta olduğunu tutar.

```
Port | MAC Adresi         | VLAN
-----|--------------------|-----
Fa0/1| AA:BB:CC:DD:EE:01  |  1
Fa0/2| AA:BB:CC:DD:EE:02  |  1
Fa0/3| AA:BB:CC:DD:EE:03  |  1
```

---

## 2. Switch Nasıl Öğrenir? — Dinamik Öğrenme

Switch, MAC adreslerini **kendiliğinden öğrenir**; elle girilmez.

```
Adım 1 — ÖĞRENME (Learning):
  PC-A (AA:...:01), Fa0/1 portundan bir frame gönderir.
  Switch: "Bu port'tan AA:...:01 geliyor" → tabloya yazar.

Adım 2 — İLETME (Forwarding):
  Frame'in hedefi AA:...:02 → tablo'da Fa0/2'de kayıtlı → oraya gönderir.

Adım 3 — YAYIN (Flooding):
  Hedef MAC tablo'da yoksa → tüm portlara gönderilir (flooding).
  Doğru cihaz cevap verince → MAC öğrenilir, tablo güncellenir.
```

> ⚠️ **Aging (Eskime):** Tablodaki kayıtlar varsayılan olarak **300 saniye** sonra silinir. Cihaz sessiz kalırsa öğrenme tekrar başlar.

---

## 3. Frame Forwarding Modları

Switch gelen frame'i nasıl ilettiğine göre üç mod vardır:

| Mod | Nasıl Çalışır | Gecikme | Hata Kontrolü |
|:---|:---|:---:|:---:|
| **Store-and-Forward** | Frame'in tamamını alır, FCS hatasını kontrol eder, sonra iletir | Yüksek | ✅ Var |
| **Cut-Through** | Hedef MAC'i okur okumaz (ilk 6 byte) iletmeye başlar | Çok düşük | ❌ Yok |
| **Fragment-Free** | İlk 64 byte'ı okur, sonra iletir (çarpışma tespiti yeter) | Orta | Kısmi |

> 💡 Kurumsal switch'lerin büyük çoğunluğu **Store-and-Forward** kullanır: güvenilirlik hızdan önce gelir.

---

## 4. Collision Domain ve Broadcast Domain

Switch kullanımının ağa kattığı en büyük değer budur:

| | Hub | Switch |
|:---|:---:|:---:|
| **Collision Domain** | Tüm portlar tek domain | Her port ayrı domain ✅ |
| **Broadcast Domain** | Tek domain | Tek domain (VLAN olmadan) |

- Switch, her portu ayrı bir **Collision Domain** yapar → çarpışma olmaz.
- Broadcast Domain'i bölmek için **VLAN** veya **Router** gerekir.

---

## 5. Unicast, Multicast, Broadcast — Switch'in Davranışı

| Frame Türü | Switch Ne Yapar? |
|:---|:---|
| **Unicast (bilinen)** | Yalnızca ilgili porta iletir |
| **Unicast (bilinmeyen)** | Tüm portlara flood eder |
| **Broadcast** | Tüm portlara iletir (FF:FF:FF:FF:FF:FF) |
| **Multicast** | Yapılandırmaya göre flood veya filtreler |

---

## Özet

```
Cihaz      Çalıştığı Katman   Zeka      Collision Domain   Broadcast Domain
─────────────────────────────────────────────────────────────────────────────
Hub        Layer 1 (Fiziksel) Yok       Tek                Tek
Switch     Layer 2 (Data Link) MAC Tablo Her port ayrı      Tek (VLAN'sız)
Router     Layer 3 (Ağ)       IP Tablo  Her port ayrı      Her port ayrı
```
