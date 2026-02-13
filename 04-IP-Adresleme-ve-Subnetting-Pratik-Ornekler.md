# 04 - Pratik Subnetting Örnekleri: Gerçek Senaryolarla Adım Adım

Bu bölümde, **gerçek hayattan örneklerle** subnetting hesaplamalarını adım adım göreceğiz. Teorik bilgiyi pratiğe dökmek için ideal bir rehber!

> 💡 **Not:** Her senaryoda hem "insanca düşünme" hem de "teknik hesaplama" yöntemlerini göstereceğiz.

---

## 📋 İçindekiler

1. [Senaryo 1: Küçük Ofis Ağı (4 Departman)](#senaryo-1-küçük-ofis-ağı)
2. [Senaryo 2: ISP Adres Dağıtımı (3 Şehir)](#senaryo-2-isp-adres-dağıtımı)
3. [Senaryo 3: Router Arası Bağlantılar (Point-to-Point)](#senaryo-3-router-arası-bağlantılar)
4. [Bonus: VLSM ile Verimli IP Kullanımı](#bonus-vlsm-ile-verimli-kullanım)

---

## Senaryo 1: Küçük Ofis Ağı

### 📝 Problem

Bir yazılım şirketinin yeni ofisine ağ kuracaksınız. Şirket, ağı **4 departmana** ayırmak istiyor:

- **Yazılım Ekibi:** 30 kişi
- **Muhasebe:** 10 kişi  
- **İK ve Yönetim:** 8 kişi
- **Misafir Ağı:** 5 cihaz

**Elinizde:** `192.168.10.0/24` ağı var (256 IP adresi).

**Görev:** Her departmana uygun boyutta subnet verin (VLSM kullanarak).

---

### 🧠 Mantıksal Yaklaşım

1. **En büyük ihtiyaçtan başla:** Yazılım Ekibi (30 kişi) → 32 IP gerekir (/27 subnet = 30 kullanılabilir IP).
2. **Sırayla devam et:** Muhasebe (10) → 16 IP (/28 = 14 kullanılabilir), İK (8) → 16 IP (/28), Misafir (5) → 8 IP (/29 = 6 kullanılabilir).

---

### ⚙️ Adım Adım Çözüm

#### 1️⃣ Yazılım Ekibi (30 cihaz)

**İhtiyaç:** En az 30 kullanılabilir IP.

- `/27` = 32 IP toplam → 30 kullanılabilir (2 adres Ağ ve Yayın için)
- **Alt Ağ (Subnet):** `192.168.10.0/27`
- **IP Aralığı:** `192.168.10.1` - `192.168.10.30`
- **Yayın Adresi (Broadcast):** `192.168.10.31`

#### 2️⃣ Muhasebe (10 cihaz)

**İhtiyaç:** En az 10 kullanılabilir IP.

- `/28` = 16 IP toplam → 14 kullanılabilir
- **Alt Ağ (Subnet):** `192.168.10.32/28` (bir sonraki boş blok)
- **IP Aralığı:** `192.168.10.33` - `192.168.10.46`
- **Yayın Adresi (Broadcast):** `192.168.10.47`

#### 3️⃣ İK ve Yönetim (8 cihaz)

**İhtiyaç:** En az 8 kullanılabilir IP.

- `/28` = 16 IP toplam → 14 kullanılabilir (8'den fazla olsa da standart)
- **Alt Ağ (Subnet):** `192.168.10.48/28`
- **IP Aralığı:** `192.168.10.49` - `192.168.10.62`
- **Yayın Adresi (Broadcast):** `192.168.10.63`

#### 4️⃣ Misafir Ağı (5 cihaz)

**İhtiyaç:** En az 5 kullanılabilir IP.

- `/29` = 8 IP toplam → 6 kullanılabilir
- **Alt Ağ (Subnet):** `192.168.10.64/29`
- **IP Aralığı:** `192.168.10.65` - `192.168.10.70`
- **Yayın Adresi (Broadcast):** `192.168.10.71`

---

### 📊 Özet Tablo

| Departman | Alt Ağ (Subnet) | Kullanılabilir IP Aralığı | Yayın Adresi (Broadcast) | Toplam IP |
|-----------|-----------------|---------------------------|--------------------------|-----------|
| **Yazılım** | 192.168.10.0/27 | .1 - .30 | .31 | 30 IP |
| **Muhasebe** | 192.168.10.32/28 | .33 - .46 | .47 | 14 IP |
| **İK** | 192.168.10.48/28 | .49 - .62 | .63 | 14 IP |
| **Misafir** | 192.168.10.64/29 | .65 - .70 | .71 | 6 IP |

**Kullanılan toplam:** 72 IP (256'dan)  
**Kalan boş alan:** `192.168.10.72` - `192.168.10.255` (gelecek genişleme için)

---

## Senaryo 2: ISP Adres Dağıtımı

### 📝 Problem

Bir İnternet Servis Sağlayıcısı (ISP), `10.0.0.0/8` blokunu 3 şehre dağıtacak:

- **İstanbul:** 500,000 müşteri
- **Ankara:** 200,000 müşteri
- **İzmir:** 100,000 müşteri

**Görev:** Her şehre uygun boyutta IP bloğu ayırın.

---

### 🧠 Mantıksal Yaklaşım

Büyük blokları alt bloklara ayırırken **hiyerarşik** düşünün:

- İstanbul için `/13` (524,286 IP)
- Ankara için `/14` (262,142 IP)
- İzmir için `/15` (131,070 IP)

---

### ⚙️ Çözüm

#### 1️⃣ İstanbul (500,000 müşteri)

**Gerekli:** ~500,000 IP → `/13` yeterli (524,286 kullanılabilir IP)

- **Blok:** `10.0.0.0/13`
- **IP Aralığı:** `10.0.0.0` - `10.7.255.255`

#### 2️⃣ Ankara (200,000 müşteri)

**Gerekli:** ~200,000 IP → `/14` yeterli (262,142 kullanılabilir IP)

- **Blok:** `10.8.0.0/14`
- **IP Aralığı:** `10.8.0.0` - `10.11.255.255`

#### 3️⃣ İzmir (100,000 müşteri)

**Gerekli:** ~100,000 IP → `/15` yeterli (131,070 kullanılabilir IP)

- **Blok:** `10.12.0.0/15`
- **IP Aralığı:** `10.12.0.0` - `10.13.255.255`

---

### 📊 Özet Tablo

| Şehir | Blok | IP Aralığı | Kullanılabilir IP | Müşteri Kapasitesi |
|-------|------|------------|-------------------|-------------------|
| **İstanbul** | 10.0.0.0/13 | 10.0.0.0 - 10.7.255.255 | 524,286 | 500K+ |
| **Ankara** | 10.8.0.0/14 | 10.8.0.0 - 10.11.255.255 | 262,142 | 200K+ |
| **İzmir** | 10.12.0.0/15 | 10.12.0.0 - 10.13.255.255 | 131,070 | 100K+ |

**Kalan:** `10.14.0.0` - `10.255.255.255` (gelecek şehirler için)

---

## Senaryo 3: Router Arası Bağlantılar

### 📝 Problem

10 adet router'ı birbirine bağlamanız gerekiyor. Her router-router bağlantısı, **point-to-point** (noktadan noktaya) bir link.

**Soru:** Kaç IP bloğu gerekir ve ne kadar verimli kullanabilirsiniz?

---

### 🧠 Mantıksal Yaklaşım

Point-to-point bağlantılar için **sadece 2 IP** gerekir (bir her uçta bir). Bu durumda `/30` subnet kullanırız:

- `/30` = 4 IP toplam → 2 kullanılabilir (1 Network, 2 Host, 1 Broadcast)

---

### ⚙️ Çözüm

**Elinizde:** `192.168.100.0/24` olsun.

10 link için 10 adet `/30` subnet oluşturursunuz:

| Link No | Alt Ağ (Subnet) | Router A IP | Router B IP | Yayın Adresi (Broadcast) |
|---------|-----------------|-------------|-------------|--------------------------|
| 1 | 192.168.100.0/30 | .1 | .2 | .3 |
| 2 | 192.168.100.4/30 | .5 | .6 | .7 |
| 3 | 192.168.100.8/30 | .9 | .10 | .11 |
| 4 | 192.168.100.12/30 | .13 | .14 | .15 |
| 5 | 192.168.100.16/30 | .17 | .18 | .19 |
| 6 | 192.168.100.20/30 | .21 | .22 | .23 |
| 7 | 192.168.100.24/30 | .25 | .26 | .27 |
| 8 | 192.168.100.28/30 | .29 | .30 | .31 |
| 9 | 192.168.100.32/30 | .33 | .34 | .35 |
| 10 | 192.168.100.36/30 | .37 | .38 | .39 |

**Kullanılan:** Sadece 40 IP (256'dan)  
**Verimlilik:** %100 (gereksiz IP israfı yok!)

---

## Bonus: VLSM ile Verimli Kullanım

### ❓ VLSM Nedir?

**Variable Length Subnet Masking (VLSM)** = Değişken Uzunluklu Alt Ağ Maskeleme. Farklı büyüklükte subnet'ler kullanma sanatı.

**Eski Yöntem (Sabit Subnetting):**  
Tüm departmanlara `/26` (62 IP) verirseniz:

- Yazılım ekibi → 62 IP (30 kullanılıyor, 32 boş)
- Misafir ağı → 62 IP (5 kullanılıyor, 57 boş) ❌ **İsraf!**

**VLSM Yöntemi:**  
Her departmana **tam ihtiyacı kadar** verin (yukarıdaki Senaryo 1'deki gibi). Bu sayede IP adreslerini maksimum verimlilikle kullanırsınız.

---

## 🎯 Pratik İpuçları

1. **En büyükten başlayın:** Subnet'leri ayırırken en büyük ihtiyaçtan başlayın.
2. **2'nin kuvvetlerini bilin:** 16, 32, 64, 128, 256... (Subnet boyutları hep bunlardır)
3. **Hesap makinesi kullanın:** Gerçek hayatta kimse kafadan yapmaz! → [Subnet Calculator](https://farukguler.com/app/IPv4-subnet-calculator/)
4. **Gelecek için yer bırakın:** Ağ genişleyebilir, boş adres blokları rezerve edin.

---

## 🔗 İleri Okuma

- [VLSM Detaylı Rehber](./04-IP-Adresleme-ve-Subnetting-VLSM.md)
- [Supernetting (Route Summarization)](./04-IP-Adresleme-ve-Subnetting-Supernetting.md)

---

**Navigasyon:**

- [⬅️ Önceki: Subnetting Mantığı](./04-IP-Adresleme-ve-Subnetting-Subnetting-Mantigi.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: VLSM](./04-IP-Adresleme-ve-Subnetting-VLSM.md)
