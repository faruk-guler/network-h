# 🔟 Decimal → 🔢 Binary Dönüşümü
 
Binary (ikili) sayı sistemi yalnızca `0` ve `1` rakamlarını kullanır.
Ağ dünyasında IP adresleri ve subnet mask'lar arka planda binary olarak işlenir.
Bu yüzden decimal → binary dönüşümünü bilmek subnetting'in temelidir.
 
---
 
## 📌 Üsler Tablosu
 
Her oktet (byte) **8 bit**'ten oluşur. Her bitin sabit bir ağırlık değeri vardır:
 
```
Pozisyon →   8      7      6      5      4      3      2      1
Değer    →  2⁷     2⁶     2⁵     2⁴     2³     2²     2¹     2⁰
Decimal  → 128     64     32     16      8      4      2      1
```
 
> 💡 Bit `1` ise o pozisyonun değeri **toplanır**, `0` ise **yok sayılır**.
 
---

### 10.5.39.163 → Binary Dönüşüm Tablosu

| Oktet | Decimal | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | Binary | Kontrol |
|-------|---------|-----|----|----|----|---|---|---|---|--------|---------|
| 1. | `10` | 0 | 0 | 0 | 0 | **1** | 0 | **1** | 0 | `00001010` | 8+2=10 ✅ |
| 2. | `5` | 0 | 0 | 0 | 0 | 0 | **1** | 0 | **1** | `00000101` | 4+1=5 ✅ |
| 3. | `39` | 0 | 0 | **1** | 0 | 0 | **1** | **1** | **1** | `00100111` | 32+4+2+1=39 ✅ |
| 4. | `163` | **1** | 0 | **1** | 0 | 0 | 0 | **1** | **1** | `10100011` | 128+32+2+1=163 ✅ |

**Sonuç:** `00001010.00000101.00100111.10100011`
> 🎨 `1` = Turuncu (toplanır) · `0` = Gri (yok sayılır)
