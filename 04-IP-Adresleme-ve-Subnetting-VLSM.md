# 04 - VLSM (Variable Length Subnet Masking): Custom Pizza Dilimleri

**VLSM**, ağınızı **farklı boyutlarda** subnet'lere bölme sanatıdır. Tek boyutlu dilimler yerine, **tam ihtiyaç kadar** pizza dilimi alırsınız!

---

## 🍕 VLSM Nedir? (Pizza Metaforu)

### Eski Yöntem: Sabit Dilimler ❌

Hayal edin: 8 kişilik bir pizzanız var ve 4 misafiriniz var:

- **Ahmet:** Çok aç, 4 dilim yiyebilir
- **Mehmet:** Orta aç, 2 dilim yeterli
- **Ayşe:** Az aç, 1 dilim yeterli
- **Fatma:** Çok az aç, 1 dilim yeterli

**Sabit dilim yöntemi** derseniz: Pizzayı **4 eşit parça**ya bölersiniz (her biri 2 dilim).

**Sonuç:**

- Ahmet → 2 dilim alır ama hala aç (eksik!)
- Mehmet → 2 dilim (tam kıvamında)
- Ayşe → 2 dilim alır, 1'ini çöpe atar (israf!)
- Fatma → 2 dilim alır, 1'ini çöpe atar (israf!)

### Yeni Yöntem: VLSM (Özel Dilimler) ✅

**VLSM ile:** Herkese **tam ihtiyacı kadar** verirsiniz:

- Ahmet → 4 dilim
- Mehmet → 2 dilim
- Ayşe → 1 dilim
- Fatma → 1 dilim

**Toplam:** 8 dilim, **sıfır israf!** 🎯

---

## 🌐 Gerçek Hayatta VLSM

### Problem: Fixed Subnetting (Sabit Bölme)

Bir ağınız var: `192.168.1.0/24` (256 IP).

3 departmanınız var:

- **IT:** 50 cihaz
- **Muhasebe:** 20 cihaz
- **Misafir:** 5 cihaz

**Sabit subnet** kullanırsanız (örn: hepsine `/26` = 62 IP verirseniz):

| Departman | Verilen Subnet | Kullanılabilir IP | Kullanılan | İsraf |
|-----------|---------------|-------------------|-----------|-------|
| IT | /26 | 62 | 50 | 12 IP |
| Muhasebe | /26 | 62 | 20 | 42 IP |
| Misafir | /26 | 62 | 5 | 57 IP |

**Toplam israf:** 111 IP! 🔴

---

### Çözüm: VLSM (Değişken Uzunluklu Alt Ağ Maskeleme)

Her departmana **tam ihtiyacı kadar** alt ağ (subnet) verin:

| Departman | İhtiyaç | Alt Ağ (Subnet) | Kullanılabilir IP | İsraf |
|-----------|---------|--------|-------------------|-------|
| IT | 50 | /26 | 62 | 12 IP |
| Muhasebe | 20 | /27 | 30 | 10 IP |
| Misafir | 5 | /29 | 6 | 1 IP |

**Toplam israf:** Sadece 23 IP! 🟢 (78 IP kurtarıldı!)

---

## 📐 VLSM Nasıl Uygulanır? (Adım Adım)

### Senaryo

**Elinizdeki Ağ:** `10.0.0.0/8`

**İhtiyaçlar:**

1. **Şube A:** 60,000 cihaz
2. **Şube B:** 30,000 cihaz
3. **Şube C:** 5,000 cihaz
4. **Veri Merkezi:** 1,000 sunucu
5. **Yönetim Ağı:** 50 cihaz

---

### Adım 1: Büyükten Küçüğe Sırala

İhtiyaçları **en büyükten başlayarak** sıralayın:

1. Şube A: 60,000
2. Şube B: 30,000
3. Şube C: 5,000
4. Veri Merkezi: 1,000
5. Yönetim: 50

---

### Adım 2: Uygun Subnet Maskelerini Belirle

Her ihtiyaç için **2'nin kuvveti** kuralına göre subnet seçin:

| İhtiyaç | En Yakın 2ⁿ | Alt Ağ (Subnet) | Kullanılabilir IP |
|---------|-------------|--------|-------------------|
| 60,000 | 65,536 | /16 | 65,534 |
| 30,000 | 32,768 | /17 | 32,766 |
| 5,000 | 8,192 | /19 | 8,190 |
| 1,000 | 2,048 | /21 | 2,046 |
| 50 | 64 | /26 | 62 |

---

### Adım 3: Blokları Sırayla Yerleştir

**Başlangıç:** `10.0.0.0/8`

#### 1️⃣ Şube A (60,000 cihaz → /16)

- **Subnet:** `10.0.0.0/16`
- **IP Aralığı:** `10.0.0.0` - `10.0.255.255`

#### 2️⃣ Şube B (30,000 cihaz → /17)

- **Subnet:** `10.1.0.0/17` (bir sonraki boş blok)
- **IP Aralığı:** `10.1.0.0` - `10.1.127.255`

