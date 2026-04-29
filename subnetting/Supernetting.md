# 04 - Supernetting (Rota Özeti / Ağ Birleştirme)

**Supernetting**, subnettingin tam tersidir! Birden fazla küçük ağı, **tek bir büyük ağ** gibi göstererek routing tablosunu küçültürüz.

> 💡 **Benzetme:** Subnetting = Pizza dilimleme, Supernetting = Dilimleri tekrar birleştirme.

---

## 🔄 Supernetting Nedir?

### Subnetting vs Supernetting

| Özellik | Subnetting | Supernetting |
|---------|-----------|--------------|
| **Amaç** | Büyük ağı küçük parçalara ayırma | Küçük ağları birleştirme |
| **Subnet Mask** | Büyüyor (/24 → /26) | Küçülüyor (/24 → /22) |
| **Host Bitleri** | Azalıyor | Artıyor |
| **Kullanım Alanı** | Ağ segmentasyonu | Routing optimizasyonu |

---

## 🌍 Neden Supernetting Kullanırız?

### Problem: Yönlendirme Tablosu (Routing Table) Şişmesi

Hayal edin, bir ISP (İnternet Servis Sağlayıcısı) 256 ayrı `/24` ağını yönetiyor:

```text
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
...
192.168.255.0/24
```

Router'ın yönlendirme tablosunda **256 satır** olacak! 😱

### Çözüm: Supernetting (Rota Özeti - Route Summarization)

Bu 256 ağı **tek satırda** özetleyebiliriz:

```text
192.168.0.0/16
```

**Sonuç:**

- Yönlendirme tablosu: 256 satır → **1 satır** ✅
- Router belleği: Daha verimli
- Yönlendirme güncellemeleri: Daha hızlı

---

## 📐 Supernetting Nasıl Yapılır?

### Örnek 1: 4 Ardışık /24 Ağı Birleştirme

Elimizde 4 ağ var:

```text
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

#### Adım 1: Binary'e Çevir

```text
192.168.0.0 = 11000000.10101000.00000000.00000000
192.168.1.0 = 11000000.10101000.00000001.00000000
192.168.2.0 = 11000000.10101000.00000010.00000000
192.168.3.0 = 11000000.10101000.00000011.00000000
```

#### Adım 2: Ortak Kısmı Bul

```text
Ortak kısım: 11000000.10101000.000000
               ^^^^^^^^ ^^^^^^^^ ^^^^^^
               24 bit ortak → /22 
```

#### Adım 3: Supernet Belirle

**Sonuç:** `192.168.0.0/22`

Bu tek bir subnet, **4 adet /24 ağını** kapsar!

**Özet:**

- `/24` = 256 IP
- `/22` = 1,024 IP (256 × 4)

---

### Örnek 2: ISP Adres Bloğu

**Senaryo:** ISP'niz şu blokları müşterilere dağıtmış:

```text
10.0.0.0/24
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24
10.0.4.0/24
10.0.5.0/24
10.0.6.0/24
10.0.7.0/24
```

#### Soru: Bunları internet backbone'a nasıl duyurursunuz?

**Cevap:** Supernetting ile tek satırda:

```text
10.0.0.0/21
```

**Neden /21?**

- 8 adet /24 = 8 × 256 = 2,048 IP
- 2,048 IP = 2^11 = /21

#### Doğrulama

```text
10.0.0.0 (binary) = 00001010.00000000.00000000.00000000
10.0.7.0 (binary) = 00001010.00000000.00000111.00000000
                                        ^^^^^
Ortak kısım: 21 bit → /21
```

---

## 🎯 Supernetting Kuralları

### Kural 1: Ardışık Olmalı

Birleştirmek istediğiniz ağlar **ardışık (contiguous)** olmalıdır.

**❌ Yanlış:**

```text
192.168.0.0/24
192.168.5.0/24  ← Arada boşluk var!
```

**✅ Doğru:**

```text
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

### Kural 2: 2'nin Kuvveti Olmalı

Birleştirdiğiniz ağ sayısı **2'nin kuvveti** olmalıdır:

- 2 ağ → ✅
- 4 ağ → ✅
- 8 ağ → ✅
- 16 ağ → ✅
- 5 ağ → ❌ (2, 4, 8 seçenekleri var)

### Kural 3: İlk Ağ "Hizalı" Olmalı

İlk ağ, supernet boyutunun katı olmalıdır.

**Örnek:** 4 adet /24'ü /22'ye çevirmek istiyorsanız:

**✅ Doğru:**

```text
192.168.0.0/24  ← 0, 4'ün katı
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
→ 192.168.0.0/22
```

