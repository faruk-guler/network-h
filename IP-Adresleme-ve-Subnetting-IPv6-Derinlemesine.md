# 04 - IPv6 Derinlemesine: Geleceğin İnternet Adresi

IPv6 (Internet Protocol version 6), IPv4'ün yerini alacak yeni nesil IP adresleme sistemidir. Neredeyse **sonsuz sayıda adres** sunar!

> 💡 **Gerçek:** IPv6 ile dünyada her kum tanesine bir IP adresi versek bile adresler bitmez!

---

## 🌍 Neden IPv6'ya İhtiyaç Var?

### IPv4'ün Problemi

- **IPv4:** 32 bit = 4.3 milyar adres (2³²)
- **Dünya nüfusu:** 8+ milyar insan
- **İnternete bağlı cihaz sayısı:** 50+ milyar (telefonlar, bilgisayarlar, IoT cihazları)

**Sonuç:** IPv4 adresleri **2011'de tükendi!** 😱

### IPv6'nın Çözümü

- **IPv6:** 128 bit = 340 undecillion adres (2¹²⁸)
- **Karşılaştırma:** IPv4'ten 340 trilyon trilyon trilyon kat daha fazla!

```text
IPv4: 4,300,000,000 adres
IPv6: 340,282,366,920,938,463,463,374,607,431,768,211,456 adres
```

---

## 📐 IPv6 Adresi Yapısı

### IPv4 vs IPv6

| Özellik | IPv4 | IPv6 |
|---------|------|------|
| **Bit Uzunluğu** | 32 bit | 128 bit |
| **Format** | Decimal (Onluk taban) | Onaltılık (Hexadecimal) |
| **Örnek** | 192.168.1.1 | 2001:0db8:85a3:0000:0000:8a2e:0370:7334 |
| **Bölümler** | 4 oktet (8 bit × 4) | 8 hextet (16 bit × 8) |
| **Ayırıcı** | Nokta (.) | İki nokta (:) |

---

### IPv6 Adres Örneği

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
│    │    │    │    │    │    │    │
└────┴────┴────┴────┴────┴────┴────┴─ 8 adet 16-bit hextet
```

Her hextet (4 karakter) = 16 bit = 0000'den FFFF'e kadar değer alabilir.

---

## ✂️ IPv6 Kısaltma Kuralları

IPv6 adresleri çok uzun! Ancak **2 kısaltma kuralı** vardır:

### Kural 1: Başındaki Sıfırları Sil

Her hextet'in **başındaki sıfırları** silebilirsiniz.

**Örnek:**

```text
Uzun hali:    2001:0db8:0000:0042:0000:8a2e:0370:7334
Kısa hali:    2001:db8:0:42:0:8a2e:370:7334
              └─┘  └─┘ └ └─┘ └ └──┘ └─┘ └──┘
              Başındaki sıfırlar temizlendi
```

### Kural 2: Ardışık Sıfır Blokları → `::`

**Bir kez** kullanarak, ardışık sıfır hextet'leri `::` ile değiştirebilirsiniz.

**Örnek:**

```text
Uzun hali:    2001:0db8:0000:0000:0000:0000:0000:0001
Kısa hali:    2001:db8::1
                      ^^
              5 adet sıfır hextet → ::
