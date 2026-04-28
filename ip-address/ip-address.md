# IP Adresi Nedir?

IP Adresi (Internet Protocol Address), bir ağa bağlı her cihazın sahip olduğu **sayısal kimlik numarasıdır.**
Tıpkı bir evin posta adresi gibi — veri paketi nereye gönderileceğini bu adres sayesinde bulur.

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


🧪🧪 IP adresi Network ve Host olmak üzere iki bölümden oluşmaktadır ve Adres Sınıflarına göre farklılık göstermektedir. (IPv4 örneği)

```
|Network |host  | -----> Örnek B Class
|192.168 |32.170|

|Class  |Network         |host       |
A ----> |10.             |.0.0.0     |
B ----> |172.16.         |.0.0       |
C ----> |192.168.0.      |.0         |
```
