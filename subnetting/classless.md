# 😄 Classless (Sınıfsız) Ağ Mimarisi

Modern yöntemdir. Sabit sınıf mantığını kaldırır ve IP adreslerini ihtiyaca göre böler. Yani kaç IP gerekiyorsa o kadar verilir (/24, /23 gibi). Örneğin 510 IP gerekiyorsa tam ona uygun bir blok verilir, ne fazla ne eksik olur. Bu yüzden IP israfını büyük ölçüde önler.
> | Bir şirket 900 IP istiyor. CIDR ile tam ihtiyaca uygun /22 bloğu (1022 IP) verilir. Sadece ~120 IP boşta kalır, geri kalan tüm adresler verimli kullanılır.

### 🥺 Classful (Eski Yöntem)

IP adreslerini A, B, C gibi sabit gruplara ayıran eski sistemdir. Yani ağlar “hazır paketler” halinde gelir. Örneğin 500 IP’ye ihtiyacın olsa bile sana ya çok küçük ya da çok büyük bir blok verilir (mesela 65.000 IP’lik Class B gibi), bu yüzden IP adresleri boşa harcanır.
> | Bir şirketin 900 IP'ye ihtiyacı var. Class C (254 IP) yetmez, mecburen Class B (65.000 IP) almak zorunda kalır. Kullanılan 900 IP dışında ~64.100 IP adresi çöpe gider.
---

## 💊💊 CIDR (Classless Inter-Domain Routing)
Subnet Mask'ın daha net ve anlaşılır bir biçimde gösterimidir. Eski sınıf tabanlı adresleme sisteminin yerini almak üzere 1993 yılında tanıtıldı.  IP adreslerini ve ağları verimli bir şekilde "bölmek" için kullanılır. Aslında ISP’lerin (internet servis sağlayıcıların), bir firma ya da ev kullanıcısı için bir adres ayırmak için kullandıkları yöntemde budur.

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
/24 => 11111111.11111111.11111111.00000000 --> 255.255.255.0 > 8 + 8 + 8 + 0 = 24
/25 => 11111111.11111111.11111111.10000000 --> 255.255.255.128
/26 => 11111111.11111111.11111111.11000000 --> 255.255.255.192
--
--
--
## 💊 Buradaki "1" ler network'ü temsil ederken "0" lar hostları temsil eder.

😉💡 Her ikisi de artık "A, B, C sınıfı" gibi eski kurallara uymadığımız için hayatımızdadır.
```

## 🖧 VLSM (Variable Length Subnet Masking)

Geleneksel, katı IP sınıf kurallarını yıkarak, devasa bir ağı farklı boyutlardaki (farklı kapasitelerdeki) alt ağlara bölme teknolojisidir.
Ağdaki IP israfını azaltmayı amaçlar.
```
Mantık: "Subnetting" (Ağı parçalara ayırma)
Özet: Aynı ağ içinde hem 2 kişilik hem 50 kişilik odalar (alt ağlar) oluşturmanıza izin verir.

| IP | Subnet Mask |
192.168.1.1 255.255.255.0
192.168.1.1 /24

```
https://jodies.de/ipcalc
