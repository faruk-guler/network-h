# 🔟 Decimal → Binary Dönüşümü
 
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

## 🔔 “Kutuda varsa 1, yoksa 0”
Decimal sayıyı başlangıçta 'Kutu' olarak al; her bit değerine sor, Kalan'ın içinde bu değer varsa 1 yaz ve çıkar, yoksa 0 yaz ve sonrakine geç."

IP Adresi: 10.5.39.163 için;

| Oktet | Decimal/Kutu | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | Binary | Kontrol |
|-------|---------|-----|----|----|----|---|---|---|---|--------|---------|
| 1. | `10` | 0 | 0 | 0 | 0 | **1** | 0 | **1** | 0 | `00001010` | 8+2=10 ✅ |
| 2. | `5` | 0 | 0 | 0 | 0 | 0 | **1** | 0 | **1** | `00000101` | 4+1=5 ✅ |
| 3. | `39` | 0 | 0 | **1** | 0 | 0 | **1** | **1** | **1** | `00100111` | 32+4+2+1=39 ✅ |
| 4. | `163` | **1** | 0 | **1** | 0 | 0 | 0 | **1** | **1** | `10100011` | 128+32+2+1=163 ✅ |

**Sonuç:** `00001010.00000101.00100111.10100011`

```text
Decimal  : 10       . 5        . 39       . 163
Binary   : 00001010 . 00000101 . 00100111 . 10100011
```