#### 3️⃣ Şube C (5,000 cihaz → /19)

- **Subnet:** `10.1.128.0/19`
- **IP Aralığı:** `10.1.128.0` - `10.1.159.255`

#### 4️⃣ Veri Merkezi (1,000 sunucu → /21)

- **Subnet:** `10.1.160.0/21`
- **IP Aralığı:** `10.1.160.0` - `10.1.167.255`

#### 5️⃣ Yönetim Ağı (50 cihaz → /26)

- **Subnet:** `10.1.168.0/26`
- **IP Aralığı:** `10.1.168.0` - `10.1.168.63`

---

### 📊 Final Tablo

| Ağ | Alt Ağ (Subnet) | IP Aralığı | Kullanılabilir IP | Kullanım |
|----|--------|------------|-------------------|----------|
| Şube A | 10.0.0.0/16 | 10.0.0.0 - 10.0.255.255 | 65,534 | 60,000 |
| Şube B | 10.1.0.0/17 | 10.1.0.0 - 10.1.127.255 | 32,766 | 30,000 |
| Şube C | 10.1.128.0/19 | 10.1.128.0 - 10.1.159.255 | 8,190 | 5,000 |
| Veri Merkezi | 10.1.160.0/21 | 10.1.160.0 - 10.1.167.255 | 2,046 | 1,000 |
| Yönetim | 10.1.168.0/26 | 10.1.168.0 - 10.1.168.63 | 62 | 50 |

**Kalan Adres Alanı:** `10.1.168.64` - `10.255.255.255` (gelecek genişleme için!)

---

## 🎯 VLSM Altın Kuralları

1. **Büyükten Başla:** En büyük subnet ihtiyacını önce yerleştir.
2. **2'nin Kuvvetleri:** Subnet boyutları hep 2, 4, 8, 16, 32, 64, 128... şeklindedir.
3. **Hizalama Önemli:** Her subnet, kendi boyutunun katı olan adresten başlamalıdır.
   - Örn: /24 subnet, .0, .256, .512'den başlayabilir ama .50'den başlayamaz!
4. **Boşluk Bırak:** Gelecekte büyüme ihtimali varsa fazladan alan rezerve et.

---

## 💡 VLSM vs Fixed Subnetting

| Özellik | Fixed Subnetting | VLSM |
|---------|------------------|------|
| **Esneklik** | Düşük | Yüksek |
| **IP İsrafı** | Çok | Minimal |
| **Karmaşıklık** | Basit | Orta |
| **Kullanım Alanı** | Küçük ağlar | Büyük/Karmaşık ağlar |
| **Routing Desteği** | Sınıflı (Classful - RIPv1) | Sınıfsız (Classless - RIPv2, OSPF, EIGRP) |

---

## 🔍 Pratik Örnek: Şirket Ağı

**Senaryo:** Bir yazılım şirketi, `172.16.0.0/16` bloğunu alt ağlara bölecek.

**İhtiyaçlar:**

- Geliştirme: 2,000 cihaz
- Test: 500 cihaz
- Üretim: 100 sunucu
- Yönetim: 20 cihaz
- DMZ: 10 sunucu

**VLSM Çözümü:**

| Ağ | İhtiyaç | Alt Ağ (Subnet) | Blok Adresi | Kullanılabilir IP |
|-----|---------|--------|------|-------------------|
| Geliştirme | 2,000 | /21 | 172.16.0.0/21 | 2,046 |
| Test | 500 | /23 | 172.16.8.0/23 | 510 |
| Üretim | 100 | /25 | 172.16.10.0/25 | 126 |
| Yönetim | 20 | /27 | 172.16.10.128/27 | 30 |
| DMZ | 10 | /28 | 172.16.10.160/28 | 14 |

**Sonuç:** Minimum israf, maksimum verimlilik! 🎯

---

## 🚀 İleri Seviye: VLSM + Supernetting

VLSM kullanarak ağı böldükten sonra, **Supernetting** (Route Summarization) ile birden fazla subnet'i tek bir routing bilgisiyle özetleyebilirsiniz.

**Örnek:**  
`172.16.0.0/21`, `172.16.8.0/23`, `172.16.10.0/25`  
→ Hepsi `172.16.0.0/20` ile özetlenebilir (routing tablosunu küçültür).

Detaylar için: [Supernetting Rehberi](./04-IP-Adresleme-ve-Subnetting-Supernetting.md)

---

## 🔗 Kaynaklar ve Araçlar

- 🧮 [Subnet Calculator](https://farukguler.com/app/IPv4-subnet-calculator/)
- 📖 [RFC 1878 - VLSM Tablo](https://www.rfc-editor.org/rfc/rfc1878)

---

**Navigasyon:**

- [⬅️ Önceki: Pratik Örnekler](./04-IP-Adresleme-ve-Subnetting-Pratik-Ornekler.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Supernetting](./04-IP-Adresleme-ve-Subnetting-Supernetting.md)
