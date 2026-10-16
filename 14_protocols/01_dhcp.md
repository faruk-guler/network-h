# 🔄 DHCP (Dynamic Host Configuration Protocol) — Otomatik IP Dağıtımı

## DHCP Nedir?

DHCP, ağa bağlanan cihazlara **otomatik olarak** IP adresi, subnet mask, default gateway ve DNS sunucusu gibi ağ yapılandırma bilgilerini dağıtan protokoldür.

> 💡 **Benzetme:** Bir otele giriş yaptığınızda resepsiyon size oda numarası, Wi-Fi şifresi ve restoran katı bilgisini verir — siz bunları tek tek aramazsınız. DHCP de ağa bağlanan her cihaza "oda numarası" (IP adresi) ve diğer bilgileri otomatik olarak atar.

**Port:** UDP 67 (Sunucu) / UDP 68 (İstemci)

---

## DHCP Olmadan Ne Olur?

DHCP olmadan her cihaza **elle (statik)** IP atanması gerekir:

| | Statik IP (Elle) | DHCP (Otomatik) |
|---|---|---|
| **Yapılandırma** | Her cihaza tek tek girilir | Otomatik dağıtılır |
| **Hata Riski** | Yüksek (çakışma, yanlış maske) | Düşük |
| **Yönetim** | Zor (100 cihaz = 100 yapılandırma) | Kolay (tek merkezden) |
| **Kullanım** | Sunucu, yazıcı, router (sabit olması gereken cihazlar) | Bilgisayar, telefon, tablet (geçici cihazlar) |

> ⚠️ Aynı ağda iki cihaza aynı IP adresi verilirse **IP çakışması** oluşur ve her iki cihaz da iletişim kuramaz. DHCP bu riski ortadan kaldırır.

---

## DORA Süreci — DHCP Nasıl Çalışır?

Bir cihaz ağa bağlandığında IP adresi almak için 4 adımlı **DORA** sürecini başlatır:

```
Cihaz                                          DHCP Sunucusu
  │                                                  │
  │  1. DISCOVER (Keşif)                             │
  │  "Ağda DHCP sunucusu var mı?"                    │
  │  (Broadcast: 255.255.255.255)                    │
  │ ──────────────────────────────────────────────►   │
  │                                                  │
  │  2. OFFER (Teklif)                               │
  │  "Ben varım! Sana 192.168.1.50 verebilirim."     │
  │ ◄──────────────────────────────────────────────   │
  │                                                  │
  │  3. REQUEST (İstek)                              │
  │  "Tamam, 192.168.1.50'yi istiyorum."             │
  │ ──────────────────────────────────────────────►   │
  │                                                  │
  │  4. ACKNOWLEDGE (Onay)                           │
  │  "Kabul! 192.168.1.50 senin. 24 saat geçerli."   │
  │ ◄──────────────────────────────────────────────   │
  │                                                  │
  ▼  Cihaz artık ağda iletişim kurabilir             ▼
```

| Adım | Kısaltma | Yön | Açıklama |
|---|---|---|---|
| 1 | **D** — Discover | İstemci → Broadcast | Cihaz, ağdaki DHCP sunucusunu arar |
| 2 | **O** — Offer | Sunucu → İstemci | Sunucu, bir IP adresi teklif eder |
| 3 | **R** — Request | İstemci → Broadcast | Cihaz, teklif edilen IP'yi kabul eder |
| 4 | **A** — Acknowledge | Sunucu → İstemci | Sunucu, IP atamasını onaylar ve yapılandırma bilgilerini gönderir |

> 💡 **Neden Broadcast?** Cihazın henüz IP adresi yoktur, bu yüzden DHCP sunucusunun adresini de bilmez. Bu nedenle ilk iki adım **broadcast** (255.255.255.255) olarak gönderilir.

---

## DHCP Lease (Kiralama Süresi)

DHCP'nin verdiği IP **kalıcı değildir**; belirli bir süre için kiralanır — ev modemlerinde tipik olarak 24 saat. Sürenin yarısında cihaz aynı sunucudan sessizce yeniler; kimse yanıt vermezse süre sonunda adresi bırakır ve DORA baştan başlar. Kurumsal ağlarda kiralama süresi 8 saate kadar düşürülebilir.

---

