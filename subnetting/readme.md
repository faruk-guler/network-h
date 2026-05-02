# 📘 IP Subnetting (Alt Ağlara Bölme) Rehberi

## 1. Konu Özeti: Subnetting Nedir?
Subnetting, büyük bir IP bloğunu, daha yönetilebilir küçük ağlara (subnets) bölme işlemidir. Bunu yapmak için farklı formüller vardır.

| # | Formül | Örnek (/26) | Sonuç |
|---|--------|-------------|-------|
| 1 | **Artış** = 256 − Maske | 256 − 192 | **64** |
| 2 | **Alt Ağ Sayısı** = 2^(Yeni−Eski) | 2^(26−24) | **4** |
| 3 | **Ağ Adresi** = IP'yi Artış'a böl → aşağı yuvarla × Artış | 70 ÷ 64 = 1 → 1 × 64 | **10.0.0.64** |
| 4 | **Broadcast** = Ağ Adresi + Artış − 1 | 64 + 64 − 1 | **10.0.0.127** |

## 🔍 Kontrol Formülleri (3 Formül)
> "Bu bölüm yeterli mi?" sorusunu cevaplar
 
| # | Formül | Örnek (/26) | Sonuç |
|---|--------|-------------|-------|
| 5 | **n** = 32 − CIDR | 32 − 26 | **6** |
| 6 | **Toplam IP** = 2ⁿ | 2⁶ | **64** |
| 7 | **Kullanılabilir IP** = 2ⁿ − 2 | 64 − 2 | **62** |

---

### 🔑 Temel Kavramlar
*   **Network ID (Ağ Adresi):** Subnet'in başlangıç noktasıdır. Cihazlara verilmez.
*   **Broadcast Adresi:** Subnet'in bitiş noktasıdır. Tüm cihaza mesaj atmak için kullanılır, cihazlara verilmez.
*   **CIDR (/xx):** Ağ maskesinin kaç bitlik olduğunu gösterir. (Örn: /24, /26)
*   **Artış Sayısı (Block Size):** Bir alt ağın kaç IP adresinden oluştuğunu belirleyen sihirli sayıdır.

---
