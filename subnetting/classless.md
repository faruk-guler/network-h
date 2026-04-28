#   SINIFSIZ AĞ MİMARİSİ (CLASSLESS)

💊💊 VLSM (Variable Length Subnet Masking)

Geleneksel, katı IP sınıf kurallarını yıkarak, devasa bir ağı farklı boyutlardaki (farklı kapasitelerdeki) alt ağlara bölme teknolojisidir.
Ağdaki IP israfını azaltmayı amaçlar.
```
Mantık: "Subnetting" (Ağı parçalara ayırma)
Özet: Aynı ağ içinde hem 2 kişilik hem 50 kişilik odalar (alt ağlar) oluşturmanıza izin verir.
```

💊💊 CIDR (Classless Inter-Domain Routing)
Subnet Mask'ın daha net ve anlaşılır bir biçimde gösterimidir. IP adreslerini ve ağları verimli bir şekilde "bölmek" için kullanılır. Aslında ISP’lerin (internet servis sağlayıcıların), bir firma ya da ev kullanıcısı için bir adres ayırmak için kullandıkları yöntemde budur.

```
CIDR, IP adresinin sonuna eklenen bir eğik çizgi ve sayı ile gösterilir. [/*]
Bu sayı, ağın kaç bitlik kısmının ağ adresi olduğunu veya bit’lerin soldan sağa kaç tanesinin 1 olduğunu gösterir.

Mantık: "Supernetting" (Ağları birleştirme).
Özet: Birçok küçük IP bloğunu tek bir büyük blok altında toplayıp internet trafiğini rahatlatır.

Örnek:
10.5.83.0/24 Buradaki "/24" IP adresinin ilk 24 biti Ağ, kalan 8 biti ise Hostlar için kullanılır.

|CIDR  |Binary                                 |Decimal
/8  => 11111111.00000000.00000000.00000000 --> 255.0.0.0
--
/24 => 11111111.11111111.11111111.00000000 --> 255.255.255.0
/25 => 11111111.11111111.11111111.10000000 --> 255.255.255.128
/26 => 11111111.11111111.11111111.11000000 --> 255.255.255.192
--
--
--
## 💊 Buradaki "1" ler network'ü temsil ederken "0" lar hostları temsil eder.

😉💡 Her ikisi de artık "A, B, C sınıfı" gibi eski kurallara uymadığımız için hayatımızdadır.
```
