# 😄 Classless (Sınıfsız) Ağ Mimarisi

Modern yöntemdir. Sabit sınıf mantığını kaldırır ve IP adreslerini ihtiyaca göre böler. Yani kaç IP gerekiyorsa o kadar verilir (/24, /23 gibi). Örneğin 510 IP gerekiyorsa tam ona uygun bir blok verilir, ne fazla ne eksik olur. Bu yüzden IP israfını büyük ölçüde önler.
> Bir şirket 900 IP istiyor. CIDR ile tam ihtiyaca uygun /22 bloğu (1022 IP) verilir. Sadece ~120 IP boşta kalır, geri kalan tüm adresler verimli kullanılır.

### 🥺 Classful (Eski Yöntem)

IP adreslerini A, B, C gibi sabit gruplara ayıran eski sistemdir. Yani ağlar “hazır paketler” halinde gelir. Örneğin 500 IP’ye ihtiyacın olsa bile sana ya çok küçük ya da çok büyük bir blok verilir (mesela 65.000 IP’lik Class B gibi), bu yüzden IP adresleri boşa harcanır.
> Bir şirketin 900 IP'ye ihtiyacı var. Class C (254 IP) yetmez, mecburen Class B (65.000 IP) almak zorunda kalır. Kullanılan 900 IP dışında ~64.100 IP adresi çöpe gider. Gereksiz Broadcast trafiği olur ve Routerlerde CPU yükü artar.
---

## 💊 CIDR (Classless Inter-Domain Routing)
Subnet Mask'ın daha net ve anlaşılır bir biçimde gösterimidir. IP adreslerini sınıfsız (class A/B/C'ye bakmadan) bölme yöntemidir. 1993 yılında tanıtılmıştır. IP adreslerini ve ağları verimli bir şekilde "bölmek", Routing tabloları küçültmek için kullanılır. Aslında ISP’lerin (internet servis sağlayıcıların), bir firma ya da ev kullanıcısı için bir adres ayırmak için kullandıkları yöntem de budur.

```
Mantık: CIDR Bit Yapısı
Özet: Her "/" değeri, IP adresinin kaç bitinin ağa ait olduğunu gösterir.

Örnek:
10.5.83.0/24 Buradaki "/24" IP adresinin ilk 24 biti Ağ, kalan 8 biti ise Hostlar için kullanılır.

|CIDR  |Binary                                 |Decimal                       |Usable Host
/8  => 11111111.00000000.00000000.00000000 --> 255.0.0.0
...
/21 => 11111111.11111111.11111000.00000000 --> 255.255.248.0                   32-21 = 11 (2¹¹ = 2048) -2 = 2046
...
/24 => 11111111.11111111.11111111.00000000 --> 255.255.255.0
/25 => 11111111.11111111.11111111.10000000 --> 255.255.255.128
/26 => 11111111.11111111.11111111.11000000 --> 255.255.255.192                 32-26 = 6 (2⁶ = 64) - 2 = 62
...
...
/32 => 11111111.11111111.11111111.11111111 --> 255.255.255.255 

🔥 "1" ler network'ü temsil ederken "0" lar hostları temsil eder.
🔥 /32 Toplam IP = 1
```

> 💡 CIDR, IP adresinin sonuna eklenen bir eğik çizgi ve sayı ile gösterilir. [/*]
Bu sayı, ağın kaç bitlik kısmının ağ adresi olduğunu ve bit’lerin soldan sağa kaç tanesinin (1) olduğunu gösterir.
> 
> 💡 **Prefix**, IP adresinin ağ kısmını belirten bit sayısıdır. Örnek: `/18`
> 
> 💡 Cihazlara IP atanabilen en küçük subnet /30'dur. > Toplam IP = 4 Broadcast ve Network çıkarılınca kalan = 2
>
> 💡 CIDR'de / sonraki sayı ağ(network) bitini gösterir. 32'den çıkarılan kısım host bit adedini verir ve kullanılabilir host sayısı 2ⁿ − 2 formülüyle hesaplanır.

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

CIDR'nin gelişmiş bir alt kümesidir. Değişken Uzunluklu Alt Ağ Maskesi anlamına gelir. Aynı ağ bloğu içinde farklı boyutlarda subnetler oluşturmanıza olanak tanıyan tekniktir. IP israfı CIDR' e göre dahada azalmıştır.
```
📌 Elimizdeki ağ: 192.168.10.0/24  →  254 kullanılabilir IP

192.168.10.0    → ağ adresi   ❌
192.168.10.1
192.168.10.2
192.168.10.3
...              →  254 cihaz tek odada, duvarsız, bölümsüz
192.168.10.254
192.168.10.255  → broadcast   ❌

VLSM ile içini böl:
───────────────────────
        ↓
192.168.10.0/24
│
├── 192.168.10.0/25    → Yazılım   → 126 IP  (ihtiyaç: 100)
├── 192.168.10.128/26  → Satış     →  62 IP  (ihtiyaç:  50)
├── 192.168.10.192/27  → Muhasebe  →  30 IP  (ihtiyaç:  25)
├── 192.168.10.224/28  → Sunucular →  14 IP  (ihtiyaç:  10)
└── 192.168.10.240/29  → Müdürlük  →   6 IP  (ihtiyaç:   5)
```
> 💡 Aynı ağ içinde; örneğin hem 2 kişilik hemde 50 vb. kişilik odalar (alt ağlar) oluşturmanıza izin verir.

## HESAP ARAÇLARI:
- [IP Subnet Calculator](https://farukguler.com/app/ip-subnet-calculator)
- [IP Calculator](https://jodies.de/ipcalc)
