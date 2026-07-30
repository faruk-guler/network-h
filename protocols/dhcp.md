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

DHCP tarafından atanan IP adresleri **kalıcı değildir**; belirli bir süre için "kiralanır". Bu süreye **Lease Time** denir.

### Lease Yaşam Döngüsü

```
├──────────── Lease Süresi (Örn: 24 saat) ────────────┤
│                                                      │
│  %50'de: Yenileme denemesi (Renew)                   │
│  %87.5'te: Son şans (Rebind)                         │
│  %100'de: IP serbest bırakılır                       │
│                                                      │
├──────────┼─────────────────────┼─────────────────────┤
0 saat    12 saat               21 saat               24 saat
```

- **Renew (T1 = %50):** Cihaz, lease süresinin yarısında aynı DHCP sunucusundan süreyi uzatmaya çalışır.
- **Rebind (T2 = %87.5):** İlk sunucudan yanıt gelmezse, ağdaki herhangi bir DHCP sunucusuna başvurur.
- **Süre Dolma:** Hiçbir sunucudan yanıt gelmezse IP serbest bırakılır ve DORA süreci baştan başlar.

> 💡 Ev modemlerinde lease süresi genellikle **24 saat**tır. Kurumsal ağlarda bu süre 8 saate kadar düşürülebilir.

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

## DHCP ile İlgili Komutlar

```cmd
:: Windows
ipconfig /all             # DHCP sunucusu ve lease bilgilerini göster
ipconfig /release         # Mevcut IP adresini bırak
ipconfig /renew           # DHCP'den yeni IP al
```

```bash
# Linux
dhclient -v               # DHCP istemcisini çalıştır (verbose)
dhclient -r               # IP adresini bırak
cat /var/lib/dhcp/dhclient.leases   # Lease bilgilerini göster
```

---

## APIPA — DHCP Bulunamazsa Ne Olur?

DHCP sunucusuna ulaşılamadığında işletim sistemi cihaza **otomatik olarak** `169.254.x.x` aralığından bir IP atar. Bu mekanizmaya **APIPA (Automatic Private IP Addressing)** denir.

- **Aralık:** `169.254.0.0` – `169.254.255.255`
- **Sonuç:** Cihaz yalnızca aynı ağdaki diğer APIPA'lı cihazlarla konuşabilir. İnternete **çıkamaz.**

> ⚠️ Bir cihazın `169.254.x.x` adresi aldığını görüyorsanız:
> 1. Kablo bağlantısını kontrol edin
> 2. DHCP sunucusunun çalıştığından emin olun
> 3. `ipconfig /renew` komutunu deneyin

---

## DHCP Relay (IP Helper)

DHCP, broadcast tabanlı çalışır. Broadcast paketleri router'dan **geçemez**. Peki DHCP sunucusu farklı bir ağdaysa ne olur?

Bu durumda router üzerinde **DHCP Relay (IP Helper)** yapılandırılır. Router, broadcast olarak gelen DHCP paketini unicast olarak DHCP sunucusuna iletir.

```
[Cihaz]  →  Broadcast  →  [Router]  →  Unicast  →  [DHCP Sunucusu]
(VLAN 10)                 (IP Helper)                (VLAN 99)
```

> 💡 Kurumsal ağlarda DHCP sunucusu genellikle merkezi bir sunucu odasındadır ve tüm VLAN'lara IP Helper aracılığıyla hizmet verir.

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
