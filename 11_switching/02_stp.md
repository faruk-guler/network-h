# 🌳 STP (Spanning Tree Protocol) — Döngü Engelleyici

## STP Nedir?

Ethernet ağlarında **sonsuz döngüleri (loop)** engellemek için geliştirilmiş Layer 2 protokolüdür.  
**Standart:** IEEE 802.1D

> 💡 **Benzetme:** Bir şehirde iki farklı yoldan aynı kavşağa ulaşılabiliyorsa ve trafik ışıkları yoksa araçlar sonsuza kadar dönebilir. STP, ikinci yolu geçici olarak kapatarak döngüyü kırar — ama o yol tamamen silinmez, arıza anında otomatik açılır.

---

## Neden Döngü Tehlikelidir?

Bir ağda yedekli switch bağlantıları olduğunda (ki yedeklilik iyi bir şeydir), yanlış yapılandırılmışsa şu felaket zinciri başlar:

```
Switch-A ──── Switch-B
    └──────────────┘   ← İkinci bağlantı (yedek)

Bir broadcast frame gelir:
  Switch-A → Switch-B'ye gönderir
  Switch-B → Switch-A'ya gönderir (geri döner!)
  Switch-A → Switch-B'ye tekrar gönderir...
  ♾️ Sonsuz döngü → Ağ çöker (Broadcast Storm)
```

STP bu durumu engellemek için yedek portlardan birini **bloke eder**; ağ çalışırken o port pasif bekler.

---

## STP Nasıl Çalışır?

### Adım 1: Root Bridge Seçimi

STP, tüm ağ için tek bir referans noktası seçer: **Root Bridge**.

- En düşük **Bridge ID**'ye sahip switch seçilir.
- Bridge ID = **Priority (0–65535)** + **MAC Adresi**
- Varsayılan priority: **32768**

```
Switch-A: Priority 32768, MAC: 00:AA:AA:AA:AA:01  →  Bridge ID: 32768.00AAAAAA0001
Switch-B: Priority 32768, MAC: 00:BB:BB:BB:BB:02  →  Bridge ID: 32768.00BBBBBBBB02

✅ Switch-A kazanır (MAC adresi daha küçük)
```

> 💡 Root Bridge'i **elle belirlemek** iyi bir uygulamadır. Aksi hâlde MAC adresi en küçük olan switch seçilir — bu en güçlü switch olmayabilir.

### Adım 2: Port Rolleri

| Port Rolü | Açıklama |
|:---|:---|
| **Root Port (RP)** | Root Bridge'e en kısa yolu olan port. Her switch'te 1 tane bulunur. |
| **Designated Port (DP)** | Her segmentte trafiği ileten port. Root Bridge'in tüm portları Designated'dır. |
| **Blocked Port** | Döngüyü kırmak için pasif beklemeye alınan port. Veri iletmez, sadece BPDU dinler. |

### Adım 3: Port Durumları (States)

```
Blocking → Listening → Learning → Forwarding
  (15 sn)     (15 sn)
```

| Durum | Süre | Ne Yapar? |
|:---|:---|:---|
| **Blocking** | Süresiz | BPDU dinler, veri iletmez |
| **Listening** | 15 sn | BPDU gönderir/alır, topolojiyi öğrenir |
| **Learning** | 15 sn | MAC adreslerini öğrenir, veri iletmez |
| **Forwarding** | Süresiz | Normal çalışma, veri iletir |
| **Disabled** | — | Port kapalı |

> ⚠️ Bir port Blocking'den Forwarding'e geçmesi **30–50 saniye** sürer. Bu nedenle modern ağlarda daha hızlı olan **RSTP** tercih edilir.

---

## STP'den RSTP'ye

Klasik STP (IEEE 802.1D) güvenlidir ama yavaştır: yedek bir yol devreye girdiğinde ağın oturması **30–50 saniye** sürer. Yerine geçen **RSTP (IEEE 802.1w)** aynı işi **1–6 saniyede** yapar ve bugün yeni kurulumların fiili standardıdır. (VLAN başına ayrı ağaç gibi kurumsal varyasyonları ileri düzey konudur.)

---

## Özet

```
Sorun    : Yedekli switch bağlantıları → Broadcast Storm → Ağ çöker
Çözüm    : STP yedek portları bloke eder, döngüyü kırar
Mekanizma: Root Bridge seç → Port rollerini belirle → Gerekli portları kapat
Günceli  : RSTP (çok daha hızlı yakınsama)
```
