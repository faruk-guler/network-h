# 😄 Classless (Sınıfsız) Ağ Mimarisi

Modern yöntemdir. Sabit sınıf mantığını kaldırır ve IP adreslerini ihtiyaca göre böler. Yani kaç IP gerekiyorsa o kadar verilir (/24, /23 gibi). Örneğin 510 IP gerekiyorsa tam ona uygun bir blok verilir, ne fazla ne eksik olur. Bu yüzden IP israfını büyük ölçüde önler.
> | Bir şirket 900 IP istiyor. CIDR ile tam ihtiyaca uygun /22 bloğu (1022 IP) verilir. Sadece ~120 IP boşta kalır, geri kalan tüm adresler verimli kullanılır.

### 🥺 Classful (Eski Yöntem)

IP adreslerini A, B, C gibi sabit gruplara ayıran eski sistemdir. Yani ağlar “hazır paketler” halinde gelir. Örneğin 500 IP’ye ihtiyacın olsa bile sana ya çok küçük ya da çok büyük bir blok verilir (mesela 65.000 IP’lik Class B gibi), bu yüzden IP adresleri boşa harcanır.
> | Bir şirketin 900 IP'ye ihtiyacı var. Class C (254 IP) yetmez, mecburen Class B (65.000 IP) almak zorunda kalır. Kullanılan 900 IP dışında ~64.100 IP adresi çöpe gider. Gereksiz Broadcast trafiği olur ve Routerlerde CPU yükü artar.
---

## 💊 CIDR (Classless Inter-Domain Routing)
Subnet Mask'ın daha net ve anlaşılır bir biçimde gösterimidir. Eski sınıf tabanlı adresleme sisteminin yerini almak üzere 1993 yılında tanıtıldı.  IP adreslerini ve ağları verimli bir şekilde "bölmek" için kullanılır. Aslında ISP’lerin (internet servis sağlayıcıların), bir firma ya da ev kullanıcısı için bir adres ayırmak için kullandıkları yöntemde budur.

```
Mantık: "Supernetting" (Ağları birleştirme).
Özet: Birçok küçük IP bloğunu tek bir büyük blok altında toplayıp internet trafiğini rahatlatır.

Örnek:
10.5.83.0/24 Buradaki "/24" IP adresinin ilk 24 biti Ağ, kalan 8 biti ise Hostlar için kullanılır.

|CIDR  |Binary                                 |Decimal
/8  => 11111111.00000000.00000000.00000000 --> 255.0.0.0     > 8 + 0 + 0 + 0 = 8
...
/21 => 11111111.11111111.11111000.00000000 --> 255.255.248.0 > 8 + 8 + 5 + 0 = 21
...
/24 => 11111111.11111111.11111111.00000000 --> 255.255.255.0 > 8 + 8 + 8 + 0 = 24
/25 => 11111111.11111111.11111111.10000000 --> 255.255.255.128
/26 => 11111111.11111111.11111111.11000000 --> 255.255.255.192
...
...
/30 => 11111111.11111111.11111111.11111100 --> Subnet en fazla /30 olabilir. > Toplam IP = 4 Broadcast ve Network çıkar = 2
--
/32 => 11111111.11111111.11111111.11111111 --> 255.255.255.2555 Toplam IP = 0

🔥 Buradaki "1" ler network'ü temsil ederken "0" lar hostları temsil eder.
```

>  💡 CIDR, IP adresinin sonuna eklenen bir eğik çizgi ve sayı ile gösterilir. [/*]
Bu sayı, ağın kaç bitlik kısmının ağ adresi olduğunu ve bit’lerin soldan sağa kaç tanesinin (1) olduğunu gösterir

### 📌 Şirkette 1500 IP adresine ihtiyacım var?

```
2¹⁰ = 1024   ❌ Yetmez
2¹¹ = 2048   ✅ Yeter (2048 ≥ 1500)
→ Host için 11 bit lazım!

CIDR: 32 - 11 = 21
✅ Sonuç: /21
```
> 💡 1500 Hostluk bir network ayarlamak isterseniz 1'leri sola kaydırarak yer açmanız gerekir.

## 🖧 VLSM (Variable Length Subnet Masking)

CIDR'nin bir alt kümesidir. Değişken Uzunluklu Alt Ağ Maskesi anlamına gelir. Aynı ağ bloğu içinde farklı boyutlarda subnetler oluşturmanıza olanak tanıyan tekniktir.
```
Mantık: "Subnetting" (Ağı parçalara ayırma)
Özet: Aynı ağ içinde hem 2 kişilik hem 50 kişilik odalar (alt ağlar) oluşturmanıza izin verir.

| IP | Subnet Mask |
192.168.1.1 255.255.255.0
192.168.1.1 /24
```
## HESAP ARAÇLARI:
https://jodies.de/ipcalc
