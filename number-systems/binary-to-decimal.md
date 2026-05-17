# 🔢 Binary → Decimal Dönüşüm
## Üsler Tablosu (İkinin Kuvvetleri)

|       Bit     |*. | 8.  | 7. | 6. | 5. | 4. | 3. | 2. | 1. |
|:--------------|:-------:|:-------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
| Gösterim (2ⁿ) | * |   2⁷    |   2⁶   |   2⁵   |   2⁴   |   2³   |   2²   |   2¹   |   2⁰   |
| Decimal Değer | * | **128** | **64** | **32** | **16** | **8**  | **4**  | **2**  | **1**  |

- ...
- 2⁷ = 2 × 2 × 2 × 2 × 2 × 2 × 2 = 128
 
> 💡 Eğer bit `1` ise tablodaki değer **toplanır**, `0` ise o değer **yok sayılır**. Çünkü 0 varsa veri yok, 1 varsa veri var demektir.

> 💡 Her oktette tekrar "0" dan başlanmalıdır.

> 💡 Üslü sayıların kuralı gereği herhangi bir sayının 0. kuvveti 1 olur.

---

## 🔔 Sadece 1 olan bitlerin üslerini al topla: 
IP Adresi: 192.168.1.10 için;
```text
Binary  : 11000000 . 10101000 . 00000001 . 00001010
Gösterim: 2⁷+2⁶      2⁷+2⁵+2³   2⁰         2³+2¹
al topla: 128+64   | 128+32+8 | 1        | 8+2 |
Decimal : 192      . 168      . 1        . 10
```
IP Adresi: 10.5.39.163 için;
```text
Binary  : 00001010 . 00000101 . 00100111 . 10100011
Gösterim: 2³+2¹      2²+2⁰      2⁵+2²+2¹+2⁰   2⁷+2⁵+2¹+2⁰
al topla: 8+2      | 4+1      | 32+4+2+1 | 128+32+2+1 |
Decimal : 10       . 5        . 39       . 163
```
> 💡 **Önemli:** Bit sayımı sağdan **0'** ile başlanarak yapılmalıdır.
