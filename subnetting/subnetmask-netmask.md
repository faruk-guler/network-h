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
