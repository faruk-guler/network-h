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
```text
IP Adresi: 192.168.1.10
Decimal : 192  .  168  .   1   .  10
Binary  : 11000000 . 10101000 . 00000001 . 00001010 > 8 bit     +   8 bit     +  8 bit      +  8 bit    =    32 bit
Hesaplama: | 128+64 | 128+32+8 | 1 | 8+2 |
```
> 💡 **Önemli:** Bit sayımı sağdan **0'** ile başlanarak yapılmalıdır.