## DHCP Sunucusunun Dağıttığı Bilgiler

DHCP yalnızca IP adresi dağıtmaz. Tam bir ağ yapılandırması sunar:

| Parametre | Açıklama | Örnek |
|---|---|---|
| **IP Adresi** | Cihazın ağdaki kimliği | `192.168.1.50` |
| **Subnet Mask** | Ağ ve host kısmını ayırır | `255.255.255.0` |
| **Default Gateway** | Dış ağlara çıkış kapısı | `192.168.1.1` |
| **DNS Sunucusu** | Alan adı çözümleme | `8.8.8.8` |
| **Lease Time** | IP kiralama süresi | `86400` saniye (24 saat) |
| **Domain Adı** | Ağın alan adı | `sirket.local` |

---

## DHCP Scope (Havuz)

DHCP sunucusu, dağıtacağı IP adreslerini bir **havuzdan (scope/pool)** seçer:

```
Ağ: 192.168.1.0/24

DHCP Scope:
├── Başlangıç : 192.168.1.50
├── Bitiş     : 192.168.1.200
├── Dağıtılabilir : 151 IP adresi
│
├── Hariç Tutulanlar (Exclusion):
│   ├── 192.168.1.1      → Router (statik)
│   ├── 192.168.1.2      → Sunucu (statik)
│   └── 192.168.1.10     → Yazıcı (statik)
│
└── Rezerve Edilenler (Reservation):
    └── MAC: AA:BB:CC:DD:EE:FF → Her zaman 192.168.1.100 al
```

- **Exclusion:** Belirli IP'lerin DHCP tarafından dağıtılmaması.
- **Reservation:** Belirli bir MAC adresine her zaman aynı IP'nin atanması (DHCP + statik'in en iyisi).


---

## APIPA — DHCP Bulunamazsa?

DHCP'ye ulaşılamazsa işletim sistemi kendine `169.254.x.x` aralığından rastgele bir IP verir (**APIPA**). Bu adres yalnızca aynı durumdaki yerel cihazlarla konuşabilir; internete çıkamaz. Böyle bir adres gördüyseniz tablo nettir: önce kablo, sonra DHCP servisi, en son `ipconfig /renew`.

---

## DHCP Relay (IP Helper)

DHCP broadcast ile konuşur, broadcast ise router'dan geçemez. DHCP sunucusu başka bir ağdaysa router'a **IP Helper (DHCP Relay)** tanımlanır: broadcast'i yakalayıp sunucuya unicast olarak taşır. Kurumsal ağlarda tek merkezi DHCP sunucusu, tüm VLAN'lara böyle hizmet verir.

---

## Özet

| Kavram | Açıklama |
|---|---|
| **DHCP** | Cihazlara otomatik IP dağıtan protokol |
| **DORA** | Discover → Offer → Request → Acknowledge süreci |
| **Lease** | IP adresinin geçerlilik süresi (kiralama) |
| **Scope** | DHCP'nin dağıtacağı IP aralığı (havuz) |
| **Reservation** | Belirli MAC'e sabit IP atama |
| **APIPA** | DHCP bulunamazsa otomatik atanan 169.254.x.x adresi |
| **DHCP Relay** | DHCP broadcast'ini farklı ağa ileten mekanizma |

---

## DHCPv6 — IPv6'da Adres Dağıtımı

IPv6 ağlarında adres atama için **SLAAC** (Stateless Address Autoconfiguration) birincil yöntemdir; cihaz ağ önekini Router Advertisement'tan alarak kendi adresini oluşturur. Ancak SLAAC tek seçenek değildir:

| Yöntem | Açıklama |
|:---|:---|
| **SLAAC** | Cihaz adresini kendi oluşturur, DNS sunucusu bilgisi gelmeyebilir |
| **DHCPv6 Stateless** | SLAAC ile adres alınır; DNS/NTP gibi ek bilgiler DHCPv6'dan gelir |
| **DHCPv6 Stateful** | Adres de dahil tüm yapılandırma DHCPv6 sunucusundan alınır (IPv4 DHCP gibi) |

> 💡 Kurumsal ağlarda DNS sunucusu ataması için genellikle **DHCPv6 Stateless** tercih edilir. Ev modemlerinde ise SLAAC yeterlidir.

