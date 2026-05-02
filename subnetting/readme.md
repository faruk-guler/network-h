# 📘 IP Subnetting (Alt Ağlara Bölme) Rehberi

## 1. Konu Özeti: Subnetting Nedir?
Subnetting, büyük bir IP bloğunu, daha yönetilebilir küçük ağlara (subnets) bölme işlemidir. Bunu yapmak için farklı formüller vardır.

## 5 TEMEL FORMÜL

| Formül | Açıklama | Örnek (/26) |
|--------|----------|-------------|
| **Artış = 256 - Maske** | Ağların ilerleme adımı | 256 - 192 = **64** |
| **n = 32 - CIDR** | Host bit sayısı | 32 - 26 = **6** |
| **Toplam IP = 2ⁿ** | Bloktaki toplam adres | 2⁶ = **64** |
| **Kullanılabilir = 2ⁿ - 2** | Cihaza atanabilir IP | 64 - 2 = **62** |
| **Alt Ağ = 2^(Yeni-Eski)** | Kaç parçaya bölündü | 2^(26-24) = **4** |

---

## 🔄 5 ADIMDA HESAPLAMA


### 🔑 Temel Kavramlar
*   **Network ID (Ağ Adresi):** Subnet'in başlangıç noktasıdır. Cihazlara verilmez.
*   **Broadcast Adresi:** Subnet'in bitiş noktasıdır. Tüm cihaza mesaj atmak için kullanılır, cihazlara verilmez.
*   **CIDR (/xx):** Ağ maskesinin kaç bitlik olduğunu gösterir. (Örn: /24, /26)
*   **Artış Sayısı (Block Size):** Bir alt ağın kaç IP adresinden oluştuğunu belirleyen sihirli sayıdır.

---
