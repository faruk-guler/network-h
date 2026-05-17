# 🔢 Binary → Decimal Dönüşüm
## Üsler Tablosu (İkinin Kuvvetleri)

|       Bit     |*  | 8  | 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|:--------------|:-------:|:-------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
| Gösterim (2ⁿ) | * |   2⁷    |   2⁶   |   2⁵   |   2⁴   |   2³   |   2²   |   2¹   |   2⁰   |
| Decimal Değer | * | **128** | **64** | **32** | **16** | **8**  | **4**  | **2**  | **1**  |

- ...
- 2⁷ = 2 × 2 × 2 × 2 × 2 × 2 × 2 = 128
 
> 💡 **Kural:** Eğer bit `1` ise tablodaki değer **toplanır**, `0` ise o değer **yok sayılır**. Çünkü 0 varsa veri yok, 1 varsa veri var demektir.

> 💡 Her octecte tekrar "0" dan başlanmalıdır.

> 💡 Üslü sayıların kuralı gereği herhangi bir sayının 0. kuvveti 1 olur.

---

## 🔔 1 olan bitlerin üstlerini al ve topla:
```
IP Adresi: 192.           168.          1.            10.

[32]          [24]                [11]          [3] [1] 
[1]1000000    [1]0101000     00000[0]01    00001[0]1[0]
8 bit     +   8 bit     +  8 bit      +  8 bit    =    32 bit
```
- Bit sayımı sağdan başlanarak yapılmalıdır.

  ### IP Adresi: 192.168.1.10 (32-Bit Analizi)

| Oktet | 1. Oktet (192) | 2. Oktet (168) | 3. Oktet (1) | 4. Oktet (10) |
|-------|----------------|----------------|--------------|---------------|
| **Binary** | `11000000` | `10101000` | `00000001` | `00001010` |
| **Bit Aralığı** | Bit 1 - 8 | Bit 9 - 16 | Bit 17 - 24 | Bit 25 - 32 |
| **Hesaplama** | 128+64 | 128+32+8 | 1 | 8+2 |
