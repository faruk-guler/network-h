# 🖧 IP Adresi Nedir?

IP Adresi (Internet Protocol Address), bir ağa bağlı her cihazın sahip olduğu **sayısal kimlik numarasıdır.**
Tıpkı bir evin posta adresi gibi — veri paketi nereye gönderileceğini bu adres sayesinde bulur. OSI modelinde **3. katmanda (Ağ Katmanı)** çalışır. IPv4 adresleri **32 bit** uzunluğunda olup nokta (.) ile ayrılırken, IPv6 adresleri **128 bit** uzunluğunda olup iki nokta üst üste (:) ile ayrılır.

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
| Format | 4 Byte/32 bit, 4 oktet | 16 Byte/128 bit, 8 hextet |
| Toplam adres | ~4,3 milyar | ≈ 3,4 × 10³⁸ (340 undesilyon) |
| Durum | Hâlâ yaygın | Geçiş süreci devam ediyor |


## 🧪 IP Adresi Formatı
IP "Network ID" ve "Host ID" olmak üzere iki bölümden oluşmaktadır ve Adres Sınıflarına göre farklılık göstermektedir. Network ağı, Host ise uç cihazları ifade eder.
```
xxx . xxx . xx .  xx
└────────┘ └────────┘
 Network ID     Host ID
```
> 💡 Yukarıdaki örnek B sınıfı adresleme yapısını göstermektedir.

---

## Sınıflı (Classful) IP Adresleme Yapısı
Bu sistem, IP adresinin hangi sınıf olduğuna ilk oktetine (bölümüne) bakarak karar verir. IPv4 adresleri tarihsel olarak A, B, C, D ve E olmak üzere 5 sınıfa ayrılmıştır.

## Özel (Private) IP Blokları (RFC 1918)
Modemlerimizde veya iç ağlarımızda gördüğümüz, internete doğrudan çıkamayan adreslerdir. Üç ana aralık vardır: `10.x.x.x`, `172.16–31.x.x` ve `192.168.x.x`. Bu adresler internette yönlendirilemez; router üzerinden NAT ile public IP'ye dönüştürülürler.

> 💡 Host bitlerinin tamamı **0** olduğunda **Network Adresi**, tamamı **1** olduğunda **Broadcast Adresi** oluşur. Bu iki uç adres cihazlara **atanamaz**; atanabilir aralık her subnet'te bunların arasındaki adreslerdir.
