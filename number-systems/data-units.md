# 🗃️ Veri Birimleri:

## Octet
🔍 "Octet" bir sayı sistemi değildir. 8 bitten oluşan bir veri birimi/gruplama kavramıdır. Octal ile karıştırılmamalıdır.
| Sistem | Slogan | Kök | Örnek | Kullanım |
|---|---|---|---|---|
| Octet | 8 parçalı | Latince “octo” (8) | her octet min 0, max 255 değerini alabilir | IPv4 adresleri 4 octet'ten oluşur |

## Hextet
🔍 "Hextet" bir sayı sistemi değildir. 16 bitten oluşan bir veri birimi/gruplama kavramıdır. Hexadecimal ile ilişkilidir ama aynı şey değildir.

| Sistem | Slogan | Kök | Örnek | Kullanım |
|--------|--------|-----|-------|-------|
| Hextet | 16 bitlik grup | "Hex" (16) + "tet" (grup) | Her hextet 0x0000–0xFFFF (0–65535) arası değer alır | IPv6 adresleri 8 hextet'ten oluşur |

## Nibble
🔍 "Nibble" bir sayı sistemi değildir. 4 bitten oluşan en küçük adreslenebilir veri grubudur. Binary'den Hexadecimal'e dönüşümün temel yapı taşıdır.
 
| Sistem | Slogan | Kök | Örnek | Kullanım |
|--------|--------|-----|-------|-------|
| Nibble | 4 bitlik yarım bayt | İngilizce "nibble" (ısırmak) | `1010` = `A` (hex) | Her hex karakteri tam olarak 1 nibble'a karşılık gelir |
 
> 💡 **İpucu:** 1 Octet = 2 Nibble = 8 bit. Bu yüzden binary→hex dönüşümünde ikişer ikişer gruplandırılır.
 
---
 
- ASCII tablosu (harf → binary → decimal → hex karşılıkları) tablosuna ulaşmak için:
https://www.asciitable.com
> 📝 **Not:** Standart ASCII 7-bittir (0–127 arası). Modern sistemler genellikle 8-bit genişletilmiş ASCII veya **UTF-8** kullanır; UTF-8 bugün web ve işletim sistemlerinde fiili standarttır.
