# 📦 IPv4 Header Yapısı

Bir IPv4 paketi iki bölümden oluşur: **Header (Başlık)** ve **Data (Veri)**. Header, paketin nasıl ve nereye iletileceğini söyleyen "zarfın üzerindeki bilgiler"dir.

> 💡 **Benzetme:** Bir kargo paketinin üzerinde; göndericinin adresi, alıcının adresi, taşıma türü ve "kırılgan" gibi özel notlar bulunur. IPv4 Header da bir paketin "kargo etiketi"dir — router'lar bu etikete bakarak paketi nereye göndereceğine karar verir.

---

## Header Yapısı (Görsel)

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├───────┬───────┬───────────────────┬───────────────────────────────┤
│Version│  IHL  │    DSCP / ToS     │         Total Length          │
├───────┴───────┴───────────────────┴───────────────────────────────┤
│          Identification           │Flags│   Fragment Offset       │
├───────────────────────────────────┼─────┴─────────────────────────┤
│      TTL      │    Protocol       │        Header Checksum        │
├───────────────┴───────────────────┴───────────────────────────────┤
│                     Source IP Address                             │
├───────────────────────────────────────────────────────────────────┤
│                   Destination IP Address                          │
├───────────────────────────────────────────────────────────────────┤
│                Options (varsa)           │      Padding           │
└───────────────────────────────────────────────────────────────────┘
```

Minimum header boyutu: **20 byte** (Options olmadan)

---

## Header Alanları — Detaylı Açıklama

### 1. Version (Sürüm) — 4 bit

IPv4 paketlerinde bu alan her zaman **`0100` (4)** değerini taşır. Router paketi aldığında bu alana bakarak "Bu bir IPv4 paketidir" der ve işleme devam eder.

> 💡 IPv6 paketlerinde bu değer `0110` (6) olur — ancak IPv6 header'ı tamamen farklı bir yapıya sahiptir ve IPv4 ile aynı alanda işlenmez.

---

### 2. IHL (Internet Header Length) — 4 bit

Header'ın 32-bitlik kelime (word) sayısı olarak uzunluğunu belirtir.

- Minimum: `0101` = 5 × 4 byte = **20 byte** (Options yok)
- Maksimum: `1111` = 15 × 4 byte = **60 byte**

> 💡 IHL neden gerekli? Çünkü Options alanı değişken uzunlukta olabilir. Router, "header nerede bitiyor, data nerede başlıyor?" sorusunu IHL'ye bakarak yanıtlar.

---

### 3. DSCP / ToS (Differentiated Services Code Point) — 8 bit

Paketin **öncelik seviyesini** ve **servis kalitesini (QoS)** belirler.

```text
Örnek:
  Sesli arama (VoIP) paketi → Yüksek öncelik (DSCP = EF)
  Normal web trafiği        → Düşük/varsayılan öncelik (DSCP = BE)
