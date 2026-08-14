# Supernetting - Ağları Birleştirmek

Supernetting (Ağ Birleştirme) Route Summarization
Subnetting'in tam tersidir. Parçalanmış küçük ağları (örneğin 10.5.0.0/24, 10.5.1.0/24, 10.5.2.0/24) yönlendiriciye (router) tek tek öğretmek yerine, bunları matematiksel olarak birleştirip tek bir büyük ağ (örn: 10.5.0.0/22) olarak özetleme işlemidir. Yönlendirme tablolarını şişirmemek için hayat kurtarır.

---

## Subnetting ile Farkı Nedir?

| | Subnetting | Supernetting |
|--|-----------|--------------|
| **Ne yapar?** | Büyük ağı böler | Küçük ağları birleştirir |
| **Maske** | Büyür (/24 → /26) | Küçülür (/24 → /22) |
| **Ne zaman kullanılır?** | Ağı bölümlere ayırmak için | Router tablolarını küçültmek için |

---

## Neden İhtiyaç Duyarız?

Bir internet servis sağlayıcısı (ISP) düşünün. Elinde 256 ayrı `/24` ağı var:

```
192.168.0.0/24
192.168.1.0/24
...
192.168.255.0/24
```

Router'ın adres defterinde 256 satır olacak. Bu defter ne kadar büyürse router o kadar yavaş çalışır.

Supernetting ile bu 256 satır **tek satıra** iner:

```
192.168.0.0/16
```

Sonuç: Daha hızlı yönlendirme, daha az bellek kullanımı, daha az güncelleme trafiği.

---

## Nasıl Yapılır?

### Örnek 1: 4 Ağı Birleştirme

Elimizde şu 4 ağ olsun:

```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

**Adım 1: Binary'e Çevir**

Her adresin ikili (binary) karşılığını yazıyoruz:

```
192.168.0.0 = 11000000.10101000.00000000.00000000
192.168.1.0 = 11000000.10101000.00000001.00000000
192.168.2.0 = 11000000.10101000.00000010.00000000
192.168.3.0 = 11000000.10101000.00000011.00000000
```

**Adım 2: Ortak Kısmı Bul**

Soldan sağa bakıyoruz, bitler nerede farklılaşmaya başlıyor?

```
Ortak kısım: 11000000.10101000.000000xx.xxxxxxxx
             |---------- 22 bit ----------|
```

İlk 22 bit hepsinde aynı. Yani ortak prefix uzunluğu: **/22**

**Adım 3: Supernet'i Belirle**

```
192.168.0.0/22
```

Bu tek adres, 4 ağın hepsini kapsar. `/24` = 256 IP, `/22` = 1.024 IP (256 × 4).

---

### Örnek 2: 8 Ağı Birleştirme

Bir ISP'nin 8 müşteri ağı olsun:

```
10.0.0.0/24
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24
10.0.4.0/24
10.0.5.0/24
10.0.6.0/24
10.0.7.0/24
```

Binary'e bakıyoruz:

```
10.0.0.0 = 00001010.00000000.00000000.00000000
10.0.7.0 = 00001010.00000000.00000111.00000000
                              ^^^^^
İlk 21 bit ortak → /21
```

**Sonuç:** `10.0.0.0/21`

8 adet /24 = 8 × 256 = 2.048 IP → tek bir /21 ağında toplandı.

---

## Hızlı Referans Tablosu

| Birleştirilen Ağ Sayısı | Yeni Maske | Örnek |
|-------------------------|------------|-------|
| 2 × /24 | /23 | 192.168.0.0/23 |
| 4 × /24 | /22 | 192.168.0.0/22 |
| 8 × /24 | /21 | 192.168.0.0/21 |
| 16 × /24 | /20 | 192.168.0.0/20 |
| 32 × /24 | /19 | 192.168.0.0/19 |

---

## Üç Temel Kural

**1. Ağlar yan yana olmalı**

Aralarında boşluk olan ağlar birleştirilemez.

```
❌  192.168.0.0/24
    192.168.5.0/24   ← Arada boşluk var!

✅  192.168.0.0/24
    192.168.1.0/24
    192.168.2.0/24
    192.168.3.0/24
```

**2. Ağ sayısı 2'nin katı olmalı**

2, 4, 8, 16... Tam bu sayılardan biri olmalı. 3 veya 5 ağı birleştiremezsiniz.

**3. İlk ağ hizalı olmalı**

4 ağı birleştiriyorsanız ilk adres 4'ün katı olmalı: 0, 4, 8, 12...

```
✅  192.168.0.0/24  ← 0, 4'ün katı
    192.168.1.0/24
    192.168.2.0/24
    192.168.3.0/24
    → 192.168.0.0/22

❌  192.168.1.0/24  ← 1, 4'ün katı değil!
    192.168.2.0/24
    192.168.3.0/24
    192.168.4.0/24
```

---

## Gerçek Hayat: Şirket Birleşmesi

İki şirket birleşiyor ve ağlarını tek bir çatı altında toplamak istiyorlar.

**Şirket A'nın ağları:**

```
172.16.0.0/24
172.16.1.0/24
172.16.2.0/24
172.16.3.0/24
```

**Şirket B'nin ağları:**

```
172.16.4.0/24
172.16.5.0/24
172.16.6.0/24
172.16.7.0/24
```

İki farklı yol var:

**1. Seçenek — Her şirketi ayrı özetle:**

```
Şirket A: 172.16.0.0/22
Şirket B: 172.16.4.0/22
```

Router'ın listesinde 8 satır yerine 2 satır olur.

**2. Seçenek — Hepsini tek adreste topla:**

```
172.16.0.0/21
```

Router'ın listesinde 8 satır yerine sadece 1 satır olur. Birleşme tamamdır.

---

## Gerçek Hayat: Türkiye'nin İnternet Adresleri

Türkiye'deki büyük operatörler, ellerindeki binlerce küçük ağı internete tek bir adres olarak duyurur:

```
Türk Telekom : 88.247.0.0/16
Superonline  : 78.188.0.0/16
Vodafone     : 185.18.0.0/16
```

Eğer her küçük ağı ayrı ayrı duyursalardı, internet router'larının listesi taşınamaz hale gelirdi. Supernetting sayesinde her operatör tek bir satırda temsil edilir.

---

## Supernetting İpuçları

**1. Modern bir routing protokolü kullanın**
Supernetting, tüm modern routing protokolleri tarafından desteklenir. Eski protokoller bu özelliği desteklemeyebilir.

**2. Çakışmadan kaçının**
Aynı IP bloğunu iki farklı yerde özetlemeyin. Router'lar hangi yolu seçeceğini bilemez ve trafik yanlış yere gider.

**3. Hesaplama için araç kullanın**
Binary hesaplamayı elle yapmak zorunda değilsiniz. Subnet calculator araçları bu işi saniyeler içinde yapar.

**4. Neyi özetlediğinizi belgeleyin**
Hangi ağları birleştirdiğinizi not alın. İleride bir sorun çıktığında nereden baktığınızı bilirsiniz.

---

## Bu Bölümde Öğrendiklerimiz

- Supernetting, küçük ağları birleştirip tek adres olarak göstermektir.
- Maske sayısı küçüldükçe kapsanan alan büyür.
- Ağların yan yana olması ve sayının 2'nin katı olması gerekir.
- İnternet bu teknik sayesinde milyonlarca ağı yönetilebilir tutar.

---
