# 🖧 IP Adresi Nedir?

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

## IP adresinin iki (2) versiyonu vardır

| | IPv4 | IPv6 |
|---|---|---|
| Örnek | 192.168.1.1 | 2001:0db8:85a3::8a2e |
| Format | 32 bit, 4 oktet | 128 bit |
| Toplam adres | ~4,3 milyar | Yaklaşık 340 Undesilyon |
| Durum | Hâlâ yaygın | Geçiş süreci devam ediyor |


## 🧪🧪 IP Adresi Formatı
IP "Network ID" ve "Host ID" olmak üzere iki bölümden oluşmaktadır ve Adres Sınıflarına göre farklılık göstermektedir. Network ağı, Host ise uç cihazları ifade eder.
```
xxx . xx. xx .   xx
└─────────────┘ └──┘
Network ID      Host ID
```
```
|Class   |Network         |Host       |
|A ----> |10.             |.0.0.0     |
|B ----> |172.16.         |.0.0       |
|C ----> |192.168.0.      |.0         |

|Network |Host  |
|172.16  |32.170| > B class örneği
```

> 💡 Host ID, teorik olarak min 0 (Network Adresi) ile max 255 (Broadcast Adresi) değerlerini alır.

> 💡 Ancak bu iki uç adres cihazlara atanamaz. Cihazlara atanabilir aralık her subnet'te .1 ile .254 arasındadır.
