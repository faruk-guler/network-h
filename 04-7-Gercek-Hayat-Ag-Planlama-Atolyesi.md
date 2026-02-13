# 04.7 - Gerçek Hayat Senaryosu: Ağ Planlama Atölyesi 🏗️

Teorik bilgileri öğrendik. Şimdi bareti takın, sahaya iniyoruz! 👷‍♂️

Bu bölümde, boş bir binayı devralıp, sıfırdan çalışan bir ağ planlayacağız. **Hiçbir komut yazmayacağız.** Sadece mühendislik, mantık ve matematik kullanacağız.

---

## 🏢 Senaryo: "TechPlaza" Binası

**Müşteri:** 5 katlı yeni bir ofis binası olan "TechPlaza".
**İsp:** Bize `192.168.10.0/24` bloğunu tahsis etmiş.
**Görev:** Departmanları güvenli ve performanslı bir şekilde bu IP bloğuna yerleştirmek.

### 1. İhtiyaç Analizi (Requirements Analysis) 📝

Önce "Kimin neye ihtiyacı var?" sorusunu soruyoruz.

| Departman | Kat | Cihaz Sayısı | Notlar |
| :--- | :--- | :--- | :--- |
| **Yönetim** | 5 | 10 | Güvenlik kritik. |
| **Yazılım** | 4 | 55 | Çok sayıda test sunucusu var. |
| **Satış** | 3 | 25 | Sürekli mobil cihazlar (Wi-Fi). |
| **Muhasebe** | 2 | 12 | İnterneti kısıtlı olacak. |
| **Misafir** | Zemin | 40 | Sadece internete çıkacak. |
| **Kameralar** | Tüm Bina | 15 | CCTV sistemi. Ayrı ağda olmalı. |
| **Yazıcılar** | Tüm Bina | 5 | Sabit IP verilecek. |

**Toplam Cihaz:** 162
**Mevcut IP Havuzu:** 254 (192.168.10.1 - .254)
**Durum:** IP sayısı yetiyor ancak **doğru bölmemiz** (Subnetting) lazım.

---

## 2. VLAN Tasarımı (Mantıksal Bölümleme) 🧩

Her departmanı ayrı bir **VLAN**'a koyacağız. Bu sayede:

1. Yazılımcıların broadcast trafiği Muhasebeyi yavaşlatmaz.
2. Misafirler Yönetim sunucularına erişemez.

| VLAN ID | İsim | Açıklama |
| :--- | :--- | :--- |
| **10** | Yonetim | 5. Kat |
| **20** | Yazilim | 4. Kat (En kalabalık) |
| **30** | Satis | 3. Kat |
| **40** | Muhasebe | 2. Kat |
| **50** | Guvenlik | Kameralar ve Kartlı Geçiş |
| **80** | Printer | Yazıcılar |
| **99** | Misafir | Zemin Kat Wi-Fi |
| **999** | Yonetim_Net | Switch/Router yönetimi (Management) |

---

## 3. Subnet Hesaplama (VLSM - Değişken Uzunluklu) 🧮

En kritik aşama burası! Pastayı (192.168.10.0/24) dilimleyeceğiz.
**Kural:** Her zaman **en büyük** ihtiyaçtan başlayarak küçüğe doğru sırala!

### Sıralama (Büyükten Küçüğe)

1. **Yazılım:** 55 Cihaz
2. **Misafir:** 40 Cihaz
3. **Satış:** 25 Cihaz
4. **Kameralar:** 15 Cihaz
5. **Muhasebe:** 12 Cihaz
6. **Yönetim:** 10 Cihaz
7. **Yazıcılar:** 5 Cihaz

---

### Adım 1: Yazılım (55 Cihaz)

- İhtiyaç: 55 Host
- En yakın 2'nin kuvveti: $2^6 = 64$ ($64-2 = 62$ IP)
- Gereken Maske: `/26` (255.255.255.192)
- **Subnet:** `192.168.10.0 /26`
- **Aralık:** `192.168.10.1` - `192.168.10.62`
- **Broadcast:** `192.168.10.63`

### Adım 2: Misafir (40 Cihaz)

