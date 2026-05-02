# 📘 IP Subnetting (Alt Ağlara Bölme)

## Subnetting Nedir?
Subnetting, büyük bir IP bloğunu, daha yönetilebilir küçük ağlara (subnets) bölme işlemidir. Bunu yapmak için farklı formüller vardır.

| No | Formül | Örnek (/26) | Sonuç |
|---|--------|-------------|-------|
| 1 | **Artış** = 256 − Maske | 256 − 192 | **64** |
| 2 | **Alt Ağ Sayısı** = 2^(Yeni−Eski) | 2^(26−24) | **4** |
| 3 | **Ağ Adresi** = IP'yi Artış'a böl → aşağı yuvarla × Artış | `10.0.0.70` için: 70 ÷ 64 = 1 → 1 × 64 | **10.0.0.64** |
| 4 | **Broadcast** = Ağ Adresi + Artış − 1 | 64 + 64 − 1 | **10.0.0.127** |

## 🔍 Kontrol Formülleri (+3 Formül daha)
> "Bu bölüm yeterli mi?" sorusunu cevaplar
 
| No | Formül | Örnek (/26) | Sonuç | Özet|
|---|--------|-------------|-------|-------| 
| 5 | **n** = 32 − CIDR | 32 − 26 | **6** |
| 6 | **Toplam IP** = 2ⁿ | 2⁶ | **64** |
| 7 | **Kullanılabilir IP** = 2ⁿ − 2 | 64 − 2 | **62** | Network ve Broadcast adresleri çıkarılır |

---

## Gerçek Dünya Örneği
 
### 🏢 Senaryo
 
Bir şirketin 16 departmanı var. Her departmanın 512 IP talebi olduğunu varsayarak gerekli hesaplamayı yapalım.

> ✅ Networkümüz: 10.5.0.0
 
### Artış sayısı formülü ile hesaplama
 
| Adım | İşlem | Sonuç |
|------|-------|-------|
| Toplam IP | 16 × 512 = 2¹³ | **8,192** |
| Ağ | 8,192 = 2^(32−19) | **10.5.0.0/19** |
| Artış (3. oktette) | 512 IP = 2 × 256 → 3. oktet 2'şer ilerler | **2** |
| Kullanılabilir IP/dept | 512 − 2 | **510 cihaz** |
 
### Subnet Tablosu
 
| No | Departman | Ağ Adresi | Broadcast | Kullanılabilir Aralık |
|---|-----------|-----------|-----------|----------------------|
| 1 | Yönetim | 10.5.0.0 | 10.5.1.255 | 10.5.0.1 − 10.5.1.254 |
| 2 | BT / IT | 10.5.2.0 | 10.5.3.255 | 10.5.2.1 − 10.5.3.254 |
| 3 | İnsan Kaynakları | 10.5.4.0 | 10.5.5.255 | 10.5.4.1 − 10.5.5.254 |
| 4 | Muhasebe | 10.5.6.0 | 10.5.7.255 | 10.5.6.1 − 10.5.7.254 |
| 5 | Satış | 10.5.8.0 | 10.5.9.255 | 10.5.8.1 − 10.5.9.254 |
| 6 | Pazarlama | 10.5.10.0 | 10.5.11.255 | 10.5.10.1 − 10.5.11.254 |
| 7 | Ar-Ge | 10.5.12.0 | 10.5.13.255 | 10.5.12.1 − 10.5.13.254 |
| 8 | Lojistik | 10.5.14.0 | 10.5.15.255 | 10.5.14.1 − 10.5.15.254 |
| 9 | Depo | 10.5.16.0 | 10.5.17.255 | 10.5.16.1 − 10.5.17.254 |
| 10 | Güvenlik | 10.5.18.0 | 10.5.19.255 | 10.5.18.1 − 10.5.19.254 |
| 11 | Teknik Servis | 10.5.20.0 | 10.5.21.255 | 10.5.20.1 − 10.5.21.254 |
| 12 | Kalite Kontrol | 10.5.22.0 | 10.5.23.255 | 10.5.22.1 − 10.5.23.254 |
| 13 | Müşteri Hizmetleri | 10.5.24.0 | 10.5.25.255 | 10.5.24.1 − 10.5.25.254 |
| 14 | Eğitim | 10.5.26.0 | 10.5.27.255 | 10.5.26.1 − 10.5.27.254 |
| 15 | Satın Alma | 10.5.28.0 | 10.5.29.255 | 10.5.28.1 − 10.5.29.254 |
| 16 | Sunucu/Server Odası | 10.5.30.0 | 10.5.31.255 | 10.5.30.1 − 10.5.31.254 |
 
> ✅ 10.5.0.0/19 tam olarak 16 eşit parçaya bölündü. 16 zaten 2'nin kuvveti olduğu için yuvarlama yok, hiç rezerve kalmıyor ve ağ sıfır israfla bölünüyor.

> Her departmana **510 cihaz** bağlanabilir.

> 💡 İhtiyaç duyulan IP veya departman sayısını her zaman bir üst 2'nin kuvvetine (8, 16, 32, 64...) yuvarlayarak tasarıma başlamalısınız."

> 💡 Departman sayısı 2'nin kuvvetiyse (8, 16, 32...) direkt 256'ya böl. Değilse (13, 18, 22...) bir üst 2'nin kuvvetine yuvarla, sonra böl.

### 🔑 Temel Kavramlar
*   **Network ID (Ağ Adresi):** Subnet'in başlangıç noktasıdır. Cihazlara verilmez.
*   **Broadcast Adresi:** Subnet'in bitiş noktasıdır. Tüm cihaza mesaj atmak için kullanılır, cihazlara verilmez.
*   **CIDR (/xx):** Ağ maskesinin kaç bitlik olduğunu gösterir. (Örn: /24, /26)
*   **Artış Sayısı (Block Size):** Bir alt ağın kaç IP adresinden oluştuğunu belirleyen sihirli sayıdır.
