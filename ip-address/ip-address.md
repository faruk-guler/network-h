# IP Adresi Nedir?

IP Adresi (Internet Protocol Address), bir ağa bağlı her cihazın sahip olduğu **sayısal kimlik numarasıdır.**
Tıpkı bir evin posta adresi gibi — veri paketi nereye gönderileceğini bu adres sayesinde bulur. OSI modelinde 3. katmanda bulunur. 32 bittir ve (.) ile ayrılır.

---

## Günlük Hayattan Örnek

Sen bir web sitesine girdiğinde aslında şu olur:

```
Senin cihazın              →    google.com sunucusu
(192.168.1.5)              →    (142.250.74.46)
"Bana ana sayfayı gönder"  →    "Tamam, işte veri"
```

İkisi de birbirini IP adresi sayesinde bulur.

---

## İki Versiyonu Vardır

| | IPv4 | IPv6 |
|---|---|---|
| Örnek | 192.168.1.1 | 2001:0db8:85a3::8a2e |
| Format | 32 bit, 4 oktet | 128 bit |
| Toplam adres | ~4,3 milyar | Yaklaşık 340 Undesilyon |
| Durum | Hâlâ yaygın | Geçiş süreci devam ediyor |

```
192.           168.          1.             10.
[32]          [24]                [11]          [3] [1]
[1]1000000    [1]0101000     00000[0]01    00001[0]1[0]
8 bit     +   8 bit     +  8 bit      +  8 bit    =    32 bit
```

## 🧪🧪 IP Adresi Formatı
IP "Network ID" ve "Host ID" olmak üzere iki bölümden oluşmaktadır ve Adres Sınıflarına göre farklılık göstermektedir. Network ağı, Host ise uç cihazları ifade eder.
```
xxx . xx. xx .   xx
└─────────────┘ └──┘
Network ID      Host ID
```
```
|Class  |Network         |Host       |
A ----> |10.             |.0.0.0     |
B ----> |172.16.         |.0.0       |
C ----> |192.168.0.      |.0         |

|Network |Host  |
|192.168 |32.170| > B class örneği
```
> 💡 Host ID leri Min 0, Max 254 olabilir (C Class'ta ise Host ID minimum 1'dir, 0 olamaz.)