- Kaldığımız yer: `192.168.10.64`
- İhtiyaç: 40 Host
- En yakın 2'nin kuvveti: $2^6 = 64$ ($62$ IP)
- Gereken Maske: `/26`
- **Subnet:** `192.168.10.64 /26`
- **Aralık:** `192.168.10.65` - `192.168.10.126`
- **Broadcast:** `192.168.10.127`

### Adım 3: Satış (25 Cihaz)

- Kaldığımız yer: `192.168.10.128`
- İhtiyaç: 25 Host
- En yakın 2'nin kuvveti: $2^5 = 32$ ($30$ IP)
- Gereken Maske: `/27` (255.255.255.224)
- **Subnet:** `192.168.10.128 /27`
- **Aralık:** `192.168.10.129` - `192.168.10.158`
- **Broadcast:** `192.168.10.159`

### Adım 4: Kameralar (15 Cihaz)

- Kaldığımız yer: `192.168.10.160`
- İhtiyaç: 15 Host
- En yakın 2'nin kuvveti: $2^5 = 32$ (Çünkü $2^4=16$ ama network+broadcast çıkınca 14 kalır, yetmez!)
- Gereken Maske: `/27`
- **Subnet:** `192.168.10.160 /27`
- **Aralık:** `192.168.10.161` - `192.168.10.190`
- **Broadcast:** `192.168.10.191`

### Adım 5: Muhasebe (12 Cihaz)

- Kaldığımız yer: `192.168.10.192`
- İhtiyaç: 12 Host
- En yakın 2'nin kuvveti: $2^4 = 16$ ($14$ IP)
- Gereken Maske: `/28` (255.255.255.240)
- **Subnet:** `192.168.10.192 /28`
- **Aralık:** `192.168.10.193` - `192.168.10.206`
- **Broadcast:** `192.168.10.207`

### Adım 6: Yönetim (10 Cihaz)

- Kaldığımız yer: `192.168.10.208`
- İhtiyaç: 10 Host
- En yakın 2'nin kuvveti: $2^4 = 16$ ($14$ IP)
- Gereken Maske: `/28`
- **Subnet:** `192.168.10.208 /28`
- **Aralık:** `192.168.10.209` - `192.168.10.222`
- **Broadcast:** `192.168.10.223`

### Adım 7: Yazıcılar (5 Cihaz)

- Kaldığımız yer: `192.168.10.224`
- İhtiyaç: 5 Host
- En yakın 2'nin kuvveti: $2^3 = 8$ ($6$ IP)
- Gereken Maske: `/29` (255.255.255.248)
- **Subnet:** `192.168.10.224 /29`
- **Aralık:** `192.168.10.225` - `192.168.10.230`
- **Broadcast:** `192.168.10.231`

---

## 4. Final Adresleme Tablosu (IP Planı) 📋

İşte bir Ağ Mühendisinin imzası olan belge budur:

| VLAN | Departman | Network Adresi | CIDR | Maske | Gateway | IP Aralığı |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **20** | Yazılım | 192.168.10.0 | /26 | .192 | 10.1 | .2 - .62 |
| **99** | Misafir | 192.168.10.64 | /26 | .192 | 10.65 | .66 - .126 |
| **30** | Satış | 192.168.10.128 | /27 | .224 | 10.129 | .130 - .158 |
| **50** | Kamera | 192.168.10.160 | /27 | .224 | 10.161 | .162 - .190 |
| **40** | Muhasebe | 192.168.10.192 | /28 | .240 | 10.193 | .194 - .206 |
| **10** | Yönetim | 192.168.10.208 | /28 | .240 | 10.209 | .210 - .222 |
| **80** | Printer | 192.168.10.224 | /29 | .248 | 10.225 | .226 - .230 |
| **--** | **BOŞ** | 192.168.10.232 | /29 | .248 | -- | (Yedek) |
| **--** | **BOŞ** | 192.168.10.240 | /28 | .240 | -- | (Yedek) |

> 💡 **Sonuç:** Elimizdeki tek bir `/24` bloğu ile tüm binayı planladık, hiç IP çakışması olmadı ve gelecekte büyüme için hala boş yerimiz (`.232`'den `.255`'e kadar) var!

---

**Navigasyon:**

- [⬅️ Önceki: IPv6 Derinlemesine](./04-IP-Adresleme-ve-Subnetting-IPv6-Derinlemesine.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Routing](./05-Yonlendirme-Routing-Router-Nasil-Calisir.md)