**❌ Yanlış:**

```text
192.168.1.0/24  ← 1, 4'ün katı değil!
192.168.2.0/24
192.168.3.0/24
192.168.4.0/24
```

---

## 🔍 Gerçek Hayat Örneği: Şirket Birleşmesi

**Senaryo:** İki şirket birleşiyor ve ağlarını tek bir routing altında birleşecekler.

**Şirket A'nın ağları:**

```text
172.16.0.0/24
172.16.1.0/24
172.16.2.0/24
172.16.3.0/24
```

**Şirket B'nin ağları:**

```text
172.16.4.0/24
172.16.5.0/24
172.16.6.0/24
172.16.7.0/24
```

#### Birleştirme Stratejisi

**1. Seçenek:** Her şirketi ayrı özetle

```text
Şirket A: 172.16.0.0/22
Şirket B: 172.16.4.0/22
```

**2. Seçenek:** Hepsini tek özette

```text
172.16.0.0/21  ← 8 ağ tek satırda!
```

---

## 📊 Supernetting Hızlı Referans Tablosu

| Birleştirilen Ağ Sayısı | Subnet Mask Değişimi | Örnek |
|-------------------------|---------------------|-------|
| 2 × /24 | /23 | 192.168.0.0/23 |
| 4 × /24 | /22 | 192.168.0.0/22 |
| 8 × /24 | /21 | 192.168.0.0/21 |
| 16 × /24 | /20 | 192.168.0.0/20 |
| 32 × /24 | /19 | 192.168.0.0/19 |
| 64 × /24 | /18 | 192.168.0.0/18 |
| 128 × /24 | /17 | 192.168.0.0/17 |
| 256 × /24 | /16 | 192.168.0.0/16 |

---

## 🚀 BGP ve Supernetting

**BGP (Sınır Ağ Geçidi Protokolü - Border Gateway Protocol)**, internetteki büyük router'ların kullandığı protokoldür. Supernetting, BGP'nin can damarıdır!

### Örnek: Türkiye'nin IP Blokları

Türkiye'deki tüm ISP'ler, blokları internete şöyle duyurur:

```text
Türk Telekom: 88.247.0.0/16
Superonline: 78.188.0.0/16
Vodafone: 185.18.0.0/16
```

Eğer her `/24`'ü ayrı ayrı duyursalardı, internet routing tablosu patlardı! Supernetting sayesinde her ISP tek bir satırda özetlenir.

---

## 💡 Supernetting İpuçları

1. **Yönlendirme Protokolü Seçimi:** Sınıflı (Classful) routing (RIPv1) supernetting desteklemez. Sınıfsız (Classless) (RIPv2, OSPF, EIGRP, BGP) kullanın.

2. **Overlapping'den Kaçının:** İki farklı yerde aynı IP bloğunu özetlemeyin, routing çakışması olur!

3. **Hesaplama Kolaylığı:** Binary hesaplamaya gerek yok, subnet calculator kullanın.

4. **Dokümantasyon:** Hangi blokları özetlediğinizi mutlaka not edin, aksi halde ağ yönetimi karmaşıklaşır.

---

## 🔗 İlgili Konular

- [VLSM (Variable Length Subnet Masking)](./04-IP-Adresleme-ve-Subnetting-VLSM.md)
- [CIDR Notasyonu](./04-IP-Adresleme-ve-Subnetting-IP-Adresi-ve-CIDR.md)
- [Routing Protokolleri](./05-Yonlendirme-Routing-Router-Nasil-Calisir.md)

---

## 🧮 Pratik Alıştırma

**Soruların:**

1. Şu 4 ağı tek bir supernet ile özetleyin:

   ```
   10.10.8.0/24
   10.10.9.0/24
   10.10.10.0/24
   10.10.11.0/24
   ```

2. `172.20.0.0/22` supernet'i kaç adet `/24` ağı kapsar?

<details>
<summary><strong>Cevaplar (Tıklayın)</strong></summary>

1. **Cevap:** `10.10.8.0/22`
   - İlk ağ: .8 (8, 4'ün katı ✅)
   - 4 ağ → /24'ten /22'ye

2. **Cevap:** **4 adet /24**
   - /22 = 1,024 IP
   - /24 = 256 IP
   - 1,024 / 256 = 4

</details>

---

**Navigasyon:**

- [⬅️ Önceki: VLSM](./04-IP-Adresleme-ve-Subnetting-VLSM.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: IPv6 Derinlemesine](./04-IP-Adresleme-ve-Subnetting-IPv6-Derinlemesine.md)
