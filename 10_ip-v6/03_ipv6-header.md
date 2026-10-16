# 📦 IPv6 Header Yapısı

Bir IPv6 paketinin başlığı, IPv4'e kıyasla **daha basit ve sabit boyutludur.** Bu, router'ların paketi daha hızlı işlemesini sağlar.

> 💡 **Benzetme:** IPv4 header bir "form" gibi düşünülebilir — bazı alanlar boş bırakılabilir, bazıları opsiyoneldir. IPv6 header ise herkesin doldurmak zorunda olduğu **sade ve standart bir etiket** gibidir.

---

## Header Yapısı (Görsel)

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├───────┬───────────────────┬───────────────────────────────────────┤
│Version│   Traffic Class   │             Flow Label                │
├───────┴───────────────────┴───────────────────────────────────────┤
│         Payload Length        │  Next Header  │   Hop Limit       │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│                   Source IPv6 Address (128 bit)                   │
│                                                                   │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│                Destination IPv6 Address (128 bit)                 │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

**Sabit header boyutu: 40 byte**
*(IPv4'te bu 20–60 byte arasında değişkendir)*

---

## Header Alanları — Açıklama

### 1. Version (Sürüm) — 4 bit
Her zaman `0110` (6) değerini taşır. Router bu alana bakarak "Bu IPv6 paketi" der.

---

### 2. Traffic Class (Trafik Sınıfı) — 8 bit
IPv4'teki **DSCP/ToS** alanının karşılığıdır. Paketin önceliğini belirler.

```text
VoIP paketi → Yüksek öncelik (düşük gecikme gerektirir)
E-posta     → Düşük öncelik (gecikmeye toleranslı)
```

---

### 3. Flow Label (Akış Etiketi) — 20 bit ⭐ *IPv6'ya Özgü*
Aynı uygulamaya ait paketleri etiketler (örneğin bir video aramasının tüm paketleri). Router'lar aynı etikete sahip paketlere tutarlı bir rota uygulayabilir.

> 💡 IPv4'te bu alan **yoktur.** IPv6'nın getirdiği en önemli yeniliklerden biridir.

---

### 4. Payload Length (Yük Uzunluğu) — 16 bit
Header'dan sonraki verinin byte cinsinden uzunluğudur.

> **IPv4 ile farkı:** IPv4'ün "Total Length" alanı header'ı da sayarken, IPv6 **yalnızca payload'ı** ölçer.

---

### 5. Next Header (Sonraki Başlık) — 8 bit
Payload'ın hangi üst katman protokolünü taşıdığını söyler. IPv4'ün **Protocol** alanının karşılığıdır.

| Değer | Protokol |
|:---:|:---|
| 6 | TCP |
| 17 | UDP |
| 58 | ICMPv6 |

---

### 6. Hop Limit (Atlama Sınırı) — 8 bit ⭐
IPv4'ün **TTL** alanının karşılığıdır. Her router bu değeri 1 azaltır; 0'a ulaşınca paket düşürülür.

> 💡 **İsim değişikliği anlamlı:** IPv4'te "Time to Live" (yaşam süresi) deniyordu ama aslında zamanı değil, atlamaları sayıyordu. IPv6 bunu daha doğru bir isimle **"Hop Limit"** olarak adlandırdı.

---

### 7. Source IPv6 Address — 128 bit
Paketi gönderen cihazın tam IPv6 adresi.

---

### 8. Destination IPv6 Address — 128 bit
Paketin gönderileceği cihazın tam IPv6 adresi. Router'lar yönlendirme kararını bu alana bakarak verir.

---

## IPv4 Header ile Karşılaştırma

| Özellik | IPv4 | IPv6 |
|:---|:---:|:---:|
| Header boyutu | 20–60 byte (değişken) | **40 byte (sabit)** |
| Checksum alanı | ✅ Var | ❌ **Kaldırıldı** |
| TTL / Hop sınırı | TTL | Hop Limit |
| QoS alanı | DSCP/ToS | Traffic Class |
| Akış etiketi | ❌ Yok | ✅ **Flow Label** |
| Broadcast | Var | **Yok** (Multicast kullanılır) |

> ⚠️ **Checksum neden kaldırıldı?** Her router'ın checksum hesaplaması gereksiz işlem yüküne yol açıyordu. Bu görev üst katmanlara (TCP/UDP) devredilerek **router performansı artırıldı.**

---

## Özet Tablo

| Alan | Boyut | Ne İşe Yarar? |
|:---|:---:|:---|
| **Version** | 4 bit | Her zaman 6 |
| **Traffic Class** | 8 bit | QoS önceliği (IPv4 DSCP karşılığı) |
| **Flow Label** | 20 bit | Akış tanımlama — IPv6'ya özgü |
| **Payload Length** | 16 bit | Payload boyutu (header hariç) |
| **Next Header** | 8 bit | TCP / UDP / ICMPv6 |
| **Hop Limit** | 8 bit | TTL karşılığı, döngü önleme |
| **Source IPv6** | 128 bit | Gönderenin adresi |
| **Destination IPv6** | 128 bit | Hedefin adresi |