```

> 💡 Bir router aynı anda hem video konferans hem de dosya indirme trafiği alırsa, DSCP değerine bakarak video konferansı öne alır. Çünkü gecikme onu daha çok etkiler.

---

### 4. Total Length (Toplam Uzunluk) — 16 bit

Header dahil tüm paketin **byte cinsinden** toplam boyutudur.

- Minimum: 20 byte (yalnızca header, data yok)
- Maksimum: 65.535 byte

> Bu değer alıcı tarafa "kaç byte alacaksın?" bilgisini verir.

---

### 5. Identification (Kimlik) — 16 bit

Aynı orijinal paketten parçalanarak gelen **fragment'ları (parçaları)** birbirine bağlayan benzersiz numaradır.

> 💡 Büyük bir paket daha küçük parçalara (fragment) bölünürse, tüm parçalar aynı Identification numarasını taşır. Alıcı bu sayede hangi parçaların bir arada olduğunu anlar.

---

### 6. Flags (Bayraklar) — 3 bit

Paketin parçalanmasıyla ilgili kontrol bitleri:

| Bit | İsim | Anlam |
|:---:|:---|:---|
| 0 | Reserved | Her zaman 0, rezerve |
| 1 | **DF** (Don't Fragment) | `1` = "Bu paketi parçalama!" |
| 2 | **MF** (More Fragments) | `1` = "Daha fazla parça var"; `0` = "Bu son parça" |

```text
Örnek: ping -f (Windows) komutu DF bitini 1'e set eder.
Eğer paket büyükse ve router parçalayamazsa "ICMP Fragmentation Needed" mesajı döner.
→ Bu, MTU (Maximum Transmission Unit) keşfinde kullanılır.
```

---

### 7. Fragment Offset (Parça Ofseti) — 13 bit

Fragment'ın orijinal paketteki **başlangıç konumunu** 8-byte'lık birimlerle gösterir.

```text
Orijinal 4000 byte'lık paket → 3 parçaya bölünür:
  Parça 1: Offset = 0     (0. byte'tan başlar)
  Parça 2: Offset = 185   (1480. byte'tan başlar — 185 × 8 = 1480)
  Parça 3: Offset = 370   (2960. byte'tan başlar)
```

> Alıcı bu bilgiyle parçaları doğru sıraya dizer.

---

### 8. ⭐ TTL (Time to Live) — 8 bit

Paketin ağda kaç **router atlaması (hop)** yapabileceğini belirleyen sayaçtır. **Sonsuz döngüleri önlemenin en temel mekanizmasıdır.**

```text
Nasıl çalışır:
  Gönderici: TTL = 128 (Windows varsayılanı)
             TTL = 64  (Linux/macOS varsayılanı)

  Her router'da:  TTL = TTL − 1

  TTL = 0 olduğunda:
    → Router paketi düşürür (atar)
    → Gönderene "ICMP Time Exceeded" mesajı gönderir
```

**Ping çıktısında TTL okuma:**
```text
ping google.com
  64 bytes from 142.250.185.78: ttl=57

  TTL = 57 → Google 64 ile gönderdi, 7 router atlayarak geldi (64-57=7)
```

> 💡 **tracert / traceroute** komutunun çalışma prensibi de TTL'dir:
> - TTL=1 gönder → ilk router "Time Exceeded" der, kendini tanıtır
> - TTL=2 gönder → ikinci router tanıtır
> - Hedefe ulaşana kadar devam...

---

### 9. ⭐ Protocol (Protokol) — 8 bit

IP payload'ının (veri kısmının) hangi üst katman protokolünü taşıdığını söyler. Router değil, **alıcı işletim sistemi** bu alana bakarak paketi doğru servise teslim eder.

| Değer (Decimal) | Değer (Hex) | Protokol | Açıklama |
|:---:|:---:|:---|:---|
| 1 | 0x01 | **ICMP** | Ping, traceroute hata mesajları |
| 6 | 0x06 | **TCP** | HTTP, SSH, FTP vb. |
| 17 | 0x11 | **UDP** | DNS, DHCP, VoIP |
| 47 | 0x2F | **GRE** | VPN tünelleme |
| 50 | 0x32 | **ESP** | IPSec şifreli tünel |
| 89 | 0x59 | **OSPF** | Routing protokolü |

```text
Örnek: Bir web sayfası açıyorsunuz (HTTP).
  IPv4 Header → Protocol = 6 (TCP)
  Alıcı işletim sistemi: "Protocol=6, bu TCP paketi,
                          TCP stack'e ver"
```

---

### 10. Header Checksum (Başlık Sağlama Toplamı) — 16 bit

Yalnızca **header'ın** doğruluğunu kontrol eder. Data'nın hatasız gelip gelmediğini **kontrol etmez** (bu TCP/UDP'nin işi).

> ⚠️ Her router, TTL'yi 1 azaltınca header değiştiği için Checksum'ı **yeniden hesaplayarak** yazar.

> 💡 IPv6, Checksum alanını tamamen kaldırmıştır. Bu hesaplama yükü üst katmanlara (TCP/UDP) bırakılarak router performansı artırılmıştır.

---

### 11. ⭐ Source IP Address (Kaynak IP) — 32 bit

Paketi gönderen cihazın IP adresi. **4 oktet × 8 bit = 32 bit.**

```text
Örnek: 192.168.1.5
Binary: 11000000.10101000.00000001.00000101
```

---

### 12. ⭐ Destination IP Address (Hedef IP) — 32 bit

Paketin gideceği cihazın IP adresi. Router'lar yönlendirme kararını **bu alana** bakarak verir.

---

### 13. Options (Seçenekler) — değişken (0–40 byte)

Nadiren kullanılan, ağ testi ve hata ayıklama için ekstra bilgiler taşıyan isteğe bağlı alandır. Modern ağlarda genellikle boştur.

---

## Özet Tablo

| Alan | Boyut | Ne İşe Yarar? |
|:---|:---:|:---|
| **Version** | 4 bit | IPv4 mü IPv6 mı? |
| **IHL** | 4 bit | Header uzunluğu |
| **DSCP/ToS** | 8 bit | Trafik önceliği (QoS) |
| **Total Length** | 16 bit | Toplam paket boyutu |
| **Identification** | 16 bit | Fragment grubu kimliği |
| **Flags (DF/MF)** | 3 bit | Parçalanma kontrolü |
| **Fragment Offset** | 13 bit | Parçanın konumu |
| **TTL** | 8 bit | Hop sınırı, döngü önleme |
| **Protocol** | 8 bit | TCP mi UDP mi ICMP mi? |
| **Header Checksum** | 16 bit | Header bütünlüğü |
| **Source IP** | 32 bit | Gönderenin adresi |
| **Destination IP** | 32 bit | Hedefin adresi |
| **Options** | 0–40 byte | İsteğe bağlı ekstra bilgi |
| **Padding** | Değişken | Options alanını 32-bit sınırına hizalamak için eklenen sıfır bitleri |

---

## Gerçek Hayat: Wireshark ile Header Okuma

Bir paketi Wireshark'ta yakaladığınızda tam olarak bu alanları görürsünüz:

```text
Internet Protocol Version 4
  Version: 4
  Header Length: 20 bytes (5)
  Differentiated Services: 0x00
  Total Length: 60
  Identification: 0x1234
  Flags: 0x40 (Don't Fragment)
  Time to Live: 64
  Protocol: TCP (6)
  Header Checksum: 0x1a2b
  Source Address: 192.168.1.5
  Destination Address: 142.250.185.78
```

> 💡 Wireshark ile gerçek trafiği yakalayarak bu alanları canlı olarak inceleyebilirsiniz.
