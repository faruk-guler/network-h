# 🔄 Hexadecimal ↔ Binary Dönüşüm

## Neden Hexadecimal?

Binary (ikili) sayılar uzun ve okunması zordur. Örneğin `11000000101010000000000100000001` yazmak yerine bunu 4'erli gruplara ayırıp kısa bir gösterimle ifade edebiliriz. İşte **Hexadecimal** (onaltılık) tam bunu yapar.

> 💡 **Altın Kural:** Her **1 Hex karakteri** tam olarak **4 bit (1 Nibble)** ile eşleşir. Bu yüzden dönüşüm çok mekaniktir — ezberlemek değil, tablodan okumak yeterlidir.

---

## Hex ↔ Binary Eşleştirme Tablosu

| Hex | Binary | Decimal |
|:---:|:------:|:-------:|
| **0** | `0000` | 0 |
| **1** | `0001` | 1 |
| **2** | `0010` | 2 |
| **3** | `0011` | 3 |
| **4** | `0100` | 4 |
| **5** | `0101` | 5 |
| **6** | `0110` | 6 |
| **7** | `0111` | 7 |
| **8** | `1000` | 8 |
| **9** | `1001` | 9 |
| **A** | `1010` | 10 |
| **B** | `1011` | 11 |
| **C** | `1100` | 12 |
| **D** | `1101` | 13 |
| **E** | `1110` | 14 |
| **F** | `1111` | 15 |

> 💡 Hexadecimal'de `A=10, B=11, C=12, D=13, E=14, F=15` olduğunu hatırlayın. Toplam 16 sembol (0–F) kullanılır.

---

## Hex → Binary Dönüşüm

Her Hex karakterini tablodaki 4 bitlik karşılığıyla değiştirin. Hepsi bu kadar.

### 📌 Örnek 1: MAC Adresi

```text
MAC Adresi: 00:1A:2B:3C:4D:5E

Hex :  0    0  :  1    A  :  2    B  :  3    C  :  4    D  :  5    E
       ↓    ↓     ↓    ↓     ↓    ↓     ↓    ↓     ↓    ↓     ↓    ↓
Binary: 0000 0000  0001 1010  0010 1011  0011 1100  0100 1101  0101 1110
```

### 📌 Örnek 2: IPv6 Adresi (Bir Hextet)

```text
Hextet: 2001

Hex :  2    0    0    1
       ↓    ↓    ↓    ↓
Binary: 0010 0000 0000 0001
```

---

## Binary → Hex Dönüşüm

Binary sayıyı **sağdan sola 4'erli gruplara** ayırın ve her grubu tablodaki Hex karşılığıyla değiştirin.

### 📌 Örnek: IP Adresinin İlk Okteti

```text
192 decimal = 11000000 binary

4'erli grupla:  1100  0000
                 ↓     ↓
Hex:             C     0

Sonuç: 192 = C0 (Hex)
```

### 📌 Örnek: Subnet Mask

```text
255.255.255.0

Binary : 11111111 . 11111111 . 11111111 . 00000000
4'erli :  FF          FF          FF          00

Hex    : FF.FF.FF.00
```

---

## 🌐 Ağ Dünyasında Nerelerde Karşılaşırız?

| Kullanım | Format | Örnek |
|:---|:---|:---|
| **MAC Adresi** | 6 byte, Hex ile gösterilir | `00:1A:2B:3C:4D:5E` |
| **IPv6 Adresi** | 8 hextet, Hex ile gösterilir | `2001:0db8:85a3::8a2e` |
| **Renk Kodları (Web)** | 3 byte RGB | `#FF5733` |

---

## 🔔 Hızlı Doğrulama Yöntemi

Elinizde bir Hex sayı var ve doğruluğunu kontrol etmek istiyorsanız:

```text
Hex: C0  →  C=12, 0=0

C = 12 × 16¹ = 192
0 =  0 × 16⁰ =   0
                ───
Toplam:         192  ✅ (192.168.1.1'in ilk okteti)
```

> 💡 **İpucu:** Hex → Decimal dönüşümde her basamak, 16'nın kuvvetleriyle çarpılır (sağdan sola: 16⁰=1, 16¹=16, 16²=256...).