```

⚠️ **Dikkat:** `::` sadece **bir kez** kullanılabilir! Aksi halde adres belirsiz olur.

**❌ Yanlış:**

```text
2001::db8::1  ← İki kez :: kullanıldığı için hatalı!
```

**✅ Doğru:**

```text
2001:db8:0:0:0:0:0:1  → 2001:db8::1
```

---

## 📊 IPv6 Adres Türleri

IPv6'da 3 ana adres türü vardır:

### 1. Tekil (Unicast) - Bir Cihaza

Bir cihazın kendine özel adresidir. 3 alt türü var:

#### a) Küresel Tekil (Global Unicast) - İnternete Açık

- **Önek (Prefix):** `2000::/3` (2000 ile 3FFF arası başlar)
- **Karşılığı:** IPv4'teki Public IP
- **Örnek:** `2001:db8:acad:1::1/64`

#### b) Yerel Bağlantı (Link-Local)

- **Önek (Prefix):** `fe80::/10`
- **Karşılığı:** IPv4'teki 169.254.x.x (APIPA)
- **Kullanım:** Aynı ağdaki cihazlar arası iletişim
- **Örnek:** `fe80::1/64`
- **Özellik:** Router'dan geçmez, sadece yerel segment!

#### c) Benzersiz Yerel (Unique Local) - Private IP

- **Önek (Prefix):** `fc00::/7` (fc00 veya fd00 ile başlar)
- **Karşılığı:** IPv4'teki 192.168.x.x, 10.x.x.x
- **Örnek:** `fd00:1234:5678::1/64`

---

### 2. Çoğul (Multicast) - Gruba

- **Önek (Prefix):** `ff00::/8`
- **Karşılığı:** IPv4'teki 224.0.0.0/4
- **Kullanım:** Bir kaynaktan birden fazla hedefe veri gönderme
- **Örnek:** `ff02::1` (tüm cihazlar)

⚠️ **Not:** IPv6'da **broadcast (yayın) yok!** Multicast kullanılır.

---

### 3. Herhangi Bir (Anycast) - En Yakın Cihaza

- Aynı IP'yi birden fazla cihaza atarsınız
- Paket, **en yakın** cihaza gider
- **Kullanım:** DNS sunucuları, load balancing

---

## 🎯 IPv6 Önek Uzunlukları (CIDR - Prefix)

IPv4'teki gibi, IPv6'da da `/` notasyonu kullanılır.

### Yaygın Önekler (Prefixes)

| Önek (Prefix) | Kullanım | Açıklama |
|--------|----------|----------|
| **/128** | Tek cihaz | IPv4'teki /32 gibi |
| **/64** | Standart subnet | **En yaygın kullanım!** |
| **/56** | Küçük kuruluşlar | Ev/ofis ağları (256 adet /64 subnet) |
| **/48** | Orta kuruluşlar | Şirketler (65,536 adet /64 subnet) |
| **/32** | ISP'ler | Servis sağlayıcılar |

> 💡 **Altın Kural:** Özel kullanım için `/64` standarttır!

---

## 🧮 IPv6 Subnetting (İnanılmaz Basit!)

IPv6'da subnetting, IPv4'ten **çok daha kolay!**

### Neden?

- IPv4: Host bitlerine dokunuyorduk (karmaşık!)
- IPv6: Sadece **subnet ID** kısmını değiştiriyoruz (basit!)

### Örnek: Bir /48 Bloğu Bölme

**Elinizde:** `2001:db8:acad::/48`

**Hedef:** 16 adet /64 subnet oluştur.

#### Adım 1: Hextet'leri Anla

```text
2001:db8:acad:0000:0000:0000:0000:0000/48
              ^^^^
              Subnet ID (ilk 16 bit boş)
