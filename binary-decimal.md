# İkili (Binary) - Onlu (Decimal) Sistem Dönüşümü

Bilgisayarlar verileri 1 ve 0'lar (Binary) halinde işler. IP adresleri ve alt ağ maskeleri (Subnet Mask) gibi kavramları daha iyi anlamak için Binary-Decimal dönüşüm mantığını kavramak çok önemlidir.

## Sihirli Tablo: 128 - 1 Kuralı

IP adreslerindeki her bir bölüm (oktet) 8 bitten oluşur. Bu 8 bitin her birinin onlu sistemde sabit bir karşılığı vardır. Sağdan sola doğru bu değerler sürekli 2 ile çarpılarak artar.

| 8. Bit | 7. Bit | 6. Bit | 5. Bit | 4. Bit | 3. Bit | 2. Bit | 1. Bit |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |

> 💡 **Kural:** Eğer bit `1` ise tablodaki değer **toplanır**, `0` ise o değer **yok sayılır**.

---

## 🔄 Örnek Dönüşümler

### Örnek 1: Binary'den Decimal'e Çevirme

Elimizdeki 8 bitlik sayımız: `10101000` olsun.

| Değer | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binary** | **1** | **0** | **1** | **0** | **1** | **0** | **0** | **0** |
| **Sonuç** | 128 | 0 | 32 | 0 | 8 | 0 | 0 | 0 |

**Hesaplama:** Sadece `1` olan değerleri topluyoruz.
128 + 32 + 8 = **168**

### Örnek 2: Decimal'den Binary'e Çevirme

Sorumuz: `192` sayısını ikili (binary) sisteme çevirelim.

Soldan sağa doğru tablodaki değerleri sorarak ilerliyoruz: "Bu sayı hedefin içinde var mı?"
1. 192'nin içinde 128 var mı? **Evet (1)**. Kalan = 192 - 128 = 64
2. Kalan 64'ün içinde 64 var mı? **Evet (1)**. Kalan = 64 - 64 = 0
3. Sayımız sıfırlandığı için geri kalan tüm bitlere **0** yazıyoruz.

| Değer | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binary** | **1** | **1** | **0** | **0** | **0** | **0** | **0** | **0** |

Sonuç: **`11000000`**

---

### 🌟 Maksimum ve Minimum Değerler

Bir oktet içindeki tüm bitler `0` olursa:
`00000000` = **0**

Bir oktet içindeki tüm bitler `1` olursa:
`11111111` = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = **255**

İşte bu nedenle bir IP adresinin herhangi bir okteti minimum `0`, maksimum `255` değerini alabilir!
