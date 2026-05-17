# 🔟 Decimal → Binary Dönüşümü
 
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
