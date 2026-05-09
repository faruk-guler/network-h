# 😷 Subnet Mask/Netmask Nedir?

Bir IP adresinin hangi kısmının ağ (network) ve hangi kısmının cihaz (host) olduğunu belirleyen bir parametredir.

Yani, ağ maskesi, bir IP adresinin hangi kısmının ağla, hangi kısmının ise o ağdaki cihazlarla ilişkili olduğunu ayırır. Daha sonra bunları kullanarak, diğer cihazlarla iletişim kurmanın yolunu bulmaya çalışır. Normal şartlarda aynı ağda bulunmayan cihazlar birbirleri  ile haberleşemez! bu durumda iletişim için bir router (yönlendirici) gerekir.

- Bir cihaz IP adresi ile subnet maskını mantıksal olarak "AND" işlemine tabi tutar, çıkan değer cihazın network adresi olur. Cihaz hangi networkte olduğunu öğrendikten sonra  bulunduğu ağ içindeki diğer cihazlara doğrudan erişebilir.

AND kuralı: "Her iki bit de 1 ise sonuç 1, diğer tüm durumlarda sonuç 0" ✅

```
IP Adresi: 172.16.1.1 =  10101100.00010000.00000001.00000001
                         ⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
Netmask: 255.255.0.0  =  11111111.11111111.00000000.00000000
-------------------------------------------------------------
Network: 172.16.0.0   =  10101100.00010000.00000000.00000000  > 172.16.0.0 ağındayız
```
## Network ve Broadcast Hesaplama Örneği: 87.121.165.49/14

```
🔢 Adım 1: Binary'den Decimal'e Dönüşüm

IP Adresi: 87.121.165.49 = 01010111.01111001.10100101.00110001
NetMask (/14): 11111111.11111100.00000000.00000000 = 255.252.0.0
               | | |     ↑14 bit network↑ ↑18 bit host↑

🔢 Adım 2: Network Adresi (AND İşlemi)

IP:        01010111.01111001.10100101.00110001
Mask:      11111111.11111100.00000000.00000000
           -----------------------------------
Network:   01010111.01111000.00000000.00000000
Decimal:   87     . 120    . 0      . 0

✅ Network Adresi: 87.120.0.0

🔢 Adım 3: Broadcast Adresi (Host Bitleri = 1)
Broadcast Adresi;
Network:   01010111.01111000.00000000.00000000
Hostleri 1 yap:
           01010111.01111011.11111111.11111111
Decimal:   87     . 123    . 255    . 255

✅ Broadcast Adresi: 87.123.255.255
```
> 💡 Her zaman en sağdan ve 2⁰ ile başlayın.

> 💡 Decimalden Binary'e dönüşüm mümkündür.

## >_ Subnet Mask neden gerekli?

Neden Subnet'lere ihtiyaç duyarız tek bir ağ yeterli olmaz mı?

Çok sayıda cihazın bulunduğu devasa ağ hayal edelim, bir bilgisayar diğer cihazlarla iletişim kurması gerektiğinde, ona ulaşmak için bir yayın (broadcast) kullanır. Ağdaki tüm cihazlara yapılan bu çağrı trafik oluşturarak ağı yavaşlatır.

- En büyük nedeni Broadcast trafiğini önlemektir, Bu yüzden ağın küçük alt ağlara bölünmesi gerekir.
- Router kullanılarak ağlar parçalanır ve fiziksel olarak ayrılır.
- Broadcast Router' dan geçemediği için yalnızca bir ağ içerisinde hapsolur ve diğer ağlara erişemez. Bu sayede trafik sorunu ortadan kalkar.
- Güvenliği sağlamak


## Default Subnet Mask
```
|Class  |Network          |Host       |

A ----> |255.             |.0.0.0     |
B ----> |255.255.         |.0.0       |
C ----> |255.255.255.     |.0         |
```

## Üsler Tablosu (İkinin Kuvvetleri)
```
+--------------+------------------+
| Gösterim(2ⁿ) | Decimal Değer    |
+--------------+------------------+
| 2^*          | **               |
| 2^7          | 128              |
| 2^6          | 64               |
| 2^5          | 32               |
| 2^4          | 16               |
| 2^3          | 8                |
| 2^2          | 4                |
| 2^1          | 2                |
| 2^0          | 1                |
+--------------+------------------+

Özet:
2⁰ = 1
2¹ = 2
......

2⁷ = 2 × 2 × 2 × 2 × 2 × 2 × 2 = 128
```
> 💡 Üslü sayıların kuralı gereği herhangi bir sayının 0. kuvveti 1 olur.