```

#### Adım 2: Subnet ID'yi Değiştir

```text
Subnet 1: 2001:db8:acad:0001::/64
Subnet 2: 2001:db8:acad:0002::/64
Subnet 3: 2001:db8:acad:0003::/64
...
Subnet 16: 2001:db8:acad:0010::/64  (10 hex = 16 decimal)
```

**İşte bu kadar!** 🎉

---

### IPv6 Subnetting Tablosu

| Verilen Blok | Subnet Sayısı | Alt Ağ Öneki (Subnet Prefix) |
|--------------|---------------|---------------|
| /48 | 65,536 | /64 |
| /52 | 4,096 | /64 |
| /56 | 256 | /64 |
| /60 | 16 | /64 |

---

## 🔧 IPv6 Adres Konfigürasyonu

### 1. Durumsuz Adres Otomatik Yapılandırma (SLAAC)

IPv6'nın en güzel özelliği: **Otomatik IP alma** (DHCP'ye gerek yok!)

**Nasıl Çalışır?**

1. Cihaz açılır
2. Router'a "Router Advertisement" (RA) mesajı gönderir
3. Router, prefix'i (`2001:db8:acad:1::/64`) gönderir
4. Cihaz, MAC adresinden EUI-64 ile kendi IP'sini oluşturur

**Örnek:**

```text
Prefix: 2001:db8:acad:1::/64
MAC:    00:1A:2B:3C:4D:5E
→ IPv6: 2001:db8:acad:1:021a:2bff:fe3c:4d5e/64
```

### 2. DHCPv6 (Stateful)

IPv4'teki DHCP gibi, sunucu IP dağıtır.

### 3. Manuel (Static)

Elle IP atarsınız.

---

## 🌐 Çift Yığın (Dual-Stack) - IPv4 + IPv6 Birlikte

**Geçiş dönemi stratejisi:** Her cihazda hem IPv4 hem IPv6 olsun.

**Örnek:**

```text
IPv4: 192.168.1.10
IPv6: 2001:db8:acad:1::10
```

Hedefe göre uygun protokol kullanılır.

---

## 🔍 Pratik Örnekler

### Örnek 1: Ev Ağı

**ISP'nizden aldığınız:** `2001:db8:1234::/56`

**Alt ağlar:**

```text
Ev LAN:       2001:db8:1234:1::/64
Misafir Wi-Fi: 2001:db8:1234:2::/64
IoT Cihazlar:  2001:db8:1234:3::/64
```

### Örnek 2: Şirket Ağı

**Elinizde:** `2001:db8:acad::/48`

**Departmanlar:**

```text
IT:        2001:db8:acad:10::/64
HR:        2001:db8:acad:20::/64
Muhasebe:  2001:db8:acad:30::/64
Sunucular: 2001:db8:acad:100::/64
```

---

## 💡 IPv6 İpuçları

1. **Herzaman /64 kullanın:** Özel ağlar için standart budur.
2. **SLAAC kullanın:** Otomasyon harikadır.
3. **Link-Local otomatiktir:** Her interface'de `fe80::` mutlaka vardır.
4. **Broadcast yok:** Multicast kullanın (`ff02::1`).
5. **Ping komutu:** `ping` yerine `ping6` kullanın (Linux/Mac).

---

## 🔗 Özel IPv6 Adresleri

| Adres | Anlamı |
|-------|--------|
| `::1/128` | Geri Döngü (Loopback - Localhost) |
| `::` | Tüm sıfırlar (0.0.0.0 gibi) |
| `::/0` | Varsayılan Rota (Default route) |
| `fe80::/10` | Yerel Bağlantı (Link-Local) |
| `ff02::1` | Tüm cihazlar (multicast) |
| `ff02::2` | Tüm router'lar |

---

## 🏎️ IPv4'ten IPv6'ya Geçiş Yöntemleri

İnternet bir gecede IPv6'ya geçemez. Bu yüzden birlikte yaşama yöntemleri kullanılır:

### 1. Çift Yığın (Dual-Stack)
Cihazlarda hem IPv4 hem IPv6 adresinin aynı anda bulunmasıdır. Modern sistemlerin çoğu varsayılan olarak budur.

### 2. Tünelleme (Tunneling)
IPv6 paketlerini, henüz IPv6 desteklemeyen bir ağdan geçirebilmek için **IPv4 paketlerinin içine saklayarak (kapsülleyerek)** taşımaktır.

### 3. Çeviri (Translation - NAT64)
IPv6 kullanan bir cihazın, sadece IPv4 destekleyen bir sunucuyla konuşabilmesi için yapılan protokol çevirisidir.

---

## 🚀 IPv6 ile Geleceğe Hazır Olun

IPv6 artık kaçınılmaz. Birçok modern sistem varsayılan olarak IPv6 kullanıyor:

- **Google:** Trafiğin %40+'ı IPv6
- **Facebook:** Tam IPv6 desteği
- **Cloudflare:** Tüm hizmetlerde IPv6

---

**Navigasyon:**

- [⬅️ Önceki: Supernetting](./04-IP-Adresleme-ve-Subnetting-Supernetting.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Gerçek Hayat Senaryosu (Workshop)](./04-7-Gercek-Hayat-Ag-Planlama-Atolyesi.md)
